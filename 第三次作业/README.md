
```
#include <eosiolib/eosio.hpp>
#include <eosiolib/print.hpp>
#include <eosiolib/asset.hpp>
#include <eosiolib/action.hpp>
#include <eosiolib/symbol.hpp>
#include <eosiolib/singleton.hpp>
#include <eosiolib/print.hpp>
#include <eosiolib/transaction.hpp>
#include <eosiolib/crypto.h>
#include <eosiolib/dispatcher.hpp>
using namespace eosio;
using namespace std;
class [[eosio::contract]] kpi : public contract {
public:
    using contract::contract;
    struct [[eosio::table]] work{
        uint64_t id;
        name worker;
        asset token;
        uint64_t score;
        uint64_t creat_time= current_time();
        uint64_t primary_key() const {  return id; }
        EOSLIB_SERIALIZE( work, (id)(worker)(token)(score)(creat_time))
    };
    typedef eosio::multi_index<name("work"), work> work_index;

    [[eosio::action]]
    void test (name from, uint64_t score){
        work_index works(_self,_self.value);
        works.emplace(_self, [&](auto& work) {
            work.id = works.available_primary_key();
            work.worker = from;
            work.score = score;
            work.token = asset(score * 10,symbol("EOS", 0));
        });
    }
};
EOSIO_DISPATCH(kpi, (test))   //公开EOS方法
```
### 命令步骤
* eosio-cpp -o kpi.wasm kpi.cpp --abigen  
* cleos set contract kpi /root/eos/contracts/eosio.contracts/kpi -p kpi@active
* cleos push action kpi test '["account1", 1]' -p kpi
* cleos push action kpi test '["account2", 2]' -p kpi
* cleos get table kpi kpi work
```
{
  "rows": [{
      "id": 0,
      "worker": "account1",
      "token": "10 EOS",
      "score": 1,
      "creat_time": "1550423660000000"
    },{
      "id": 1,
      "worker": "account2",
      "token": "20 EOS",
      "score": 2,
      "creat_time": "1550423700000000"
    },{
      "id": 2,
      "worker": "account1",
      "token": "10 EOS",
      "score": 1,
      "creat_time": "1550488122500000"
    }
  ],
  "more": false
}
```

服务器地址： 180.76.234.155 用户名称 kpi scope kpi  表名 work
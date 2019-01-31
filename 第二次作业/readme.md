## 创建game账户
```
cleos create account eosio game EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu
```
## 将第一节创建的token转给game账户
### 通过命令转账
* 上节课的token创建到了homework1st账户内，共999999.0000 WYWY，已经转给homework1st账户99.0000 WYWY
* 向game账户内转账9900.0000 WYWY
```
cleos push action homework1st issue '["game", "9900.0000 WYWY" "second homework transfer"]' -p homework1st@active     
cleos get currency balance homework1st game

输出显示： 9900.0000 WYWY
```
### 通过合约转账
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
class hello : public contract {
  public:
      using contract::contract;

      [[eosio::action]]
      void hi( name user ) {
		print("game start");
		require_auth(_self);
		auto values=user.value;
        	print("hello user value:",values);
		print( ",: Hello ,: ", user);
      		action(permission_level{_self, name("active")},
              	name("eosio.token"), name("transfer"),
                std::make_tuple(_self, user, asset(1, symbol("EOS", 4)),
                                std::string("game send  eos")) ).send();
	}
	
	[[eosio::action]]
	void delay(string memo){
		 eosio::transaction t{};
       		 t.actions.emplace_back(eosio::permission_level(_self, name("active")),
        	                       name("test3"), name("hi"),
                               std::make_tuple(name("test1")));
        	t.delay_sec = 1;
        	t.send(1, _self, false);
		print("delay end");
	}
	
    [[eosio::action]]
    void homework2( name user ) {
            print("start homework2");
            require_auth(_self);
            action(permission_level{_self, name("active")},
            name("homework1st"), name("transfer"),
            std::make_tuple(_self, user, asset(100, symbol("WYWY", 4)),
                            std::string("homework1st send WYWY")) ).send();
    }


};


#define EOSIO_DISPATCH_CUSTOM(TYPE, MEMBERS) \
extern "C" { \
   void apply( uint64_t receiver, uint64_t code, uint64_t action ) { \
   auto self = receiver; \
      if(( code == self&&action != name("transfer").value) || (code == name("hello").value) && action == name("transfer").value){\
        switch( action ) { \
            EOSIO_DISPATCH_HELPER( TYPE, MEMBERS ) \
         } \
         /* does not allow destructor of this contract to run: eosio_exit(0); */ \
      } \
   } \
} \


EOSIO_DISPATCH_CUSTOM( hello, (hi)(delay)(transfer)(homework2))
                                                                    
```
* 编译 部署合约
```
eosio-cpp -o hello.wasm hello.cpp --abigen
cleos set contract hello /root/eos/contracts/eosio.contracts/hello -p hello@active
```
* 获取permission
```
cleos set account permission hello active '{"threshold": 1, "keys":[{"key":"EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu", "weight": 1}], "accounts": [{"permission": {"actor": "hello", "permission": "eosio.code"}, "weight": 1}]}' owner -p hello
```
* 执行转账(作业函数)
```
cleos push action hello homework2 '["game"]' -p hello@active 
```
> 只有hello账户有权限，其他账户无权限
![结果](https://github.com/WangYangA9/EOSContractHomework/blob/master/%E7%AC%AC%E4%BA%8C%E6%AC%A1%E4%BD%9C%E4%B8%9A/homework2.png)
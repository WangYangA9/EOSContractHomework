# 作业
* 服务器地址 180.76.234.155 
* 用户名称  homework1st

## 生成自己的账户
```
cleos create account eosio.token homework1st  EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu -p eosio.token@active
```
## 发布合约到账户
```
cleos set contract homework1st /root/eos/contracts/eosio.contracts/eosio.token -p homework1st@active
```
## 创建自己的token
```
cleos push action homework1st create '{"issuer": "homework1st", "maximum_supply": "999999.0000 WYWY"}' -p homework1st@active
```
## 进行转账
```
cleos push action homework1st issue '["homework1st", "99.0000 WYWY" "first homework transfer"]' -p homework1st@active
```
## 查看账户余额
```
cleos get currency balance homework1st homework1st
结果 99.0000 WYWY  用户名称  homework1st
```
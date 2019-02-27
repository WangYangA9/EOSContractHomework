# 作业
```
创建testaaa11111账户
cleos create account eosio testaaa11111 EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu
在账户上发布eosio.token合约
cleos set contract testaaa11111 /root/eos/contracts/eosio.contracts/eosio.token -p testaaa11111@active 
发行代币KPI 数量100万
cleos push action testaaa11111 create '{"issuer": "testaaa11111", "maximum_supply": "1000000.0000 KPI"}' -p testaaa11111@active
创建账户testaaa22222
cleos create account eosio testaaa22222 EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu
```

## 截图
![1](https://github.com/WangYangA9/EOSContractHomework/blob/master/%E7%AC%AC%E5%9B%9B%E6%AC%A1%E4%BD%9C%E4%B8%9A/1%E7%A8%8B%E5%BA%8F%E5%90%AF%E5%8A%A8%E6%88%90%E5%8A%9F%E6%8E%A7%E5%88%B6%E5%8F%B0.png)
![2](https://github.com/WangYangA9/EOSContractHomework/blob/master/%E7%AC%AC%E5%9B%9B%E6%AC%A1%E4%BD%9C%E4%B8%9A/2%E7%A8%8B%E5%BA%8F%E5%90%AF%E5%8A%A8%E5%89%8D%E7%AB%AF%E9%A1%B5%E9%9D%A2.png)
![3](https://github.com/WangYangA9/EOSContractHomework/blob/master/%E7%AC%AC%E5%9B%9B%E6%AC%A1%E4%BD%9C%E4%B8%9A/3%E8%B0%83%E7%94%A8scatter%E8%BD%AC%E8%B4%A6.png)
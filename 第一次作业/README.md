# ��ҵ
* ��������ַ 180.76.234.155 
* �û�����  homework1st

## �����Լ����˻�
```
cleos create account eosio.token homework1st  EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu EOS6be5W2US4LvueqiUAhjEXMyoz25Gf5eyp22tt7SMnH1h98fGUu -p eosio.token@active
```
## ������Լ���˻�
```
cleos set contract homework1st /root/eos/contracts/eosio.contracts/eosio.token -p homework1st@active
```
## �����Լ���token
```
cleos push action homework1st create '{"issuer": "homework1st", "maximum_supply": "999999.0000 WYWY"}' -p homework1st@active
```
## ����ת��
```
cleos push action homework1st issue '["homework1st", "99.0000 WYWY" "first homework transfer"]' -p homework1st@active
```
## �鿴�˻����
```
cleos get currency balance homework1st homework1st
��� 99.0000 WYWY  �û�����  homework1st
```
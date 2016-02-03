# MinerGate API

_Host_: https://api.minergate.com

### Currencies List
| Currency Name | Currency Code (cc) |
| --- | --- |
| Bytecoin | bcn |
| Monero | xmr |
| FantomCoin | fcn |
| QuazarCoin | qcn |
| DigitalNote | xdn |
| MonetaVerde | mcn |
| Dashcoin | dsh |
| Aeon coin | aeon |
| Infinium-8 | inf8 |
| Bitcoin | btc |
| Lytecoin | ltc |


### Non-authorized API methods

#### Methods list
- [get profit currency rating](#profit-rating)
- [get top hasrates by currencies](#top-hashrate)
- [get blockhain info](#blockchain-info)
- [login](#login)

#### Profit rating

_Method_: GET

_Path_: /1.0/pool/profitRating

_Example response_:
```json
["btc", "qcn", "xmr", "bcn"]
```

#### Top hashrate

_Method_: GET

_Path_: /1.0/pool/top/hashrate

_Example response_:
```json
{
"xmr": [
    {
      "hashrate": 536450.558066599,
      "nickname": "nickname1"
    },
    {
      "hashrate": 90208.49551531563,
      "nickname": "nickname2"
    },
    {
      "hashrate": 55373.55420204257,
      "nickname": "nickname3"
    }, ...
  ], 
"bcn" : {
  ...
}, ...}
```

#### Blockchain info

_Method_: GET

_Path_: /1.0/:cc/status

_Example request_: /1.0/bcn/status

_Example response_:
```json
{
  "hash": "1efd43e0d8ae9826278cfddffc2fe2e082c4683910766d7e0c28cb2e386b02b5",
  "height": 930169,
  "orphan": false,
  "timestamp": 1454422483,
  "difficulty": 132222356,
  "prevBlockHash": "e4542479ad51aa6aa61ae91eba62f060362cd4fdf4fc43c6763b4fb5ef5d3aa7",
  "sizeMedian": 5009,
  "blockSize": 14249,
  "txCumulativeSize": 13603,
  "txCount": 10,
  "baseReward": 2163929365089,
  "penalty": 0,
  "reward": 2163938365089,
  "feeSumm": 9000000,
  "alreadyGeneratedCoins": 17879485138156950000,
  "cumulativeTxCount": 2315170,
  "rewardBlocksWindow": 100,
  "fullRewardMaxBlockSize": 20000,
  "instantHashrate": 1101852.9666666666
}
```

#### Login

_Method_: POST

_Path_: /1.0/auth/login

_Parameters_: login(your email), password, totp(2-step authorization token, not-required)

_Example parameters_: 
```json
{
  "login": "your_email@gmail.com",
  "password": "your_password",
  "totp": 123456
}
```

_Example success response_:
```json
{
  "token": "1c2VySWQiOiJibGFja19sdWdhMkBtYW1c2VySWQiOiJibGFja19sdWdhMkBtYW1c2VySWQiOiJibGFja19sdWdhMkBtYW"
}
```
This token you should use in authorized requests.

_Possible errors_:
```json
{
  "error": "WrongEmailOrPassword",
  "message": "Email and Password pair did not authenticate."
}
``` 
```json
{
  "error": "TotpRequired",
  "message": "Two-factor authorization is enabled for this account. Please provide TOTP code."
}
```



### Authorized API methods

#### Methods list
- [get balance](#balance)
- [get transfers](#transfers)
- [get withdrawals](#withdrawals)
- [get workers](#workers)
- [get mining stats](#mining-stats)
- [get affiliate links](#affilliate-links)
- [get affiliates](#ffilliates)
- [get affiliate profits](#ffilliate-profits)
- [get invoices](#invoices)
- [get invoice by token](#invoice)
- [get nickname](#nickname)

#### Balance

_Method_: GET

_Path_: /1.0/balance

_Example response_:
```json
{
  "aeon": "30.66592521533400000000",
  "bcn": "30143.50038210000000000000",
  "btc": "0.00800000000000000000",
  "dsh": "2.80476725202",
  "xdn": "4.53423417000000000000",
  "fcn": "4.14526383581300000000",
  "inf8": "24.88587286959600000000",
  "ltc": "0.10015669000000000000",
  "mcn": "16.42067126414000000000",
  "xmr": "0.01750385351100000000",
  "qcn": "13.59907377987700000000"
}
```

#### Transfers

_Method_: GET

_Path_: /1.0/transfers/:cc

_Exmaple request_: /1.0/transfers/xdn

_Example response_:
```json
[
  {
    "cc": "xdn",
    "amount": 700,
    "fromUserId": "user1@gmail.com",
    "toUserId": "user2@gmail.com",
    "id": "c5d7b9d3-c2ce-4621-825c-58cbb5ea6eff",
    "state": "finished",
    "created": 1449161749429
  },
  {
    "cc": "xdn",
    "amount": 10,
    "fromUserId": "user2@gmail.com",
    "toUserId": "user18@gmail.com",
    "id": "e81cde3a-9b67-4f5e-98ad-08ce7884e02a",
    "state": "finished",
    "created": 1448977022415
  }
]
```

_Exmaple request_: /1.0/transfers/

_Example response_:
```json
[
  {
    "cc": "bcn",
    "amount": 700,
    "fromUserId": "user1@gmail.com",
    "toUserId": "user2@gmail.com",
    "id": "c5d7b9d3-c2ce-4621-825c-58cbb5ea6eff",
    "state": "finished",
    "created": 1449161749429
  },
  {
    "cc": "inf8",
    "amount": 10,
    "fromUserId": "user2@gmail.com",
    "toUserId": "user18@gmail.com",
    "id": "e81cde3a-9b67-4f5e-98ad-08ce7884e02a",
    "state": "finished",
    "created": 1448977022415
  }
]
```

#### Withdrawals

_Method_: GET

_Path_: /1.0/withdrawals/:cc

_Exmaple request_: /1.0/withdrawals/xdn

_Example response_:
```json
[
  {
    "cc": "xdn",
    "address": "address",
    "transactionHash": "acaef20101873165b576ec44f0754c4847e5c16831b79810cff71a2eb7c00a38",
    "amount": 1.9,
    "fee": 0.1,
    "paymentId": "paymentId",
    "transactionIdHash": "5bb3f705-82e2-4b61-8651-7567571c72f3",
    "status": "finished",
    "created": 1451151685.785
  },
  {
    "cc": "xdn",
    "address": "address",
    "transactionHash": "acaef20101873165b576ec44f0754c4847e5c16831b79810cff71a2eb7c00a38",
    "amount": 1.9,
    "fee": 0.1,
    "paymentId": "paymentId",
    "transactionIdHash": "5bb3f705-82e2-4b61-8651-7567571c72f3",
    "status": "finished",
    "created": 1451151685.785
  }
]
```

_Exmaple request_: /1.0/withdrawals

_Example response_:
```json
[
  {
    "cc": "fcn",
    "address": "address",
    "transactionHash": "acaef20101873165b576ec44f0754c4847e5c16831b79810cff71a2eb7c00a38",
    "amount": 1.9,
    "fee": 0.1,
    "paymentId": "paymentId",
    "transactionIdHash": "5bb3f705-82e2-4b61-8651-7567571c72f3",
    "status": "pending",
    "created": 1451151685.785
  },
  {
    "cc": "bcn",
    "address": "address",
    "transactionHash": "acaef20101873165b576ec44f0754c4847e5c16831b79810cff71a2eb7c00a38",
    "amount": 1.9,
    "fee": 0.1,
    "paymentId": "paymentId",
    "transactionIdHash": "5bb3f705-82e2-4b61-8651-7567571c72f3",
    "status": "finished",
    "created": 1451151685.785
  }
]
```

#### Workers

_Method_: GET

_Path_: /1.0/workers

_Example response_:
```json
[
  {
  "bcn": {
    "minersCount": 1,
    "hashrate": 322.484387977974,
    "hashrateRank": 256
  },
  "fcn": {
    "minersCount": 1,
    "hashrate": 322.484387977974,
    "hashrateRank": 155
  }
}
]
```

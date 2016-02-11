# MinerGate API

_Host_: https://api.minergate.com

### Currencies List
| Currency Name | Currency Code (cc) |
| --- | --- |
| Bitcoin | btc |
| Litecoin | ltc |
| Bytecoin | bcn |
| Monero | xmr |
| FantomCoin | fcn |
| QuazarCoin | qcn |
| DigitalNote | xdn |
| MonetaVerde | mcn |
| Dashcoin | dsh |
| Aeon coin | aeon |
| Infinium-8 | inf8 |


### Non-authorized API methods

#### Methods list
- [get profit currency rating](#profit-rating)
- [get top hasrates by currencies](#top-hashrate)
- [get blockhain info](#blockchain-info)
- [login](#login)

#### Profit rating

_Summary_: Returns the list of all currencies sorted by profitability.

_Method_: GET

_Path_: /1.0/pool/profit-rating

_Example response_:
```json
["btc", "qcn", "xmr", "bcn"]
```

#### Top hashrate

_Summary_: Returns the lists of top 10 miners for each currency. 

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

_Summary_: Returns the blockchain data of the specified currency. Returned values are as follows: chain height, last block timestamp, network difficulty, network hashrate, base reward.

_Method_: GET

_Path_: /1.0/:cc/status

_Example request_: /1.0/xmr/status

_Example response_:
```json
{
  "hash": "04ab3e8bb9c7724b27563cb9c5cab9d25f948f4579e57deb9b7a95b4b66e4acc",
  "height": 940410,
  "orphan": false,
  "timestamp": 1454512169,
  "difficulty": 795820297,
  "prevBlockHash": "21af39326483b2f1d4556e0e363887e28aeb7e1753eec2e1e2ba4d984ecccae3",
  "sizeMedian": 210,
  "blockSize": 254,
  "txCumulativeSize": 210,
  "txCount": 1,
  "baseReward": 7.193899826126,
  "penalty": 0,
  "reward": 7.193899826126,
  "feeSumm": 0,
  "alreadyGeneratedCoins": 10903400.563529158,
  "cumulativeTxCount": 1481736,
  "rewardBlocksWindow": 100,
  "fullRewardMaxBlockSize": 20000,
  "instantHashrate": 13263671.616666667
}
```

#### Login

_Summary_: Authorizes the user and gives token for the following methods.

_Method_: POST

_Path_: /1.0/auth/login


_Content-Type_: application/json

_Body_: email, password, totp (2-step authorization token, required if 2-step authorization is enabled)

_Example body_: 
```json
{
  "email": "your_email@gmail.com",
  "password": "your_password",
  "totp": 123456
}
```

_Possible errors_:
```json
{
  "error": "WrongEmailOrPassword",
  "message": "Email and password did not match."
}
``` 
```json
{
  "error": "TotpRequired",
  "message": "Two-factor authorization is enabled for this account. Please provide TOTP code."
}
```

_Example success response_:
```json
{
  "token": "1c2VySWQiOiJibGFja19sdWdhMkBtYW1c2VySWQiOiJibGFja19sdWdhMkBtYW1c2VySWQiOiJibGFja19sdWdhMkBtYW"
}
```

### Authorized API methods

To perform the authorized request, put the token to its header. The token value is generated during login process.

#### Methods list
- [get balance](#balance)
- [get transfers](#transfers)
- [get withdrawals](#withdrawals)
- [get workers](#workers)
- [get mining stats](#mining-stats)
- [get affiliate links](#affiliate-links)
- [get affiliates](#affiliates)
- [get affiliate profit](#affiliate-profit)
- [get invoices](#invoices)
- [get invoice by id](#invoice)
- [get nickname](#nickname)

#### Balance

_Summary_: Returns the user’s balance. Requires authorization. 

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

_Summary_: Returns the list of user’s transfers. Requires authorization. 

_Method_: GET

_Path_: /1.0/transfers/:cc

_Example request_: /1.0/transfers/xdn

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

_Example request_: /1.0/transfers/

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

_Summary_: Returns the list of user’s withdrawals for all the currencies or a specific currency if such parameter is set. Requires authorization.  

_Method_: GET

_Path_: /1.0/withdrawals/:cc

_Example request_: /1.0/withdrawals/xdn

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
    "transactionId": "5bb3f705-82e2-4b61-8651-7567571c72f3",
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
    "transactionId": "5bb3f705-82e2-4b61-8651-7567571c72f3",
    "status": "finished",
    "created": 1451151685.785
  }
]
```

_Example request_: /1.0/withdrawals

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

_Summary_: Returns the number of user’s active workers. Requires authorization.

_Method_: GET

_Path_: /1.0/workers

_Example response_:
```json
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
```

#### Mining stats

_Summary_: Returns the user’s mining statistics. Requires authorization. 

_Method_: GET

_Path_: /1.0/mining/stats

_Example response_:
```json
{
  "bcn": {
    "unconfirmedBalance": 191049661,
    "minersCount": "1",
    "hashrate": "65.405322258114126",
    "hashrateRank": 1061,
    "minerOnline": true,
    "shares": {
      "good": 827813,
      "goodEq": 968780359,
      "bad": 3469,
      "badEq": 4033431,
      "invalid": 0,
      "invalidEq": 0
    },
    "ppsTotalMined": 111023.92139614478,
    "pplnsTotalMined": 22249.54433594,
    "blocksFound": 5,
    "totalMined": 133273.4657320848
  }, ...
  "paymentModels": {
    "bcn": "pps",
    "fcn": "pps",
    "dsh": "pplns",
    "xmr": "pps",
    "qcn": "pps",
    "xdn": "pps",
    "mcn": "pps",
    "aeon": "pps",
    "inf8": "pps",
    "btc": "pps",
    "ltc": "pps"
  },
  "timestamp": 1454496693669
}
```

#### Affiliate links

_Summary_: Returns the list of user’s affiliate links. Requires authorization. 

_Method_: GET

_Path_: /1.0/affiliate/links

_Example response_:
```json
{
  "/a/7d14d06a612312349": "link",
  "/a/ad9e3352adde3f7123256556": "link2",
  "/a/f36f11e816381123b9b12295": "link3",
  "/a/37d05a536010d46a123e44f4": "link4",
  "/a/15e64ffe0aa0aa506dcg452a": "link5"
}
```

#### Affiliates

_Summary_: Returns the list of user’s affiliates. Requires authorization. 

_Method_: GET

_Path_: /1.0/affiliate/childrens

_Example response_:
```json
{
  "test1@gmail.com": {
    "registered": 1426754165398,
    "profits": {
      "bcn": 34.91620052067053,
      "xmr": 0.0014406817930471406,
      "xdn": 0.05284179398738854,
      "mcn": 0.00000356443120348296,
      "qcn": 9.373443247396294,
      "fcn": 0.04380865486606831,
      "aeon": 9.385291553402276,
      "dsh": 1244.935845946683
    },
    "lastProfit": 1454496377768,
    "token": "/a/d976f19wefr234fasdfd598"
  },
  "test2@gmail.com": {
    "registered": 1426229844791,
    "token": "/a/d976f11231d598"
  },
}
```

#### Affiliate profit

_Summary_: Returns the user’s income from affiliates. Requires authorization.

_Method_: GET

_Path_: /1.0/affiliate/profit

_Example response_:
```json
{
  "bcn": 48481.30996792437,
  "xmr": 0.22784646878529005,
  "xdn": 0.8658647284964952,
  "mcn": 23.31826311843995,
  "qcn": 11.443061561369651,
  "fcn": 0.32156100510772107,
  "aeon": 24.456462240551215,
  "dsh": 6193.343139060691,
  "ltc": 0.0001675684355892698,
  "inf8": 3.279558343484024,
  "btc": 0.00000503616312175371
}
```

#### Invoices

_Summary_: Returns the list of user's invoices. Requires authorization.

_Method_: GET

_Path_: /1.0/invoices

_Example response_:
```json
[
  {
    "amount": 100000,
    "cc": "bcn",
    "address": "address",
    "comment": "Some text from invoice creator",
    "expiredDate": 1454273838471,
    "invoiceId": "44872a9e0dbb66fa5b5782cfef36f5b4bcdfba43",
    "created": 1454101038531,
    "status": "finished",
    "email": "test@gmail.com",
    "finished": 1454101196469
  }, ...
]
```

#### Invoice

_Summary_: Returns the specified invoice. Requires authorization.

_Method_: GET

_Path_: /1.0/invoices/:id

_Example request_: /1.0/invoices/44872a9e0dbb66fa5b5782cfef36f5b4bcdfba43

_Example response_:
```json

{
  "amount": 100000,
  "cc": "bcn",
  "address": "address",
  "comment": "Some text from invoice creator",
  "expiredDate": 1454273838471,
  "invoiceId": "44872a9e0dbb66fa5b5782cfef36f5b4bcdfba43",
  "created": 1454101038531,
  "status": "finished",
  "email": "test@gmail.com",
  "finished": 1454101196469
}

```

#### Nickname

_Summary_: Returns the user’s nickname. Requires authorization. 

_Method_: GET

_Path_: /1.0/profile/nickname

_Example response_:
```json
"YourNickname"
```

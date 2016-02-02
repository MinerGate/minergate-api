# MinerGate API



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


### API non-authorized methods

#### Methods list
- [get profit currency rating](#profit-rating)
- [get top hasrates by currencies](#top-hashrate)
- [get blockhain info](#blockchain-info)
- [login](#login)

#### Profit rating

_Method_: GET

_URL_: /1.0/pool/profitRating

_Example response_:
```json
["btc", "qcn", "xmr", "bcn"]
```

#### Top hashrate

_Method_: GET

_URL_: /1.0/pool/top/hashrate

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

_URL_: /1.0/:cc/status

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

_URL_: /1.0/auth/login

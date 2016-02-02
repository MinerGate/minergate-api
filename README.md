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
['btc', 'qcn', 'xmr', 'bcn']
```

#### Top hashrate

_Method_: GET

_URL_: /1.0/pool/top/hashrate

_Example response_:
```json
{
xmr: [
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
bcn : {
  ...
}, ...}
```

#### Blockchain info

_Method_: GET

_URL_: /1.0/:cc/status

#### Login

_Method_: POST

_URL_: /1.0/auth/login

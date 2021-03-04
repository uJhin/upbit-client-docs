
# WebSocket (웹 소켓)
## 개요

### 1. 시세 정보
WebSocket을 이용하여 수신할 수 있는 정보는 다음과 같습니다.

1. 현재가 (스냅샷, 실시간 정보 제공)
2. 체결 (스냅샷, 실시간 정보 제공)
3. 호가 (스냅샷, 실시간 정보 제공)

각각의 정보는 `스냅샷`과 `실시간 데이터`로 나뉘며 요청 방법에 따라 수신할 수 있는 데이터가 달라집니다.

`스냅샷` 정보란 요청 당시의 상태를 의미합니다.

`실시간` 정보란 요청 정보가 스트림 형태로 지속적으로 제공되는 것을 의미합니다.

WebSocket을 이용하여 스냅샷 정보나 실시간 정보를 요청할 수 있으며 둘 중 하나의 정보만을 요청할 수도 있습니다.

자세한 요청 방법은 `2. 요청 포맷` 섹션과 `UpbitWebSocket` 섹션에서 다룹니다.

### 2. 요청 형식
연결이 성공적으로 이루어졌다면 웹소켓 서버에 여러가지 요청을 할 수 있습니다.
요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다.

요청은 크게 `[{ticket field}, {type field}, {format field}]` 로 나누어지며 각각의 필드는 다음 구성요소로 이루어져 있습니다.

**Ticket Field**

일반적으로 용도를 식별하기 위해 `ticket` 이라는 필드값이 필요합니다.

이 값은 시세를 수신하는 대상을 식별하며 되도록 유니크한 값을 사용하도록 권장합니다. (UUID 등)

필드 명 | 내용    | 타입   | 필요 여부
------- | ------ | ------ | ---------
ticket  | 식별값 | String | O


**Type Field**

수신하고 싶은 시세 정보를 나열하는 필드입니다.

`isOnlySnapshot`, `isOnlyRealtime` 필드는 생략 가능하며 모두 생략시 스냅샷과 실시간 데이터 모두를 수신합니다.

하나의 요청에 `{type field}` 는 여러개를 명시할 수 있습니다.

필드명         | 내용                                                                                   | 타입    | 필요 여부
-------------- | ------------------------------------------------------------------------------------- | ------- | ---------
type           | 수신할 시세 타입 (현재가: `ticker`, 체결: `trade`, 호가: `orderbook`)                   | String  | O
codes          | 수신할 시세 종목 정보 (**주의**: codes 필드에 명시되는 종목들은 대문자로 요청해야 합니다.) | List    | O
isOnlySnapshot | 시세 스냅샷만 제공                                                                      | Boolean | X
isOnlyRealtime | 실시간 시세만 제공                                                                      | Boolean | X

<aside class="notice">
    <b>NOTE</b>: v1.1.0 Orderbook Unit 갯수 커스텀 수신기능 추가
    <br/><br/>
    v1.1.0 부터 orderbook 타입의 패킷에 한하여 Orderbook Unit의 갯수를 최대 제공 갯수(15개) 안에서 원하는 만큼 조절하여 호출 가능합니다.
    <br/>
    기존의 <code>codes</code> 항목에 시세 종목과 원하는 Unit 갯수를 넣어주시면 됩니다.
    <br/>
    형식: <code>{code}.{count}</code>
    <br/>
    ex) "KRW-BTC.5", "BTC-XRP.3"
    <br/><br/>
</aside>


**Format Field**

마지막으로 포맷 정보입니다. `Simple`로 지정될 경우 응답의 필드명이 모두 간소화됩니다.

트래픽 부담이 클 때 사용하는 방법입니다.

필드명 | 내용                                                         | 타입   | 필요 여부
------ | ----------------------------------------------------------- | ------ | ---------
format | 포맷 (`SIMPLE`: 간소화된 필드명, `DEFAULT`: 기본값(생략 가능) | String | X (기본: `Default`)


## UpbitWebSocket
고성능 네트워크 및 웹 서버 비동기(async) 프레임워크 기반의 동시성 코드 작성을 위한 업비트 웹 소켓 클래스를 생성합니다.

자세한 사항은 파이썬 표준 라이브러리 [`asyncio`](https://docs.python.org/3/library/asyncio.html) 패키지를 참고해주세요.

> Example Code

```python
from upbit.websocket import UpbitWebSocket

sock = UpbitWebSocket()
print(sock)

async with sock as conn:
    # Do something
    pass
```

> Result Example

```python
UpbitWebSocket(wss://api.upbit.com/websocket/v1)
```

### UpbitWebSocket(uri=WEBSOCKET_URI, ping_interval=None, ping_timeout=None)

Parameter      | Description
-------------- | --------------------
uri            | 웹 소켓에 연결할 URI. (기본값: `wss://api.upbit.com/websocket/v1`)
ping_interval  | ping 간격 제한 (기본값: `None`)
ping_timeout   | ping 시간 초과 제한 (기본값: `None`)


## socket.Connection
**Property**

웹 소켓에 연결하기 위해 생성된 Connection 객체입니다.

위의 예제와 동일한 결과를 가집니다.

> Example Code

```python
from upbit.websocket import UpbitWebSocket

sock = UpbitWebSocket()
connection = sock.Connection

async with connection as conn:
    # Do Something
    pass
```

## socket.connect
**Method**

URI에 연결을 시도하고 Connection 객체를 재생성합니다.

`UpbitWebSocket` 클래스의 `__init__` 메소드 호출 시 자동으로 호출됩니다.

> Example Code

```python
from upbit.websocket import UpbitWebSocket

sock = UpbitWebSocket()
sock.connect(
    ping_interval=20,
    ping_timeout=20
)

async with sock as conn:
    # Do Something
    pass
```

### socket.connect(ping_interval=None, ping_timeout=None)

Parameter      | Description
-------------- | --------------------
ping_interval  | ping 간격 제한 (기본값: `None`)
ping_timeout   | ping 시간 초과 제한 (기본값: `None`)


## conn.send
웹 소켓에 데이터를 수신합니다.

> Example Code

```python
from upbit.websocket import UpbitWebSocket

sock = UpbitWebSocket()

async with sock as conn:
    await conn.send('PING')
```

### conn.send(message)

Parameter      | Description
-------------- | --------------------
message *      | 서버에 수신할 데이터


## conn.recv
서버로부터 전달받은 바이트 스트림(bytes stream) 데이터를 받습니다.

예외를 발생시키는 경우는 아래와 같습니다.

- **ConnectionClosed**: `Connection` 객체가 `Close` 상태가 되었을 경우
- **RuntimeError**: 두 가지 코루틴이 동시에 `recv` 를 호출하는 경우

> Example Code

```python
import re
import json
from upbit.websocket import UpbitWebSocket

sock = UpbitWebSocket()

async with sock as conn:
    await conn.send('PING')
    data = await conn.recv()

    pattern = re.compile('{"\S+":"\S+"}')
    search = pattern.search(data.decode('utf8'))
    result = json.loads(search.group())
    print(result)
```

> Result

```json
{"status": "UP"}
```

### conn.recv()

No Parameters


## UpbitWebSocket.generate_type_field (Type Field Generate)
**staticmethod**

웹 소켓 수신에 필요한 payload의 type field 데이터를 generate 합니다.

요청 형식에 대한 사항은 위의 `2. 요청 형식` 섹션을 참고해주세요.

> Example Code

```python
from upbit.websocket import UpbitWebSocket

currencies = ['KRW-BTC', 'KRW-ETH']

type_field = UpbitWebSocket.generate_type_field(
    type="trade",
    codes=currencies
)
print(type_field)
```

> Result

```json
{
    "type": "trade",
    "codes": ["KRW-BTC", "KRW-ETH"]
}
```

### UpbitWebSocket.generate_type_field(type, codes, isOnlySnapshot=None, isOnlyRealtime=None)
**staticmethod**

Parameter      | Description
-------------- | --------------------
type *         | 수신할 시세 타입 (현재가: `ticker`, 체결: `trade`, 호가: `orderbook`)
codes *        | 수신할 시세 종목 정보 (ex. `['KRW-BTC', 'KRW-ETH']`)
isOnlySnapshot | 시세 스냅샷만 제공 여부 (`True`, `False`)
isOnlyRealtime | 실시간 시세만 제공 여부 (`True`, `False`)


## UpbitWebSocket.generate_orderbook_codes (Orderbook Codes Generate)
**staticmethod**

`type` 파라미터가 `orderbook`일 경우에 필요한 `codes` 파라미터를 요청 형식에 맞춰 generate 합니다.

> Example Code

```python
from upbit.websocket import UpbitWebSocket

currencies = ['KRW-BTC', 'KRW-ETH']
counts = [5, 5]

codes = UpbitWebSocket.generate_orderbook_codes(
    currencies=currencies,
    counts=counts
)
print(codes)
```

> Result

```json
["KRW-BTC.5", "KRW-ETH.5"]
```

### UpbitWebSocket.generate_orderbook_codes(currencies, counts=None)

Parameter      | Description
-------------- | --------------------
currencies *   | 수신할 시세 종목들
counts         | 수신할 각 시세 종목에 대한 개수


## UpbitWebSocket.generate_payload (Payload Generate)
**staticmethod**

웹 소켓 수신에 필요한 payload 데이터를 json 포맷 형식의 문자열로 generate 합니다.

> Example Code

```python
from upbit.websocket import UpbitWebSocket


codes = ['KRW-BTC', 'KRW-ETH', 'KRW-BCH', 'KRW-XRP']
counts = [1 for _ in range(len(codes))]

ord_codes = UpbitWebSocket.generate_orderbook_codes(
    currencies=codes,
    counts=counts
)

trade = UpbitWebSocket.generate_type_field(
    type='trade',
    codes=codes
)
orderbook = UpbitWebSocket.generate_type_field(
    type='orderbook',
    codes=ord_codes
)

type_fields = [trade, orderbook]

payload = UpbitWebSocket.generate_payload(
    type_fields=type_fields,
    format='SIMPLE'
)

print(payload)
```

> Result

```json
[
    {
        "ticket": "43552c23-6596-478d-8f71-b8289779a996"
    },
    {
        "type": "trade",
        "codes": ["KRW-BTC", "KRW-ETH", "KRW-BCH", "KRW-XRP"]
    },
    {
        "type": "orderbook",
        "codes": ["KRW-BTC.1", "KRW-ETH.1", "KRW-BCH.1", "KRW-XRP.1"]
    },
    {
        "format": "SIMPLE"
    }
]
```


### UpbitWebSocket.generate_payload(type_fields, ticket=None, format='DEFAULT')

Parameter      | Description
-------------- | --------------------
type_fields *  | Type Fields
ticket         | 식별값 (기본값은 `uuid4` 형식으로 생성)
format         | 포맷, `SIMPLE`: 간소화된 필드명, `DEFAULT`: 기본 포맷 (생략 가능)


## 웹 소켓으로 시세 정보 요청하기
웹 소켓을 통해 시세 정보를 요청합니다.

> Example Code

```python
import json
import asyncio

from upbit.websocket import UpbitWebSocket


# Definition async function
async def ticker(sock, payload):
    async with sock as conn:
        while True:
            await conn.send(payload)
            recv = await conn.recv()
            data = recv.decode('utf8')
            result = json.loads(data)
            print(result)


sock = UpbitWebSocket()

currencies = ['KRW-BTC', 'KRW-ETH']
type_field = sock.generate_type_field(
    type='ticker',
    codes=currencies
)
payload = sock.generate_payload(
    type_fields=[type_field]
)

event_loop = asyncio.get_event_loop()
event_loop.run_until_complete( ticker(sock, payload) )
```

> Result

```json
{
    "type": "ticker",
    "code": "KRW-BTC",
    "opening_price": 36408000.0,
    "high_price": 38161000.0,
    "low_price": 35907000.0,
    "trade_price": 36784000.0,
    "prev_closing_price": 36408000.0,
    "acc_trade_price": 466420626861.1874,
    "change": "RISE",
    "change_price": 376000.0,
    "signed_change_price": 376000.0,
    "change_rate": 0.0103274006,
    "signed_change_rate": 0.0103274006,
    "ask_bid": "BID",
    "trade_volume": 0.004996,
    "acc_trade_volume": 12633.27063535,
    "trade_date": "20210201",
    "trade_time": "192943",
    "trade_timestamp": 1612207783000,
    "acc_ask_volume": 6355.28646728,
    "acc_bid_volume": 6277.98416807,
    "highest_52_week_price": 48550000.0,
    "highest_52_week_date": "2021-01-08",
    "lowest_52_week_price": 5489000.0,
    "lowest_52_week_date": "2020-03-13",
    "trade_status": null,
    "market_state": "ACTIVE",
    "market_state_for_ios": null,
    "is_trading_suspended": false,
    "delisting_date": null,
    "market_warning": "NONE",
    "timestamp": 1612207783496,
    "acc_trade_price_24h": 503390500539.5724,
    "acc_trade_volume_24h": 13650.71883738,
    "stream_type": "SNAPSHOT"
},
{
    "type": "ticker",
    "code": "KRW-ETH",
    "opening_price": 1444000.0,
    "high_price": 1509500.0,
    "low_price": 1413000.0,
    "trade_price": 1444000.0,
    "prev_closing_price": 1444000.0,
    "acc_trade_price": 331846956832.1946,
    "change": "EVEN",
    "change_price": 0.0,
    "signed_change_price": 0.0,
    "change_rate": 0,
    "signed_change_rate": 0,
    "ask_bid": "ASK",
    "trade_volume": 1.0,
    "acc_trade_volume": 229202.315562,
    "trade_date": "20210201",
    "trade_time": "192925",
    "trade_timestamp": 1612207765000,
    "acc_ask_volume": 126760.03539062,
    "acc_bid_volume": 102442.28017138,
    "highest_52_week_price": 1626000.0,
    "highest_52_week_date": "2021-01-25",
    "lowest_52_week_price": 124350.0,
    "lowest_52_week_date": "2020-03-13",
    "trade_status": null,
    "market_state": "ACTIVE",
    "market_state_for_ios": null,
    "is_trading_suspended": false,
    "delisting_date": null,
    "market_warning": "NONE",
    "timestamp": 1612207765752,
    "acc_trade_price_24h": 354570292652.8257,
    "acc_trade_volume_24h": 244893.27187195,
    "stream_type": "SNAPSHOT"
},
...
```

### Request Parameters

Parameter      | Description
-------------- | --------------------
payload        | 포맷에 맞춰진 요청 데이터


### Response


**현재가(Ticker) 응답**

필드명                      | 축약형 (format: SIMPLE) | 내용                | 타입  | 값
-------------------------- | ---------------------- | ------------------- | ----- | -----
type                       | ty           | 타입                           | String | `ticker` : 현재가
code                       | cd           | 마켓 코드 (ex. KRW-BTC)        | String | -
opening_price              | op           | 시가                           | Double | -
high_price                 | hp           | 고가                           | Double | -
low_price                  | lp           | 저가                           | Double | -
trade_price                | tp           | 현재가                         | Double | -
prev_closing_price         | pcp          | 전일 종가                      | Double | 
change                     | c            | 전일 대비                      | String | `RISE`: 상승, `EVEN`: 보합, `FALL`: 하락
change_price               | cp           | 부호 없는 전일 대비 값          | Double | -
signed_change_price        | scp          | 전일 대비 값                   | Double | -
change_rate                | cr           | 부호 없는 전일 대비 등락율      | Double | -
signed_change_rate         | scr          | 전일 대비 등락율               | Double | -
trade_volume               | tv           | 가장 최근 거래량               | Double | -
acc_trade_volume           | atv          | 누적 거래량(UTC 0시 기준)      | Double | -
acc_trade_volume_24h       | atv24h       | 24시간 누적 거래량              | Double | -
acc_trade_price            | atp          | 누적 거래대금(UTC 0시 기준)     | Double | -
acc_trade_price_24h        | atp24h       | 24시간 누적 거래대금            | Double | -
trade_date                 | tdt          | 최근 거래 일자(UTC)            | String | `yyyyMMdd`
trade_time                 | ttm          | 최근 거래 시각(UTC)            | String | `HHmmss`
trade_timestamp            | ttms         | 체결 타임스탬프 (milliseconds) | Long | -
ask_bid                    | ab           | 매수/매도 구분                 | String  | `ASK`: 매도, `BID`: 매수
acc_ask_volume             | aav          | 누적 매도량                    | Double | -
acc_bid_volume             | abv          | 누적 매수량                    | Double | -
highest_52_week_price      | h52wp        | 52주 최고가                    | Double | -
highest_52_week_date       | h52wdt       | 52주 최고가 달성일              | String | `yyyy-MM-dd`
lowest_52_week_price       | l52wp        | 52주 최저가                    | Double | -
lowest_52_week_date        | l52wdt       | 52주 최저가 달성일              | String |`yyyy-MM-dd`
trade_status               | ts           | 거래상태 *deprecated           | String | -
market_state               | ms           | 거래상태                       | String | `PREVIEW`: 입금지원, `ACTIVE`: 거래지원가능, `DELISTED` : 거래지원종료
market_state_for_ios       | msfi         | 거래 상태 *deprecated          | String | - 
is_trading_suspended       | its          | 거래 정지 여부                  | Boolean | - 
delisting_date             | dd           | 상장폐지일                      | Date  | -
market_warning             | mw           | 유의 종목 여부                  | String | `NONE`: 해당없음, `CAUTION`: 투자유의
timestamp                  | tms          | 타임스탬프 (milliseconds)       | Long | -
stream_type                | st           | 스트림 타입                     | String | `SNAPSHOT`: 스냅샷, `REALTIME`: 실시간


**체결(Trade) 응답**

필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값
----- | ------------------------ | --- | --- | ----
type | ty | 타입 | String | `trade`: 체결
code | cd | 마켓 코드 (ex. KRW-BTC) | String | - 
trade_price | tp | 체결 가격 | Double | -
trade_volume | tv | 체결량 | Double | -
ask_bid | ab | 매수/매도 구분 | String | `ASK`: 매도, `BID`: 매수
prev_closing_price | pcp | 전일 종가 | Double | -
change | c | 전일 대비 | String | `RISE` : 상승, `EVEN` : 보합, `FALL` : 하락
change_price | cp | 부호 없는 전일 대비 값 | Double | -
trade_date | td | 체결 일자(UTC 기준) | String | `yyyy-MM-dd`
trade_time | ttm | 체결 시각(UTC 기준) | String | `HH:mm:ss`
trade_timestamp | ttms | 체결 타임스탬프 (millisecond) | Long | -
timestamp | tms | 타임스탬프 (millisecond) | Long | -
sequential_id | sid | 체결 번호 (Unique) | Long | -
stream_type | st | 스트림 타입 | String | `SNAPSHOT`: 스냅샷, `REALTIME`: 실시간

<aside class="notice">
    <code>sequential_id</code> 필드는 체결의 유일성 판단을 위한 근거로 쓰일 수 있습니다.
    <br/>
    하지만 체결의 순서를 보장하지는 못합니다.
</aside>


**호가(Orderbook) 응답**

필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값
------ | ----------------------- | --- | --- | -------
type | ty | 타입 | String | `orderbook`: 호가
code | cd | 마켓 코드 (ex. KRW-BTC) | String | - 
total_ask_size | tas | 호가 매도 총 잔량 | Double | - 
total_bid_size | tbs | 호가 매수 총 잔량 | Double | -
orderbook_units | obu | 호가 | List of Objects | -
ask_price | ap | 매도 호가 | Double | -
bid_price | bp | 매수 호가 | Double | -
ask_size | as | 매도 잔량 | Double | -
bid_size | bs | 매수 잔량 | Double | -
timestamp | tms | 타임스탬프 (millisecond) | Long | -
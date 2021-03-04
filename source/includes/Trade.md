# Trade (거래; 시세 체결)

## Trade_ticks (최근 체결 내역)
최근 체결 내역을 조회합니다.

> Request Example

```python
from upbit.client import Upbit

client = Upbit()
resp = client.Trade.Trade_ticks(
    market='KRW-BTC'
)
print(resp['result'])
```

> Response Example

```json
[
	{
		"market": "KRW-BTC",
		"trade_date_utc": "2021-01-08",
		"trade_time_utc": "17:44:15",
		"timestamp": 1610127855000,
		"trade_price": 47560000.0,
		"trade_volume": 0.47572963,
		"prev_closing_price": 44698000.0,
		"change_price": 2862000.0,
		"ask_bid": "ASK",
		"sequential_id": 1610127855000000
    },
    ...
]
```

### Method
**GET** `/v1/trades/ticks`

### Operation Code
`Trade.Trade_ticks`

### 요청 (Request)

Parameter | Description
--------  | -----------
market *  | 마켓 코드 (ex. KRW-BTC, BTC-BCC)
to        | 마지막 캔들 시각 (exclusive). 포맷 : `yyyy-MM-dd'T'HH:mm:ssXXX` or `yyyy-MM-dd HH:mm:ss`. 비워서 요청시 가장 최근 캔들
count     | 캔들 개수 (최대 200개까지 요청 가능)
cursor    | 페이지네이션 커서 (`sequentialId`)
daysAgo   | 최근 체결 날짜 기준 7일 이내의 이전 데이터 조회 가능. 비워서 요청 시 가장 최근 체결 날짜 반환. (범위: 1 ~ 7)

### 응답 (Response)

Parameter          | Description
------------------ | -----------
trade_date_utc     | 체결 일자(UTC 기준)
trade_time_utc     | 체결 시각(UTC 기준)
timestamp          | 체결 타임스탬프
trade_price        | 체결 가격
trade_volume       | 체결량
prev_closing_price | 전일 종가
change_price       | 변화량
ask_bid            | 매도/매수
sequential_id      | 체결 번호 (Unique)

<aside class="notice">
    <code>sequential_id</code> 필드는 체결의 유일성 판단을 위한 근거로 쓰일 수 있습니다.
    <br/>
    하지만 체결의 순서를 보장하지는 못합니다.
</aside>

## Trade_ticker (시세 Ticker 조회 - 현재가 정보)
요청 당시 종목의 스냅샷을 반환합니다.

> Request Example

```python
from upbit.client import Upbit

client = Upbit()
resp = client.Trade.Trade_ticker(
    markets='KRW-BTC, KRW-ETH'
)
print(resp['result'])
```

> Response Example

```json
[
	{
		"market": "KRW-BTC",
		"trade_date": "20210108",
		"trade_time": "174621",
		"trade_date_kst": "20210109",
		"trade_time_kst": "024621",
		"trade_timestamp": 1610127981000,
		"opening_price": 44698000.0,
		"high_price": 48550000.0,
		"low_price": 42271000.0,
		"trade_price": 47577000.0,
		"prev_closing_price": 44698000.0,
		"change": "RISE",
		"change_price": 2879000.0,
		"change_rate": 0.0644100407,
		"signed_change_price": 2879000.0,
		"signed_change_rate": 0.0644100407,
		"trade_volume": 0.00033988,
		"acc_trade_price": 861919074055.3187,
		"acc_trade_price_24h": 1082457070848.9071,
		"acc_trade_volume": 18804.39719428,
		"acc_trade_volume_24h": 23822.32449006,
		"highest_52_week_price": 48550000.0,
		"highest_52_week_date": "2021-01-08",
		"lowest_52_week_price": 5489000.0,
		"lowest_52_week_date": "2020-03-13",
		"timestamp": 1610127981564
	},
	{
		"market": "KRW-ETH",
		"trade_date": "20210108",
		"trade_time": "174619",
		"trade_date_kst": "20210109",
		"trade_time_kst": "024619",
		"trade_timestamp": 1610127979000,
		"opening_price": 1388000.0,
		"high_price": 1485000.0,
		"low_price": 1233500.0,
		"trade_price": 1410000.0,
		"prev_closing_price": 1388000.0,
		"change": "RISE",
		"change_price": 22000.0,
		"change_rate": 0.0158501441,
		"signed_change_price": 22000.0,
		"signed_change_rate": 0.0158501441,
		"trade_volume": 0.22966312,
		"acc_trade_price": 581867851790.185,
		"acc_trade_price_24h": 717996348913.0636,
		"acc_trade_volume": 422799.52433396,
		"acc_trade_volume_24h": 521320.18764923,
		"highest_52_week_price": 1485000.0,
		"highest_52_week_date": "2021-01-08",
		"lowest_52_week_price": 124350.0,
		"lowest_52_week_date": "2020-03-13",
		"timestamp": 1610127979352
	}
]
```

### Method
**GET** `/v1/ticker`

### Operation Code
`Trade.Trade_ticker`

### 요청 (Request)

Parameter  | Description
---------- | -----------
markets *  | 반점으로 구분되는 마켓 코드 (ex. KRW-BTC, BTC-BCC)

### 응답 (Response)

Parameter             | Description
--------------------- | -----------
market                | 종목 구분 코드
trade_date            | 최근 거래 일자(UTC)
trade_time            | 최근 거래 시각(UTC)
trade_date_kst        | 최근 거래 일자(KST)
trade_time_kst        | 최근 거래 시각(KST)
opening_price         | 시가
high_price            | 고가
low_price             | 저가
trade_price           | 종가
prev_closing_price    | 전일 종가
change                | `EVEN`: 보합, `RISE`: 상승, `FALL`: 하락
change_price          | 변화액의 절대값
change_rate           | 변화율의 절대값
signed_change_price   | 부호가 있는 변화액
signed_change_rate    | 부호가 있는 변화율
trade_volume          | 가장 최근 거래량
acc_trade_price       | 누적 거래대금 (UTC 0시 기준)
acc_trade_price_24h   | 24시간 누적 거래대금
acc_trade_volume      | 누적 거래량 (UTC 0시 기준)
acc_trade_volume_24h  | 24시간 누적 거래량
highest_52_week_price | 52주 신고가
highest_52_week_date  | 52주 신고가 달성일
lowest_52_week_price  | 52주 신저가
lowest_52_week_date   | 52주 신저가 달성일
timestamp             | 타임스탬프


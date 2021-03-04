# Candle (시세 캔들; 봉)

## Candle_minutes (분; Minute 캔들)
분(Miniute) 단위로 시세 캔들을 조회합니다.

> Request Example

```python
from upbit.client import Upbit

client = Upbit()
resp = client.Candle.Candle_minutes(
    unit=1,
    market='KRW-BTC'
)
print(resp['result'])
```

> Response Example

```json
[
	{
		"market": "KRW-BTC",
		"candle_date_time_utc": "2021-01-08T17:05:00",
		"candle_date_time_kst": "2021-01-09T02:05:00",
		"opening_price": 47550000.0,
		"high_price": 47563000.0,
		"low_price": 47550000.0,
		"trade_price": 47551000.0,
		"timestamp": 1610125540014,
		"candle_acc_trade_price": 44005459.60087,
		"candle_acc_trade_volume": 0.92535793,
		"unit": 1
    },
    ...
]
```

### Method
**GET** `/v1/candles/minutes/{unit}`

### Operation Code
`Candle.Candle_minutes`


### 요청 (Request)

Parameter  | Description
--------   | -----------
unit *     | 분 단위 (가능한 값: 1, 3, 5, 15, 10, 30, 60, 240) 
market *   | 마켓 코드 (ex. KRW-BTC, BTC-BCC)
to         | 마지막 캔들 시각 (exclusive). 포맷 : `yyyy-MM-dd'T'HH:mm:ssXXX` or `yyyy-MM-dd HH:mm:ss`. 비워서 요청시 가장 최근 캔들
count      | 캔들 개수 (최대 200개까지 요청 가능)

### 응답 (Response)

Parameter               | Description
----------------------- | -----------
market                  | 마켓명
candle_date_time_utc    | 캔들 기준 시각(UTC 기준)
candle_date_time_kst    | 캔들 기준 시각(KST 기준)
opening_price           | 시가
high_price              | 고가
low_price               | 저가
trade_price             | 종가
timestamp               | 해당 캔들에서 마지막 틱이 저장된 시각
candle_acc_trade_price  | 누적 거래 금액
candle_acc_trade_volume | 누적 거래량
unit                    | 분 단위 (유닛)

## Candle_days (일; Day 캔들)
일(Day) 단위로 시세 캔들을 조회합니다.

> Request Example

```python
from upbit.client import Upbit

client = Upbit()
resp = client.Candle.Candle_days(
    market='KRW-BTC'
)
print(resp['result'])
```

> Response Example

```json
[
	{
		"market": "KRW-BTC",
		"candle_date_time_utc": "2021-01-08T00:00:00",
		"candle_date_time_kst": "2021-01-08T09:00:00",
		"opening_price": 44698000.0,
		"high_price": 48550000.0,
		"low_price": 42271000.0,
		"trade_price": 47544000.0,
		"timestamp": 1610126678593,
		"candle_acc_trade_price": 868607517589.245,
		"candle_acc_trade_volume": 18953.44414088,
		"prev_closing_price": 44698000.0,
		"change_price": 2846000.0,
		"change_rate": 0.0636717527
    },
    ...
]
```

### Method
**GET** `/v1/candles/days`

### Operation Code
`Candle.Candle_days`


### 요청 (Request)

Parameter                | Description
------------------------ | -----------
market *                 | 마켓 코드 (ex. KRW-BTC, BTC-BCC)
to                       | 마지막 캔들 시각 (exclusive). 포맷 : `yyyy-MM-dd'T'HH:mm:ssXXX` or `yyyy-MM-dd HH:mm:ss`. 비워서 요청시 가장 최근 캔들
convertingPriceUnit      | 종가 환산 화폐 단위 (생략 가능, KRW로 명시할 시 원화 환산 가격을 반환.)

### 응답 (Response)

Parameter               | Description
----------------------- | -----------
market                  | 마켓명
candle_date_time_utc    | 캔들 기준 시각(UTC 기준)
candle_date_time_kst    | 캔들 기준 시각(KST 기준)
opening_price           | 시가
high_price              | 고가
low_price               | 저가
trade_price             | 종가
timestamp               | 해당 캔들에서 마지막 틱이 저장된 시각
candle_acc_trade_price  | 누적 거래 금액
candle_acc_trade_volume | 누적 거래량
prev_closing_price      | 전일 종가(UTC 0시 기준)
change_price            | 전일 종가 대비 변화 금액
change_rate             | 전일 종가 대비 변화량
converted_trade_price   | 종가 환산 화폐 단위로 환산된 가격(요청에 `convertingPriceUnit` 파라미터 없을 시 해당 필드 포함되지 않음.)

## Candle_weeks (주; Week 캔들)
주(Week) 단위로 시세 캔들을 조회합니다.

> Request Example

```python
from upbit.client import Upbit

client = Upbit()
resp = client.Candle.Candle_weeks(
    market='KRW-BTC'
)
print(resp['result'])
```

> Response Example

```json
[
	{
		"market": "KRW-BTC",
		"candle_date_time_utc": "2021-01-04T00:00:00",
		"candle_date_time_kst": "2021-01-04T09:00:00",
		"opening_price": 37537000.0,
		"high_price": 48550000.0,
		"low_price": 33000000.0,
		"trade_price": 47617000.0,
		"timestamp": 1610126559879,
		"candle_acc_trade_price": 3531977900551.1753,
		"candle_acc_trade_volume": 88370.43948385,
		"first_day_of_period": "2021-01-04"
    },
    ...
]
```

### Method
**GET** `/v1/candles/weeks`

### Operation Code
`Candle.Candle_weeks`


### 요청 (Request)

Parameter  | Description
--------   | -----------
market *   | 마켓 코드 (ex. KRW-BTC, BTC-BCC)
to         | 마지막 캔들 시각 (exclusive). 포맷 : `yyyy-MM-dd'T'HH:mm:ssXXX` or `yyyy-MM-dd HH:mm:ss`. 비워서 요청시 가장 최근 캔들
count      | 캔들 개수 (최대 200개까지 요청 가능)

### 응답 (Response)

Parameter               | Description
----------------------- | -----------
market                  | 마켓명
candle_date_time_utc    | 캔들 기준 시각(UTC 기준)
candle_date_time_kst    | 캔들 기준 시각(KST 기준)
opening_price           | 시가
high_price              | 고가
low_price               | 저가
trade_price             | 종가
timestamp               | 해당 캔들에서 마지막 틱이 저장된 시각
candle_acc_trade_price  | 누적 거래 금액
candle_acc_trade_volume | 누적 거래량
first_day_of_period     | 캔들 기간의 가장 첫 날

## Candle_month (월; Month 캔들)
월(Month) 단위로 시세 캔들을 조회합니다.

> Request Example

```python
from upbit.client import Upbit

client = Upbit()
resp = client.Candle.Candle_month(
    market='KRW-BTC'
)
print(resp['result'])
```

> Response Example

```json
[
	{
		"market": "KRW-BTC",
		"candle_date_time_utc": "2021-01-01T00:00:00",
		"candle_date_time_kst": "2021-01-01T09:00:00",
		"opening_price": 32037000.0,
		"high_price": 48550000.0,
		"low_price": 31800000.0,
		"trade_price": 47609000.0,
		"timestamp": 1610126792251,
		"candle_acc_trade_price": 5279753367606.828,
		"candle_acc_trade_volume": 136975.61257404,
		"first_day_of_period": "2021-01-01"
    },
    ...
]
```

### Method
**GET** `/v1/candles/months`

### Operation Code
`Candle.Candle_month`

### 요청 (Request)

Parameter  | Description
--------   | -----------
market *   | 마켓 코드 (ex. KRW-BTC, BTC-BCC)
to         | 마지막 캔들 시각 (exclusive). 포맷 : `yyyy-MM-dd'T'HH:mm:ssXXX` or `yyyy-MM-dd HH:mm:ss`. 비워서 요청시 가장 최근 캔들
count      | 캔들 개수 (최대 200개까지 요청 가능)

### 응답 (Response)

Parameter               | Description
----------------------- | -----------
market                  | 마켓명
candle_date_time_utc    | 캔들 기준 시각(UTC 기준)
candle_date_time_kst    | 캔들 기준 시각(KST 기준)
opening_price           | 시가
high_price              | 고가
low_price               | 저가
trade_price             | 종가
timestamp               | 해당 캔들에서 마지막 틱이 저장된 시각
candle_acc_trade_price  | 누적 거래 금액
candle_acc_trade_volume | 누적 거래량
first_day_of_period     | 캔들 기간의 가장 첫 날
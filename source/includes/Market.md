# Market (마켓)

## Market_info_all (마켓 코드 조회)
업비트에서 거래 가능한 마켓 목록을 조회합니다.

> Request Example

```python
from upbit.client import Upbit

client = Upbit()
resp = client.Market.Market_info_all()
print(resp['result'])
```

> Response Example

```json
[
	{
		"market": "KRW-BTC",
		"korean_name": "비트코인",
		"english_name": "Bitcoin"
	},
	{
		"market": "KRW-ETH",
		"korean_name": "이더리움",
		"english_name": "Ethereum"
	},
	{
		"market": "BTC-ETH",
		"korean_name": "이더리움",
		"english_name": "Ethereum"
	},
	{
		"market": "BTC-LTC",
		"korean_name": "라이트코인",
		"english_name": "Litecoin"
	},
	{
		"market": "BTC-XRP",
		"korean_name": "리플",
		"english_name": "Ripple"
    },
    ...
]
```

### Method
**GET** `/v1/market/all`

### Operation Code
`Market.Market_info_all`

### 요청 (Request)

Parameter      | Description
-------------- | -----------
isDetails      | 유의종목 필드과 같은 상세 정보 노출 여부 (선택 파라미터, 기본 값: false)

### 응답 (Response)

Parameter      | Description
-------------- | -----------
market         | 업비트에서 제공중인 시장 정보
korean_name    | 거래 대상 암호화폐 한글명
english_name   | 거래 대상 암호화폐 영문명
market_warning | 유의 종목 여부; (`NONE`: 해당 사항 없음, `CAUTION`: 투자 유의)
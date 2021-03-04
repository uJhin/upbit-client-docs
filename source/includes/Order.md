# Order (주문)

## Order_orderbook (오더북; Orderbook)
현재 시세 호가 정보를 조회합니다.

> Request Example

```python
from upbit.client import Upbit

client = Upbit()
resp = client.Order.Order_orderbook(
    markets=['KRW-BTC', 'KRW-ETH']
)
print(resp['result'])
```

> Response Example

```json
[
	{
		"market": "KRW-BTC",
		"timestamp": 1610070624000,
		"total_ask_size": 7.71050069,
		"total_bid_size": 3.33182914,
		"orderbook_units": [
			{
				"ask_price": 43973000.0,
				"bid_price": 43952000.0,
				"ask_size": 0.00166408,
				"bid_size": 0.03190123
			},
			{
				"ask_price": 43974000.0,
				"bid_price": 43951000.0,
				"ask_size": 1.22621878,
				"bid_size": 0.00451153
			},
			{
				"ask_price": 43984000.0,
				"bid_price": 43933000.0,
				"ask_size": 0.05844488,
				"bid_size": 0.5
			},
			{
				"ask_price": 43985000.0,
				"bid_price": 43920000.0,
				"ask_size": 1.24634891,
				"bid_size": 1.04638941
			},
			...
		]
	},
	{
		"market": "KRW-ETH",
		"timestamp": 1610070624062,
		"total_ask_size": 292.1165831,
		"total_bid_size": 368.94615831,
		"orderbook_units": [
			{
				"ask_price": 1347000.0,
				"bid_price": 1346000.0,
				"ask_size": 13.27655932,
				"bid_size": 24.64993035
			},
			{
				"ask_price": 1347500.0,
				"bid_price": 1345500.0,
				"ask_size": 16.63316797,
				"bid_size": 0.10945805
			},
			{
				"ask_price": 1348000.0,
				"bid_price": 1345000.0,
				"ask_size": 12.27655416,
				"bid_size": 10.15483109
			},
			{
				"ask_price": 1348500.0,
				"bid_price": 1344500.0,
				"ask_size": 27.44579387,
				"bid_size": 21.77733151
			},
			...
		]
	}
]
```

### Method
**GET** `/v1/orderbook`

### Operation Code
`Order.Order_orderbook`

### 요청 (Request)

Parameters | Description
---------- | ------------
markets *  | 마켓 코드 목록 (ex. KRW-BTC, KRW-ETH)

### 응답 (Response)

Parameters                      | Description
------------------------------- | ------------
market                          | 마켓 코드
timestamp                       | 호가 생성 시각
total_ask_size                  | 호가 매도 총 잔량
total_bid_size                  | 호가 매수 총량
orderbook_units                 | 호가
orderbook_units.ask_price       | 매도호가
orderbook_units.bid_price       | 매수호가
orderbook_units.ask_size        | 매도 잔량
orderbook_units.bid_size        | 매수 잔량

## Order_chance (주문 가능 정보)
마켓별 주문 가능 정보를 확인합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Order.Order_chance(
    market='KRW-BTC'
)
print(resp['result'])
```

> Response Example

```json
{
	"bid_fee": "0.0005",
	"ask_fee": "0.0005",
	"maker_bid_fee": "0.0005",
	"maker_ask_fee": "0.0005",
	"market": {
		"id": "KRW-BTC",
		"name": "BTC/KRW",
		"order_types": [
			"limit"
		],
		"order_sides": [
			"ask",
			"bid"
		],
		"bid": {
			"currency": "KRW",
			"price_unit": null,
			"min_total": 5000
		},
		"ask": {
			"currency": "BTC",
			"price_unit": null,
			"min_total": 5000
		},
		"max_total": "1000000000.0",
		"state": "active"
	},
	"bid_account": {
		"currency": "KRW",
		"balance": "0.34202414",
		"locked": "4999.99999922",
		"avg_buy_price": "0",
		"avg_buy_price_modified": true,
		"unit_currency": "KRW"
	},
	"ask_account": {
		"currency": "BTC",
		"balance": "0.00048",
		"locked": "0.0",
		"avg_buy_price": "20870000",
		"avg_buy_price_modified": false,
		"unit_currency": "KRW"
	}
}
```

### Method
**GET** `/v1/orders/chance`

### Operation Code
`Order.Order_chance`

### 요청 (Request)

Parameters   | Description
------------ | ------------
market *     | 마켓 ID

### 응답 (Response)

Parameters                         | Description
---------------------------------- | --------------------------------
bid_fee                            | 매수 수수료 비율
ask_fee                            | 매도 수수료 비율
maker_bid_fee                      | 매수 시 메이커 수수료 비율
maker_ask_fee                      | 매도 시 메이커 수수료 비율
market                             | 마켓에 대한 정보
market.id                          | 마켓 ID
market.name                        | 마켓 이름
market.order_types                 | 지원 주문 방식
market.order_sides	               | 지원 주문 종류
market.bid	                       | 매수 시 제약사항
market.bid.currency	               | 화폐를 의미하는 영문 대문자 코드
market.bid.price_unit              | 주문금액 단위
market.bid.min_total               | 최소 매도/매수 금액
market.ask                         | 매도 시 제약사항
market.ask.currency                | 화폐를 의미하는 영문 대문자 코드
market.ask.price_unit              | 주문금액 단위
market.ask.min_total               | 최소 매도/매수 금액
market.max_total                   | 최대 매도/매수 금액
market.max_total                   | 최대 매도/매수 금액
market.state                       | 마켓 운영 상태
bid_account                        | 매수 시 사용하는 화폐의 계좌 상태
bid_account.currency               | 화폐를 의미하는 영문 대문자 코드
bid_account.balance                | 주문가능 금액/수량
bid_account.locked                 | 주문 중 묶여있는 금액/수량
bid_account.avg_buy_price          | 매수평균가
bid_account.avg_buy_price_modified | 매수평균가 수정 여부
bid_account.unit_currency          | 평단가 기준 화폐
ask_account                        | 매도 시 사용하는 화폐의 계좌 상태
ask_account.currency               | 화폐를 의미하는 영문 대문자 코드
ask_account.balance                | 주문가능 금액/수량
ask_account.locked                 | 주문 중 묶여있는 금액/수량
ask_account.avg_buy_price          | 매수평균가
ask_account.avg_buy_price_modified | 매수평균가 수정 여부
ask_account.unit_currency          | 평단가 기준 화폐

## Order_info (개별 주문 조회)
주문 UUID 를 통해 개별 주문건을 조회합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Order.Order_info(
    uuid='9ca023a5-851b-4fec-9f0a-48cd83c2eaae'
)
print(resp['result'])
```

> Response Example

```json
{
  "uuid": "9ca023a5-851b-4fec-9f0a-48cd83c2eaae",
  "side": "ask",
  "ord_type": "limit",
  "price": "4280000.0",
  "state": "done",
  "market": "KRW-BTC",
  "created_at": "2019-01-04T13:48:09+09:00",
  "volume": "1.0",
  "remaining_volume": "0.0",
  "reserved_fee": "0.0",
  "remaining_fee": "0.0",
  "paid_fee": "2140.0",
  "locked": "0.0",
  "executed_volume": "1.0",
  "trades_count": 1,
  "trades": [
    {
      "market": "KRW-BTC",
      "uuid": "9e8f8eba-7050-4837-8969-cfc272cbe083",
      "price": "4280000.0",
      "volume": "1.0",
      "funds": "4280000.0",
      "side": "ask"
    }
  ]
}
```
### Method
**GET** `/v1/order`

### Operation Code
`Order.Order_info`

### 요청 (Request)

Parameter  | Description
---------  | -----------
uuid       | 주문 UUID
identifier | 조회용 사용자 지정 값

<aside class="warning">
    <code>uuid</code> 혹은 <code>identifier</code> 둘 중 하나의 값이 반드시 포함되어야 합니다.
</aside>

### 응답 (Response)

Parameter         | Description
----------------- | -----------
uuid              | 주문의 고유 아이디
side              | 주문 종류
ord_type          | 주문 방식
price             | 주문 당시 화폐 가격
state             | 주문 상태
market            | 마켓의 유일키
created_at        | 주문 생성 시간
volume            | 사용자가 입력한 주문 양
remaining_volume  | 체결 후 남은 주문 양
reserved_fee	  | 수수료로 예약된 비용
remaining_fee	  | 남은 수수료
paid_fee          | 사용된 수수료
locked            | 거래에 사용중인 비용
executed_volume   | 체결된 양
trade_count       | 해당 주문에 걸린 체결 수
trades            | 체결
trades.market     | 마켓의 유일 키
trades.uuid       | 체결의 고유 아이디
trades.price      | 체결 가격
trades.volume     | 체결 양
trades.funds      | 체결된 총 가격
trades.side       | 체결 종류
trades.created_at | 체결 시각

## Order_info_all (주문 리스트 조회)
주문 리스트를 조회합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Order.Order_info_all()
print(resp['result'])
```

> Response Example

```json
[
  {
    "uuid": "9ca023a5-851b-4fec-9f0a-48cd83c2eaae",
    "side": "ask",
    "ord_type": "limit",
    "price": 4280000,
    "state": "done",
    "market": "KRW-BTC",
    "created_at": {},
    "volume": 1,
    "remaining_volume": 0,
    "reserved_fee": 0,
    "remaining_fee": 0,
    "paid_fee": 2140,
    "locked": 0,
    "executed_volume": 1,
    "trades_count": 1
  },
  ...
]
```

### Method
**GET** `/v1/orders`

### Operation Code
`Order.Order_info_all`

### 요청 (Request)

<table>
  <tr>
    <th>
      Parameter
    </th>
    <th>
      Description
    </th>
  </tr>
  <tr>
    <td>
        market
    </td>
    <td>
        마켓 ID
    </td>
  </tr>
  <tr>
    <td>
        uuids
    </td>
    <td>
        주문 UUID의 목록
    </td>
  </tr>
  <tr>
    <td>
        identifiers
    </td>
    <td>
        주문 identifier의 목록
    </td>
  </tr>
  <tr>
    <td>
        state
    </td>
    <td>
      주문 상태
      <ul>
        <li>wait: 주문 대기 (default)</li>
        <li>done: 전체 체결 완료</li>
        <li>cancel: 주문 취소</li>
      </ul>
    </td>
  </tr>
  <tr>
  <td>
      states
  </td>
  <td>
      주문 상태의 목록
  </td>
</tr>
<tr>
  <td>
      page
  </td>
  <td>
      페이지 수 (default: 1)
  </td>
</tr>
<tr>
  <td>
      limit
  </td>
  <td>
      요청 개수 (default: 100)
  </td>
</tr>
<tr>
  <td>
      order_by
  </td>
  <td>
      정렬 방식
      <ul>
        <li>asc: 오름 차순</li>
        <li>desc: 내림 차순 (default)</li>
      </ul>
  </td>
</tr>
</table>

### 응답 (Response)

Parameter        | Description
---------------- | ------------
uuid             | 주문의 고유 아이디
side             | 주문 종류
ord_type         | 주문 방식
price            | 주문 당시 화폐 가격
state            | 주문 상태
market           | 마켓의 유일키
created_at       | 주문 생성 시간
volume           | 사용자가 입력한 주문 양
remaining_volume | 체결 후 남은 주문 양
reserved_fee     | 수수료로 예약된 비용
remaining_fee    | 남은 수수료
paid_fee         | 사용된 수수료
locked           | 거래에 사용중인 비용
executed_volume  | 체결된 양
trade_count      | 해당 주문에 걸린 체결 수


## Order_new (주문하기)
새로운 주문 요청을 합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Order.Order_new(
    market='KRW-BTC',
    side='bid',
    volume='0.01',
    price='100.0',
    ord_type='limit'
)
print(resp['result'])
```

> Response Example

```json
{
  "uuid":"cdd92199-2897-4e14-9448-f923320408ad",
  "side":"bid",
  "ord_type":"limit",
  "price":"100.0",
  "avg_price":"0.0",
  "state":"wait",
  "market":"KRW-BTC",
  "created_at":"2018-04-10T15:42:23+09:00",
  "volume":"0.01",
  "remaining_volume":"0.01",
  "reserved_fee":"0.0015",
  "remaining_fee":"0.0015",
  "paid_fee":"0.0",
  "locked":"1.0015",
  "executed_volume":"0.0",
  "trades_count":0
}
```

### Method
**POST** `/v1/orders`

### Operation Code
`Order.Order_new`

### 요청 (Request)

<table>
  <tr>
    <th>
      Parameter
    </th>
    <th>
      Description
    </th>
  </tr>
  <tr>
    <td>
        market *
    </td>
    <td>
        마켓 ID (필수)
    </td>
  </tr>
  <tr>
    <td>
        side *
    </td>
    <td>
      주문 종류 (필수)
      <ul>
        <li>bid: 매수</li>
        <li>ask: 매도</li>
      </ul>
    </td>
  </tr>
  <tr>
  <td>
      volume *
  </td>
  <td>
      주문량 (지정가, 시장가 매도 시 필수)
  </td>
</tr>
<tr>
  <td>
      price *
  </td>
  <td>
      주문 가격. (지정가, 시장가 매수 시 필수)
      <br/>
      <br/>
      ex) KRW-BTC 마켓에서 1BTC당 1,000 KRW로 거래할 경우, 값은 1000 이 된다.
      <br/>
      ex) KRW-BTC 마켓에서 1BTC당 매도 1호가가 500 KRW 인 경우, 시장가 매수 시 값을 1000으로 세팅하면 2BTC가 매수된다.
      <br/>
      (수수료가 존재하거나 매도 1호가의 수량에 따라 상이할 수 있음)
  </td>
</tr>
<tr>
  <td>
      ord_type *
  </td>
  <td>
      주문 유형 (필수)
      <ul>
        <li>limit: 지정가 주문</li>
        <li>price: 시장가 주문 (매수)</li>
        <li>market: 시장가 주문 (매도)</li>
      </ul>
  </td>
</tr>
<tr>
  <td>
      identifier
  </td>
  <td>
      주문 조회용 사용자 지정값 (선택)
  </td>
</tr>
</table>

<aside class="warning">
    <b>NOTE</b>: 원화 마켓 가격 단위를 확인하세요.
    <br/>
    <br/>
    원화 마켓에서 주문을 요청 할 경우, <a href="https://docs.upbit.com/docs/%EC%9B%90%ED%99%94-%EB%A7%88%EC%BC%93-%EC%A3%BC%EB%AC%B8-%EA%B0%80%EA%B2%A9-%EB%8B%A8%EC%9C%84">원화 마켓 주문 가격 단위</a>를 확인하여 값을 입력해주세요.
</aside>
<aside class="warning">
    <b>NOTE</b>: identifier 파라미터 사용
    <br/>
    <br/>
    <code>identifier</code>는 서비스에서 발급하는 <code>uuid</code>가 아닌 이용자가 직접  발급하는 키값으로, 주문을 조회하기 위해 할당하는 값입니다. 해당  값은 사용자의 전체 주문 내 유일한 값을 전달해야하며, 비록 주문 요청 시 오류가 발생하더라도 같은 값으로 다시 요청을 보낼 수 없습니다.
    <br/>
    <br/>
    주문의 성공 / 실패 여부와 관계없이 중복해서 들어온 <code>identifier</code> 값에서는 중복 오류가 발생하니, 매 요청시 새로운 값을  생성해주세요.
</aside>
<aside class="warning">
    <b>NOTE</b>: 시장가 주문
    <br/>
    <br/>
    시장가 주문은 <code>ord_type</code> 필드를 <code>price</code> or <code>market</code> 으로 설정해야됩니다.
    <br/>
    <br/>
    매수 주문의 경우 <code>ord_type</code>을 <code>price</code>로 설정하고 <code>volume</code>을 <code>null</code> 혹은 제외해야 합니다.
    <br/>
    매도 주문의 경우 <code>ord_type</code>을 <code>market</code>으로 설정하고 <code>price</code>를 <code>null</code> 혹은 제외해야 합니다.
</aside>

### 응답 (Response)

Parameter        | Description
---------------- | -------------
uuid             | 주문의 고유 아이디
side             | 주문 종류
ord_type         | 주문 방식
price            | 주문 당시 화폐 가격
avg_price        | 체결 가격의 평균가
state            | 주문 상태
market           | 마켓의 유일키
created_at       | 주문 생성 시간
volume           | 사용자가 입력한 주문 양
remaining_volume | 체결 후 남은 주문 양
reserved_fee     | 수수료로 예약된 비용
remaining_fee    | 남은 수수료
paid_fee         | 사용된 수수료
locked           | 거래에 사용중인 비용
executed_volume  | 체결된 양
trade_count      | 해당 주문에 걸린 체결 수

## Order_cancel (주문 취소 접수)
주문 UUID를 통해 해당 주문에 대한 취소 접수를 합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Order.Order_cancel(
    uuid='cdd92199-2897-4e14-9448-f923320408ad'
)
print(resp['result'])
```

> Response Example

```json
{
  "uuid":"cdd92199-2897-4e14-9448-f923320408ad",
  "side":"bid",
  "ord_type":"limit",
  "price":"100.0",
  "state":"wait",
  "market":"KRW-BTC",
  "created_at":"2018-04-10T15:42:23+09:00",
  "volume":"0.01",
  "remaining_volume":"0.01",
  "reserved_fee":"0.0015",
  "remaining_fee":"0.0015",
  "paid_fee":"0.0",
  "locked":"1.0015",
  "executed_volume":"0.0",
  "trades_count":0
}
```

### Method
**DELETE** `/v1/order`

### Operation Code
`Order.Order_cancel`

### 요청 (Request)

Parameter  | Description
---------  | -----------
uuid       | 주문 UUID
identifier | 조회용 사용자 지정 값

<aside class="warning">
    <code>uuid</code> 혹은 <code>identifier</code> 둘 중 하나의 값이 반드시 포함되어야 합니다.
</aside>

### 응답 (Response)

Parameter         | Description
----------------- | -----------
uuid              | 주문의 고유 아이디
side              | 주문 종류
ord_type          | 주문 방식
price             | 주문 당시 화폐 가격
state             | 주문 상태
market            | 마켓의 유일키
created_at        | 주문 생성 시간
volume            | 사용자가 입력한 주문 양
remaining_volume  | 체결 후 남은 주문 양
reserved_fee	  | 수수료로 예약된 비용
remaining_fee	  | 남은 수수료
paid_fee          | 사용된 수수료
locked            | 거래에 사용중인 비용
executed_volume   | 체결된 양
trade_count       | 해당 주문에 걸린 체결 수

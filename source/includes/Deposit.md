# Deposit (입금)

## Deposit_info_all (입금 리스트 조회)
입금 리스트 조회합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Deposit.Deposit_info_all()
print(resp['result'])
```

> Response Example

```json
[
	{
		"type": "deposit",
		"uuid": "20c84493-6e70-4e54-83ce-90915a19d110",
		"currency": "KRW",
		"txid": "BKD-2021-01-07-82a877188ce61d7b4b3c709dad",
		"state": "ACCEPTED",
		"created_at": "2021-01-07T11:59:31+09:00",
		"done_at": "2021-01-07T12:00:12+09:00",
		"amount": "5000.0",
		"fee": "0.0",
		"transaction_type": "default"
	},
	{
		"type": "deposit",
		"uuid": "7b34ea4d-fb46-4da1-9172-8dd42b8814f5",
		"currency": "KRW",
		"txid": "BKD-2021-01-06-fd2ba0cc92670c72fba22f78d0",
		"state": "ACCEPTED",
		"created_at": "2021-01-06T20:42:41+09:00",
		"done_at": "2021-01-06T20:43:15+09:00",
		"amount": "10000.0",
		"fee": "0.0",
		"transaction_type": "default"
    },
    ...
]
```

### Method
**GET** `/v1/deposits`

### Operation Code
`Deposit.Deposit_info_all`

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
        currency
    </td>
    <td>
        Currency 코드
    </td>
  </tr>
  <tr>
    <td>
        state
    </td>
    <td>
      입금 상태
      <ul>
        <li>submitting: 처리 중</li>
        <li>submitted: 처리 완료</li>
        <li>almost_accepted: 입금 대기 중</li>
        <li>rejected: 거절</li>
        <li>accepted: 승인됨</li>
        <li>processing: 처리 중</li>
      </ul>
    </td>
  </tr>
  <tr>
  <td>
      uuids
  </td>
  <td>
      입금 UUID의 목록
  </td>
</tr>
<tr>
  <td>
      txids
  </td>
  <td>
      입금 TXID의 목록
  </td>
</tr>
<tr>
  <td>
      limit
  </td>
  <td>
      개수 제한 (default: 100, limit: 100)
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
        type
    </td>
    <td>
        입출금 종류
    </td>
  </tr>
  <tr>
    <td>
        uuid
    </td>
    <td>
      입금에 대한 고유 아이디
    </td>
  </tr>
  <tr>
  <td>
      currency
  </td>
  <td>
      화폐를 의미하는 영문 대문자 코드
  </td>
</tr>
<tr>
  <td>
      txid
  </td>
  <td>
      입금의 트랜잭션 아이디
  </td>
</tr>
<tr>
  <td>
      state
  </td>
  <td>
      입금 상태
  </td>
</tr>
<tr>
  <td>
      created_at
  </td>
  <td>
      입금 생성 시간
  </td>
</tr>
<tr>
  <td>
      done_at
  </td>
  <td>
      입금 완료 시간
  </td>
</tr>
<tr>
  <td>
      amount
  </td>
  <td>
      입금 수량
  </td>
</tr>
<tr>
  <td>
      fee
  </td>
  <td>
      입금 수수료
  </td>
</tr>
<tr>
  <td>
      transaction_type
  </td>
  <td>
      입금 유형
      <ul>
        <li>default: 일반 입금</li>
        <li>internal: 바로 입금</li>
      </ul>
  </td>
</tr>
</table>

## Deposit_info (개별 입금 조회)
개별 입금 내역을 조회합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Deposit.Deposit_info(
    uuid='20c84493-6e70-4e54-83ce-90915a19d110'
)
print(resp['result'])
```

> Response Example

```json
{
	"type": "deposit",
	"uuid": "20c84493-6e70-4e54-83ce-90915a19d110",
	"currency": "KRW",
	"txid": "BKD-2021-01-07-82a877188ce61d7b4b3c709dad",
	"state": "ACCEPTED",
	"created_at": "2021-01-07T11:59:31+09:00",
	"done_at": "2021-01-07T12:00:12+09:00",
	"amount": "5000.0",
	"fee": "0.0",
	"transaction_type": "default"
}
```

### Method
**GET** `/v1/deposit`

### Operation Code
`Deposit.Deposit_info`

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
        uuid
    </td>
    <td>
        입금 UUID
    </td>
  </tr>
  <tr>
    <td>
        txid
    </td>
    <td>
      입금 TXID
    </td>
  </tr>
  <tr>
  <td>
      currency
  </td>
  <td>
      Currency 코드
  </td>
</tr>
</table>

<aside class="notice">
  <b>NOTE</b>: 파라미터를 입력하지 않으면 가장 최근의 입금 내역을 불러옵니다.
</aside>

### 응답 (Response)

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
        type
    </td>
    <td>
        입출금 종류
    </td>
  </tr>
  <tr>
    <td>
        uuid
    </td>
    <td>
      입금에 대한 고유 아이디
    </td>
  </tr>
  <tr>
  <td>
      currency
  </td>
  <td>
      화폐를 의미하는 영문 대문자 코드
  </td>
</tr>
<tr>
  <td>
      txid
  </td>
  <td>
      입금의 트랜잭션 아이디
  </td>
</tr>
<tr>
  <td>
      state
  </td>
  <td>
      입금 상태
  </td>
</tr>
<tr>
  <td>
      created_at
  </td>
  <td>
      입금 생성 시간
  </td>
</tr>
<tr>
  <td>
      done_at
  </td>
  <td>
      입금 완료 시간
  </td>
</tr>
<tr>
  <td>
      amount
  </td>
  <td>
      입금 수량
  </td>
</tr>
<tr>
  <td>
      fee
  </td>
  <td>
      입금 수수료
  </td>
</tr>
<tr>
  <td>
      transaction_type
  </td>
  <td>
      입금 유형
      <ul>
        <li>default: 일반 입금</li>
        <li>internal: 바로 입금</li>
      </ul>
  </td>
</tr>
</table>

## Deposit_coin_addresses (전체 입금 주소 조회)
내가 보유한 자산 리스트를 보여줍니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Deposit.Deposit_coin_addresses()
print(resp['result'])
```

> Response Example

```json
[
	{
		"currency": "BTC",
		"deposit_address": "3NVw2seiTQddGQwc1apqudKxuTqebpyL3s",
		"secondary_address": null
	},
	{
		"currency": "ETH",
		"deposit_address": "0x60dd373f59862d9df776596889b997e24bee42eb",
		"secondary_address": null
	},
	{
		"currency": "EOS",
		"deposit_address": "eosupbitsusr",
		"secondary_address": "516252ca-0993-454d-bd8b-6bc9db2d4c25"
	},
	{
		"currency": "XRP",
		"deposit_address": "raQwCVAJVqjrVm1Nj5SFRcX8i22BhdC9WA",
		"secondary_address": "22325934"
	},
	...
]
```

### Method
**GET** `/v1/deposits/coin_addresses`

### Operation Code
`Deposit.Deposit_coin_addresses`

### 요청 (Request)

No Parameters

### 응답 (Response)

Parameter         | Description
----------------  | -----------
currency          | 화폐를 의미하는 영문 대문자 코드
deposit_address   | 입금 주소
secondary_address | 2차 입금 주소

<aside class="notice">
  <b>NOTE</b>: 입금 주소 조회 요청 API 유의사항
  <br/>
  <br/>
  입금 주소 생성 요청 이후 아직 발급되지 않은 상태일 경우 <code>deposit_address</code>가 <code>null</code>일 수 있습니다.
</aside>

## Deposit_coin_address (개별 입금 주소 조회)
내가 보유한 개별 자산 내역을 보여줍니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Deposit.Deposit_coin_address(
    currency='BTC'
)
print(resp['result'])
```

> Response Example

```json
{
	"currency": "BTC",
	"deposit_address": "3NVw2seiTQddGQwc1apqudKxuTqebpyL3s",
	"secondary_address": null
}
```

### Method
**GET** `/v1/deposits/coin_address`

### Operation Code
`Deposit.Deposit_coin_address`

### 요청 (Request)

Parameter         | Description
----------------  | -----------
currency *        | 화폐를 의미하는 영문 대문자 코드

### 응답 (Response)

Parameter         | Description
----------------  | -----------
currency          | 화폐를 의미하는 영문 대문자 코드
deposit_address   | 입금 주소
secondary_address | 2차 입금 주소

<aside class="notice">
  <b>NOTE</b>: 입금 주소 조회 요청 API 유의사항
  <br/>
  <br/>
  입금 주소 생성 요청 이후 아직 발급되지 않은 상태일 경우 <code>deposit_address</code>가 <code>null</code>일 수 있습니다.
</aside>

## Deposit_generate_coin_address (입금 주소 생성 요청)
입금 주소 생성을 요청합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Deposit.Deposit_generate_coin_address(
    currency='SNT'
)
print(resp['result'])
```

> Response1 Example: 201 Created

```json
{
    "success": true,
    "message": "SNT 입금주소를 생성중입니다."
}
```

> Response2 Example: 200 OK

```json
{
	"currency": "SNT",
	"deposit_address": "0x72012d8af69263a509af8cd522374fc65c454539",
	"secondary_address": null
}
```

### Method
**POST** `/v1/deposits/generate_coin_address`

### Operation Code
`Deposit.Deposit_generate_coin_address`

### 요청 (Request)

Parameter         | Description
----------------  | -----------
currency *        | 화폐를 의미하는 영문 대문자 코드

### 응답 (Response1)

Parameter  | Description
---------- | -----------
success    | 요청 성공 여부
message    | 요청 결과에 대한 메세지


### 응답 (Response2)

Parameter         | Description
----------------  | -----------
currency          | 화폐를 의미하는 영문 대문자 코드
deposit_address   | 입금 주소
secondary_address | 2차 입금 주소

<aside class="notice">
  <b>NOTE</b>: 입금 주소 생성 요청 API 유의사항
  <br/><br/>
  입금 주소의 생성은 서버에서 비동기적으로 이뤄집니다.
  <br/><br/>
  비동기적 생성 특성상 요청과 동시에 입금 주소가 발급되지 않을 수 있습니다.
  <br/><br/>
  주소 발급 요청 시 결과로 <code>Response1</code>이 반환되며 주소 발급 완료 이전까지 계속 <code>Response1</code>이 반환됩니다.
  <br/><br/>
  주소가 발급된 이후부터는 새로운 주소가 발급되는 것이 아닌 이전에 발급된 주소가 <code>Response2</code> 형태로 반환됩니다.
  <br/><br/>
  정상적으로 주소가 생성되지 않는다면 일정 시간 이후 해당 API를 다시 호출해주시길 부탁드립니다.
</aside>


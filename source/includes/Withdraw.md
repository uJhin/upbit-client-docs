# Withdraw (출금)

## Withdraw_info_all (출금 리스트 조회)

출금 리스트 조회합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Withdraw.Withdraw_info_all()
print(resp['result'])
```

> Response Example

```json
[
  {
    "type": "withdraw",
    "uuid": "35a4f1dc-1db5-4d6b-89b5-7ec137875956",
    "currency": "XRP",
    "net_type": "XRP",
    "txid": "98c15999f0bdc4ae0e8a-ed35868bb0c204fe6ec29e4058a3451e-88636d1040f4baddf943274ce37cf9cc",
    "state": "DONE",
    "created_at": "2019-02-28T15:17:51+09:00",
    "done_at": "2019-02-28T15:22:12+09:00",
    "amount": 1,
    "fee": 0,
    "transaction_type": "default"
  },
  ...
]
```

### Method

**GET** `/v1/withdraws`

### Operation Code

`Withdraw.Withdraw_info_all`

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
      출금 상태
      <ul>
        <li>submitting: 처리 중</li>
        <li>submitted: 처리 완료</li>
        <li>almost_accepted: 출금 대기 중</li>
        <li>rejected: 거부</li>
        <li>accepted: 승인됨</li>
        <li>processing: 처리 중</li>
        <li>done: 완료</li>
        <li>canceled: 취소됨</li>
      </ul>
    </td>
  </tr>
  <tr>
  <td>
      uuids
  </td>
  <td>
      출금 UUID의 목록
  </td>
</tr>
<tr>
  <td>
      txids
  </td>
  <td>
      출금 TXID의 목록
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
      출금에 대한 고유 아이디
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
        net_type
    </td>
    <td>
      출금 네트워크
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
      출금의 트랜잭션 아이디
  </td>
</tr>
<tr>
  <td>
      state
  </td>
  <td>
      출금 상태
  </td>
</tr>
<tr>
  <td>
      created_at
  </td>
  <td>
      출금 생성 시간
  </td>
</tr>
<tr>
  <td>
      done_at
  </td>
  <td>
      출금 완료 시간
  </td>
</tr>
<tr>
  <td>
      amount
  </td>
  <td>
      출금 금액/수량
  </td>
</tr>
<tr>
  <td>
      fee
  </td>
  <td>
      출금 수수료
  </td>
</tr>
<tr>
  <td>
      transaction_type
  </td>
  <td>
      출금 유형
      <ul>
        <li>default: 일반 출금</li>
        <li>internal: 바로 출금</li>
      </ul>
  </td>
</tr>
</table>

## Withdraw_info (개별 출금 조회)

출금 UUID를 통해 개별 출금 정보를 조회합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Withdraw.Withdraw_info(
    uuid='35a4f1dc-1db5-4d6b-89b5-7ec137875956'
)
print(resp['result'])
```

> Response Example

```json
{
  "type": "withdraw",
  "uuid": "35a4f1dc-1db5-4d6b-89b5-7ec137875956",
  "currency": "XRP",
  "net_type": "XRP",
  "txid": "98c15999f0bdc4ae0e8a-ed35868bb0c204fe6ec29e4058a3451e-88636d1040f4baddf943274ce37cf9cc",
  "state": "DONE",
  "created_at": "2019-02-28T15:17:51+09:00",
  "done_at": "2019-02-28T15:22:12+09:00",
  "amount": 1,
  "fee": 0,
  "transaction_type": "default"
}
```

### Method

**GET** `/v1/withdraw`

### Operation Code

`Withdraw.Withdraw_info`

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
        출금 UUID
    </td>
  </tr>
  <tr>
    <td>
        txid
    </td>
    <td>
      출금 TXID
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
  <b>NOTE</b>: 파라미터를 입력하지 않으면 가장 최근의 출금 내역을 불러옵니다.
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
      출금에 대한 고유 아이디
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
        net_type
    </td>
    <td>
      출금 네트워크
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
      출금의 트랜잭션 아이디
  </td>
</tr>
<tr>
  <td>
      state
  </td>
  <td>
      출금 상태
  </td>
</tr>
<tr>
  <td>
      created_at
  </td>
  <td>
      출금 생성 시간
  </td>
</tr>
<tr>
  <td>
      done_at
  </td>
  <td>
      출금 완료 시간
  </td>
</tr>
<tr>
  <td>
      amount
  </td>
  <td>
      출금 수량
  </td>
</tr>
<tr>
  <td>
      fee
  </td>
  <td>
      출금 수수료
  </td>
</tr>
<tr>
  <td>
      transaction_type
  </td>
  <td>
      출금 유형
      <ul>
        <li>default: 일반 출금</li>
        <li>internal: 바로 출금</li>
      </ul>
  </td>
</tr>
</table>

## Withdraw_chance (출금 가능 정보)

해당 통화의 가능한 출금 정보를 확인합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Withdraw.Withdraw_chance(
    currency='BTC',
    net_type='BTC'
)
print(resp['result'])
```

> Response Example

```json
{
	"member_level": {
		"security_level": 4,
		"fee_level": 0,
		"email_verified": true,
		"identity_auth_verified": true,
		"bank_account_verified": true,
		"kakao_pay_auth_verified": true,
		"locked": false,
		"wallet_locked": false
	},
	"currency": {
		"code": "BTC",
		"withdraw_fee": "0.0009",
		"is_coin": true,
		"wallet_state": "working",
		"wallet_support": [
			"deposit",
			"withdraw"
		]
	},
	"account": {
		"currency": "BTC",
		"balance": "0.00048",
		"locked": "0.0",
		"avg_buy_price": "20870000",
		"avg_buy_price_modified": false,
		"unit_currency": "KRW"
	},
	"withdraw_limit": {
		"currency": "BTC",
		"onetime": "50.0",
		"daily": null,
		"remaining_daily": "0.0",
		"remaining_daily_fiat": "1000000000.0",
		"fiat_currency": "KRW",
		"minimum": "0.001",
		"fixed": 8,
		"can_withdraw": true,
		"remaining_daily_krw": "1000000000.0"
	}
}
```

### Method

**GET** `/v1/withdraws/chance`

### Operation Code

`Withdraw.Withdraw_chance`

### 요청 (Request)

| Parameter  | Description                      |
| ---------- | -------------------------------- |
| currency * | 화폐를 의미하는 영문 대문자 코드 |
| net_type * | 출금 네트워크                    |

### 응답 (Response)

| Parameter                            | Description                      |
| ------------------------------------ | -------------------------------- |
| member_level                         | 사용자의 보안 등급 정보          |
| member_level.security_level          | 사용자의 보안 등급               |
| member_level.fee_level               | 사용자의 수수료 등급             |
| member_level.email_verified          | 사용자의 이메일 인증 여부        |
| member_level.identity_auth_verified  | 사용자의 실명 인증 여부          |
| member_level.bank_account_verified   | 사용자의 계좌 인증 여부          |
| member_level.kakao_pay_auth_verified | 사용자의 카카오페이 인증 여부    |
| member_level.locked                  | 사용자의 계정 보호 상태          |
| member_level.wallet_locked           | 사용자의 출금 보호 상태          |
| currency                             | 화폐 정보                        |
| currency.code                        | 화폐를 의미하는 영문 대문자 코드 |
| currency.withdraw_fee                | 해당 화폐의 출금 수수료          |
| currency.is_coin                     | 화폐의 코인 여부                 |
| currency.wallet_state                | 해당 화폐의 지갑 상태            |
| currency.wallet_support              | 해당 화폐가 지원하는 입출금 정보 |
| account                              | 사용자의 계좌 정보               |
| account.currency                     | 화폐를 의미하는 영문 대문자 코드 |
| account.balance                      | 주문 가능 금액/수량              |
| account.locked                       | 주문 중 묶여있는 금액/수량       |
| account.avg_buy_price                | 매수 평균가                      |
| account.avg_buy_price_modified       | 매수 평균가 수정 여부            |
| account.unit_currency                | 평단가 기준 화폐                 |
| withdraw_limit                       | 출금 제약 정보                   |
| withdraw_limit.currency              | 화폐를 의미하는 영문 대문자 코드 |
| withdraw_limit.minimum               | 출금 최소 금액/수량              |
| withdraw_limit.onetime               | 1회 출금 한도                    |
| withdraw_limit.daily                 | 1일 출금 한도                    |
| withdraw_limit.remaining_daily       | 1일 잔여 출금 한도               |
| withdraw_limit.remaining_daily_krw   | 통합 1일 잔여 출금 한도          |
| withdraw_limit.fixed                 | 출금 금액/수량 소수점 자리 수    |
| withdraw_limit.can_withdraw          | 출금 지원 여부                   |

## Withdraw_coin (디지털 자산 출금 하기)

디지털 자산 출금을 요청합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Withdraw.Withdraw_coin(
    currency='BTC',
    net_type='BTC',
    amount='0.01',
    address='3NVw2seiTQddGQwc1apqudKxuTqebpyL3s'
)
print(resp['result'])
```

> Response Example

```json
{
  "type": "withdraw",
  "uuid": "9f432943-54e0-40b7-825f-b6fec8b42b79",
  "currency": "BTC",
  "net_type": "BTC",
  "txid": "ebe6937b-130e-4066-8ac6-4b0e67f28adc",
  "state": "processing",
  "created_at": "2018-04-13T11:24:01+09:00",
  "done_at": null,
  "amount": "0.01",
  "fee": "0.0",
  "krw_amount": "80420.0",
  "transaction_type": "default"
}
```

### Method

**POST** `/v1/withdraws/coin`

### Operation Code

`Withdraw.Withdraw_coin`

### 요청 (Request)

<aside class="notice">
<b>NOTE: 허용된 지갑 주소로만 출금을 진행할 수 있습니다.</b>
<br/><br/>
Open API를 이용하여 출금을 진행하기 위해서는 출금허용주소 등록이 필요합니다. 다음 페이지에서 출금 주소를 등록해주시길 바랍니다.
<br/><br/>
업비트 웹 [마이페이지] > [Open API 관리] > [암호화폐 출금주소 관리] 탭
</aside>

<aside class="warning">
  <b>NOTE: 업비트 회원의 지갑 주소로만 바로출금을 진행할 수 있습니다.</b>
  <br/><br/>
  업비트 회원의 주소가 아닌 주소로 바로출금을 요청하는 경우, 출금이 정상적으로 수행되지 않습니다. 반드시 주소를 확인 후 출금을 진행하시기 바랍니다.
</aside>

<aside class="warning">
  <b>NOTE: (2023-05-22) 출금 네트워크( <code>net_type</code> ) 파라미터가 추가됩니다.</b>
  <br/><br/>
  멀티체인 입출금 지원에 따라, 디지털 자산 출금 요청 시 출금 네트워크( <code>net_type</code> ) 파라미터가 필수로 입력되어야 합니다.
  출금하실 네트워크의 <code>net_type</code> 값은 출금 허용 주소 조회 API를 통해 확인 가능합니다.
  <br/><br/>
  자세한 내용은 <a href="https://docs.upbit.com/changelog/net_type">공지사항</a>을 참조 부탁드립니다.
</aside>

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
        currency *
    </td>
    <td>
        Currency 코드
    </td>
  </tr>
  <tr>
    <td>
        net_type *
    </td>
    <td>
        출금 네트워크
    </td>
  </tr>
  <tr>
    <td>
        amount *
    </td>
    <td>
      출금 수량
    </td>
  </tr>
  <tr>
  <td>
      address *
  </td>
  <td>
      출금 가능 주소에 등록된 출금 주소
  </td>
</tr>
<tr>
  <td>
      secondary_address
  </td>
  <td>
      2차 출금 주소 (필요한 코인에 한해서)
  </td>
</tr>
<tr>
  <td>
      transaction_type
  </td>
  <td>
      출금 유형
      <ul>
        <li>default: 일반 출금</li>
        <li>internal: 바로 출금</li>
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
      출금에 대한 고유 아이디
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
        net_type
    </td>
    <td>
        출금 네트워크
    </td>
  </tr>
<tr>
  <td>
      txid
  </td>
  <td>
      출금의 트랜잭션 아이디
  </td>
</tr>
<tr>
  <td>
      state
  </td>
  <td>
      출금 상태
  </td>
</tr>
<tr>
  <td>
      created_at
  </td>
  <td>
      출금 생성 시간
  </td>
</tr>
<tr>
  <td>
      done_at
  </td>
  <td>
      출금 완료 시간
  </td>
</tr>
<tr>
  <td>
      amount
  </td>
  <td>
      출금 수량
  </td>
</tr>
<tr>
  <td>
      fee
  </td>
  <td>
      출금 수수료
  </td>
</tr>
<tr>
  <td>
      krw_amount
  </td>
  <td>
      원화 환산 가격
  </td>
</tr>
<tr>
  <td>
      transaction_type
  </td>
  <td>
      출금 유형
      <ul>
        <li>default: 일반 출금</li>
        <li>internal: 바로 출금</li>
      </ul>
  </td>
</tr>
</table>

## Withdraw_krw (원화 출금 하기)

원화 출금 요청을 합니다. 등록된 출금 계좌로 출금됩니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Withdraw.Withdraw_krw(
    amount='10000'
)
print(resp['result'])
```

> Response Example

```json
{
  "type": "withdraw",
  "uuid": "35a4f1dc-1db5-4d6b-89b5-7ec137875956",
  "currency": "KRW",
  "txid": "98c15999f0bdc4ae0e8a-ed35868bb0c204fe6ec29e4058a3451e-88636d1040f4baddf943274ce37cf9cc",
  "state": "DONE",
  "created_at": "2019-02-28T15:17:51+09:00",
  "done_at": "2019-02-28T15:22:12+09:00",
  "amount": 1,
  "fee": 0,
  "transaction_type": "default"
}
```

### Method

**POST** `/v1/withdraws/krw`

### Operation Code

`Withdraw.Withdraw_krw`

### 요청 (Request)

| Parameter | Description             |
| --------- | ----------------------- |
| amount *  | 출금액 (출금 원화 수량) |

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
      출금에 대한 고유 아이디
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
      출금의 트랜잭션 아이디
  </td>
</tr>
<tr>
  <td>
      state
  </td>
  <td>
      출금 상태
  </td>
</tr>
<tr>
  <td>
      created_at
  </td>
  <td>
      출금 생성 시간
  </td>
</tr>
<tr>
  <td>
      done_at
  </td>
  <td>
      출금 완료 시간
  </td>
</tr>
<tr>
  <td>
      amount
  </td>
  <td>
      출금 수량
  </td>
</tr>
<tr>
  <td>
      fee
  </td>
  <td>
      출금 수수료
  </td>
</tr>
<tr>
  <td>
      transaction_type
  </td>
  <td>
      출금 유형
      <ul>
        <li>default: 일반 출금</li>
        <li>internal: 바로 출금</li>
      </ul>
  </td>
</tr>
</table>

## Withdraw_coin_addresses (출금 허용 주소 리스트 조회)

등록된 출금 허용 주소 목록을 조회한다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Withdraw.Withdraw_krw(
    amount='10000'
)
print(resp['result'])
```

> Response Example

```json
{
  "currency": "BTC",
  "net_type": "BTC",
  "withdraw_address": "3NVw2seiTQddGQwc1apqudKxuTqebpyL3s",
  "secondary_address": null
}
```

### Method

**POST** `/v1/withdraws/krw`

### Operation Code

`Withdraw.Withdraw_krw`

### 요청 (Request)

No Parameters

<aside class="notice">
  <b>[NOTE] 출금 기능을 이용하기 위해서는 주소 등록이 필요합니다.</b>
  <br/><br/>
  Open API를 통해 디지털 자산을 출금하기 위해서는 출금 허용 주소 등록이 필요합니다.
  <br/><br/>
  <b>[출금 허용 주소 등록 방법]</b>
  <br/>
  업비트 웹 > [MY] > [Open API 관리] > [디지털 자산 출금주소 관리] 페이지에서 진행하실 수 있습니다.
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
      currency
    </td>
    <td>
      출금 화폐
    </td>
  </tr>
  <tr>
    <td>
      net_type
    </td>
    <td>
      출금 네트워크
    </td>
  </tr>
<tr>
  <td>
      withdraw_address
  </td>
  <td>
      출금 주소
  </td>
</tr>
<tr>
  <td>
      secondary_address
  </td>
  <td>
      2차 출금 주소 (필요한 디지털 자산에 한해서)
  </td>
</tr>
</table>

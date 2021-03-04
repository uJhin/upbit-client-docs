# Account (계좌)

## Account_info (전체 계좌 조회)
내가 보유한 자산 리스트를 보여줍니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Account.Account_info()
print(resp['result'])
```

> Response Example

```json
[
    {
        "currency": "BTC",
        "balance": "0.00048",
        "locked": "0.0",
        "avg_buy_price": "20870000",
        "avg_buy_price_modified": false,
        "unit_currency": "KRW"
    },
    {
        "currency": "KRW",
        "balance": "0.34202414",
        "locked": "4999.99999922",
        "avg_buy_price": "0",
        "avg_buy_price_modified": true,
        "unit_currency": "KRW"
    },
    {
        "currency": "ETH",
        "balance": "0.00935861",
        "locked": "0.0",
        "avg_buy_price": "1068000",
        "avg_buy_price_modified": false,
        "unit_currency": "KRW"
    }
]
```

### Method
**GET** `/v1/accounts`

### Operation Code
`Account.Account_info`

### 요청 (Request)

No Parameters


### 응답 (Response)

Parameter              | Description
--------               | -----------
currency               | 화폐를 의미하는 영문 대문자 코드
balance                | 주문가능 금액/수량
locked                 | 주문 중 묶여있는 금액/수량
avg_buy_price          | 매수평균가
avg_buy_price_modified | 매수평균가 수정 여부
unit_currency          | 평단가 기준 화폐


## Account_wallet (입출금 현황)
입출금 현황 및 블록 상태를 조회합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.Account.Account_wallet()
print(resp['result'])
```

> Response Example

```json
[
    {
        "currency": "BTC",
        "wallet_state": "working",
        "block_state": "normal",
        "block_height": 665013,
        "block_updated_at": "2021-01-07T19:44:40.005+00:00",
        "block_elapsed_minutes": 14
    },
    {
        "currency": "POWR",
        "wallet_state": "working",
        "block_state": "normal",
        "block_height": 11609520,
        "block_updated_at": "2021-01-07T19:54:27.007+00:00",
        "block_elapsed_minutes": 5
    },
    {
        "currency": "ETH",
        "wallet_state": "working",
        "block_state": "normal",
        "block_height": 11609520,
        "block_updated_at": "2021-01-07T19:54:25.242+00:00",
        "block_elapsed_minutes": 5
    },
    {
        "currency": "ETC",
        "wallet_state": "working",
        "block_state": "normal",
        "block_height": 11947575,
        "block_updated_at": "2021-01-07T19:54:38.171+00:00",
        "block_elapsed_minutes": 4
    },
    ...
]
```

### Method
**GET** `/v1/status/wallet`

### Operation Code
`Account.Account_wallet`

### 요청 (Request)

No Parameters

<aside class="notice">
    <b>NOTE</b>: 입출금 현황 데이터는 실제 서비스 상태와 다를 수 있습니다.
    <br/>
    <br/>
    입출금 현황 API에서 제공하는 입출금 상태, 블록 상태 정보는 수 분 정도 지연되어 반영될 수 있습니다.
    <br/>
    본 API는 참고용으로만 사용하시길 바라며 실제 입출금을 수행하기  전에는 반드시 업비트 공지사항 및 입출금 현황 페이지를    참고해주시기 바랍니다.
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
        화폐를 의미하는 영문 대문자 코드
    </td>
  </tr>
  <tr>
    <td>
      wallet_state
    </td>
    <td>
      입출금 상태
      <ul>
        <li>working: 입출금 가능</li>
        <li>withdraw_only: 출금만 가능</li>
        <li>deposit_only: 입금만 가능</li>
        <li>paused: 입출금 중단</li>
        <li>unsupported : 입출금 미지원</li>
      </ul>
    </td>
  </tr>
  <tr>
  <td>
      block_state
  </td>
  <td>
      블록 상태
      <ul>
        <li>normal: 정상</li>
        <li>delayed: 지연</li>
        <li>inactive: 비활성 (점검 등)</li>
      </ul>
  </td>
</tr>
<tr>
  <td>
      block_height
  </td>
  <td>
      블록 높이
  </td>
</tr>
<tr>
  <td>
      block_updated_at
  </td>
  <td>
      블록 갱신 시각
  </td>
</tr>
</table>

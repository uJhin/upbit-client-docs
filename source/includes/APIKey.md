# APIKey (API 키)

## APIKey_info (API 키 리스트 조회)
API 키 목록 및 만료 일자를 조회합니다.

> Request Example

```python
from upbit.client import Upbit

access_key = "Your Access Key"
secret_key = "Your Secret Key"

client = Upbit(access_key, secret_key)
resp = client.APIKey.APIKey_info()
print(resp['result'])
```

> Response Example

```json
[
  {
    "access_key" : "xxxxxxxxxxxxxxxxxxxxxxxx",
    "expire_at" : "2021-03-09T12:39:39.000Z"
  },
  {
    "access_key" : "xxxxxxxxxxxxxxxxxxxxxxxx",
    "expire_at" : "2021-03-09T12:39:39.000Z"
  }
]
```

### Method
**GET** `/v1/api_keys`

### Operation Code
`APIKey.APIKey_info`


### 요청 (Request)

No Parameters


### 응답 (Response)

Parameter  | Description
--------   | -----------
access_key | 발급받은 키
expire_at  | 유효 기간

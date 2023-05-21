# APIKey (API 키)

## APIKey_info (API 키 리스트 조회)
API 키 목록 및 만료 일자를 조회합니다.

- Open API를 사용하기 위해선 사용기능 선택과 사용하실 IP 주소를 반드시 입력해야 Open API Key 발급이 가능합니다. Key 발급과 관리는 [해당 페이지](https://upbit.com/mypage/open_api_management)에서 가능합니다.
- Open API Key 발급 당시 입력한 IP 주소로만 접속해야 Open API 사용이 가능하며, Key당 최대 5개까지 등록할 수 있습니다.
- Open API Key는 계정당 10개 까지 발급이 가능합니다.
- 한 계정에서 여러 API 키를 사용하시는 경우 각 키마다 독립적으로 요청 횟수가 측정됩니다.
- Secret key는 최초 1회에 한해 발급되며 추가로 확인하실 수 없으니, 발급받으신 Secret key는 반드시 안전한 곳에 별도로 보관하여 주시기 바랍니다.
- Open API Key 토큰의 유효 기간은 1년이며 연장은 불가합니다. 유효 기간 만료 후 Open API Key를 삭제하여 추가로 발급받아 주시기 바랍니다.
- Open API Key 발급, 수정 및 삭제 시에는 2채널 추가 인증이 필요하며, 필요한 기능의 변경 발생 시에는 [Open API Key 관리](https://upbit.com/mypage/open_api_management)에서 해당 Key를 삭제하신 뒤 다시 등록해 주시기 바랍니다.

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

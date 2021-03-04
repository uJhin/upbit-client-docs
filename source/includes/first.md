# UpbitClient (Upbit 클라이언트 사용하기)
### 클라이언트 객체 생성

> Code Example

```python
from upbit.client import Upbit

access_key = "발급받은 액세스 키"
secret_key = "발급받은 시크릿 키"

client = Upbit(access_key, secret_key)
print(client)
```

> Result

```python
UpbitClient(https://api.upbit.com)
```

설치가 완료되면 `from upbit.client import Upbit`로 패키지를 import 합니다.
그 다음 `UpbitClient` 객체를 생성하면 클라이언트를 사용할 준비가 완료됩니다.


### UpbitClient(access_key=None, secret_key=None, **kwargs)

Parameter  | Description
---------- | -----------
access_key | 발급받은 액세스 키
secret_key | 발급받은 시크릿 키
spec_uri   | Swagger Mapping JSON Path 
config     | Swagger Client Configuration


<aside class="notice">
    <b>NOTE</b>: <b>QUOTATION API (Market, Candle, Trade 섹션 참고)</b>에 대해서는 <code>access_key</code>와 <code>secret_key</code>가 강제되지 않습니다.
</aside>


### 결과

모든 요청에 대한 결과는 JSON 포맷으로 반환됩니다.

남은 요청 제한 시간에 대한 `remaining_request`와 응답 결과 `result`의 키(key) 값을 가집니다.

요청 제한에 대한 부분은 `Remaining Requests (요청 수 제한)` 섹션에서 다룹니다.

Parameter         | Description
----------------  | ------------------
remaining_request | 남은 요청 제한 시간
result            | 요청에 대한 결과

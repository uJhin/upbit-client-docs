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

Parameter            | Description
-------------------- | ------------------
response             | 요청에 대한 응답 객체
response.url         | 요청 URL
response.headers     | 요청 헤더값
response.status_code | HTTP 응답 코드
response.reason      | 응답 메시지
response.text        | 요청에 대한 결과(UTF-8 Text 포맷)
response.content     | 요청에 대한 결과(Byte string 포맷)
response.ok          | HTTP 상태 코드의 200 OK 여부
remaining_request    | 남은 요청 제한 시간
result               | 요청에 대한 결과(JSON 포맷)


### 참고사항

### 1. REST API 요청 시 오류가 발생합니다.

API 요청 처리 중 오류가 발생한 경우 HTTP 응답 body에 에러 코드가 함께 반환됩니다.
주요 에러 코드는 본 문서의 에러코드 항목에서 확인하실 수 있습니다.

만약 위 문서에서 확인되지 않는 오류가 발생하는 경우, 해당 에러 코드를 포함하여 업비트 측에 문의주시기 바랍니다.

### 2. IP 주소를 허용했으나 오류가 발생합니다.

로컬 네트워크에서 확인되는 IP 주소와 실제 통신에 사용하는 IP 주소가 다른 경우가 있습니다.

- **로컬 PC를 이용하시는 경우**: 구글 등의 검색엔진에서 "what is my ip" 혹은 "내 IP 주소" 등을 검색하시어 나오는 외부 IP 주소
- **서버를 이용하시는 경우**: 서버의 외부망 통신에 사용하는 IP 주소

위 주소를 허용 목록에 등록하신 후 다시 시도 부탁드립니다.

### 3. 유동 IP 환경에서 이용하고 싶습니다.

주문하기 및 출금하기 API를 이용하시기 위해서는 허용 IP를 필수적으로 입력해주셔야합니다.

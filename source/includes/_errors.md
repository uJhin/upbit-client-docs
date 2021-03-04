# Errors

> Response Example

```json
{
  "error": {
    "message": "<오류에 대한 설명>",
    "name": "<오류 코드>"
  }
}
```

> Exception Example

```python
from requests import HTTPError

try:
    # Do Something ..
except HTTPError as e:
    # Do Something ..
finally:
    # Do Something ..
```

> Exception Result Example

```console
HTTPError: 429 Client Error: Too Many Requests for url: https://api.upbit.com/v1/~
```

API 요청값이 유효하지 않거나 처리 중 오류가 발생한 경우, HTTP 상태 코드와 함께 다음과 같은 형태의 JSON body가 리턴됩니다.

만약 요청에 실패할 경우, 다음과 같은 예외를 발생시킵니다.


### 400 Bad Request

400 에러는 주로 파라미터 요청 값이 잘못된 경우가 많습니다. 본 문서를 참고하여 올바른 파라미터를 확인해주세요.

<table>
  <tr>
    <th>Error Code</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>
        create_ask_error
        <br/>
        create_bid_error
    </td>
    <td>
      주문 요청 정보가 올바르지 않습니다.
      <br/>
      파라미터 값이 올바른지 확인해주세요.
      <br/>
      <br/>
      특히, 시장가 주문임에도 가격을 입력하여 오류가 발생하는 경우가 많습니다. 주문하기 파라미터를 참고하세요.
    </td>
    <tr>
      <td>
        insufficient_funds_ask
        <br/>
        insufficient_funds_bid
      </td>
      <td>
        매수/매도 가능 잔고가 부족합니다.
      </td>
    </tr>
    <tr>
      <td>
        under_min_total_ask
        <br/>
        under_min_total_bid
      </td>
      <td>
        주문 요청 금액이 최소주문금액 미만입니다.
      </td>
    </tr>
    <tr>
      <td>
        withdraw_address_not_registerd
      </td>
      <td>
        허용되지 않은 출금 주소입니다.
        <br/>
        허용 목록에 등록된 주소로만 출금이 가능합니다.
      </td>
    </tr>
    <tr>
      <td>
        validation_error
      </td>
      <td>
        잘못된 API 요청입니다.
        <br/>
        누락된 파라미터가 없는지 확인해주세요.
      </td>	
    </tr>
</table>

### 401 Unauthorized

401 Unauthorized 오류는 대부분 JWT 서명이 올바르게 되지 않았을 때 발생합니다.

<table>
  <tr>
    <th>Error Code</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>
        invalid_query_payload
    </td>
    <td>
        JWT 헤더의 페이로드가 올바르지 않습니다.
        <br/>
        서명에 사용한 페이로드 값을 확인해주세요.
    </td>
    <tr>
      <td>
        jwt_verification
      </td>
      <td>
        JWT 헤더 검증에 실패했습니다.
        <br/>
        토큰이 올바르게 생성, 서명되었는지 확인해주세요.
      </td>
    </tr>
    <tr>
      <td>
        expired_access_key
      </td>
      <td>
        API 키가 만료되었습니다.
      </td>
    </tr>
    <tr>
      <td>
        nonce_used
      </td>
      <td>
        이미 요청한 nonce값이 다시 사용되었습니다.
        <br/>
        JWT 헤더 페이로드의 nonce 값은 매번 새로운 값을 사용해야합니다.
      </td>
    </tr>
    <tr>
      <td>
        no_authorization_i_p
      </td>
      <td>
        허용되지 않은 IP 주소입니다.
      </td>	
    </tr>
    <tr>
      <td>
        out_of_scope
      </td>
      <td>
        허용되지 않은 기능입니다.
      </td>	
    </tr>
</table>
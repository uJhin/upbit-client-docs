# Authentication (인증)

> Request Example

```json
{
  "access_key": "발급 받은 acccess key (필수)",
  "nonce": "무작위의 UUID 문자열 (필수)",
  "query_hash": "해싱된 query string (파라미터가 있을 경우 필수)",
  "query_hash_alg": "query_hash를 생성하는 데에 사용한 알고리즘 (기본값 : SHA512)"
}
```

Upbit OPEN API는 기본적으로 REST API 요청시, 발급받은 access key와 secret key로 토큰을 생성하여 Authorization 헤더를 통해 전송합니다. 토큰은 <a href="https://jwt.io">JWT</a> 형식을 따릅니다.

서명 방식은 HS256 을 권장하며, 서명에 사용할 secret은 발급받은 secret key를 사용합니다.
Payload의 구성은 예제와 같습니다.

인증방식에 대한 세부적인 코드를 확인하고 싶으시면 <a href="https://github.com/uJhin/upbit-client/blob/main/client/python/upbit/authentication.py"><b>여기</b></a>를 참고해주시기 바랍니다.

<aside class="notice">
<b> NOTE: v1.0.3 업데이트부터 JWT payload를 생성하는 방식이 다음과 같이 변경되었습니다.</b>

<ul>
  <li><code>nonce</code> 필드의 값으로 무작위 UUID 문자열을 이용합니다.</li>
  <li><code>query</code> 필드가 <code>query_hash</code>, <code>query_hash_alg</code> 의 두 가지 필드로 대체됩니다.</li>
</ul>

기존의 JWT payload 생성 방식도 여전히 지원하지만, Open API 이용의 안정성을 위해 추가된 기능이므로 새로운 방식으로 변경하실 것을 권장드립니다.

자세한 사항은 <a href="https://docs.upbit.com/docs">공식 API 문서</a>를 참조해주세요.
</aside>

<aside class="warning">
payload의 <code>query_hash</code> 값을 생성할 때 사용하는 쿼리 값은 <code>query string</code> 이어야 합니다. JSON 및 기타 포멧은 허용되지 않습니다.
</aside>

<aside class="warning">
Signature 생성시 secret encoding 옵션을 확인해주세요. <b>발급된 <code>secret key</code>는 base64로 encoding 되어있지 않습니다.</b> JWT 관련 library를 사용하신다면 해당 옵션을 확인해주세요.
</aside>

<aside class="warning">
<b>NOTE: v1.3.0 업데이트 - urlencoded form 지원 종료 (2022. 3. 1.)</b>
<br/><br/>
2022년 3월부터 <code>urlencoded form</code> 형식을 이용한 HTTP body 요청은 지원이 종료될 예정입니다.
<br/>
JSON 형식을 이용해주시기 바랍니다.
<br/><br/>
자세한 변경사항은 <a href="https://docs.upbit.com/changelog/open-api-%EB%B3%80%EA%B2%BD%EC%82%AC%ED%95%AD-%EC%95%88%EB%82%B4">공지사항</a>을 참조해주세요.
</aside>

<aside class="warning">
<b>NOTE: v1.3.0 업데이트 - 기존 인증방식 지원 종료 (2022. 3. 1.)</b>
<br/><br/>
2022년 3월부터 query 필드를 이용한 JWT 페이로드 생성 방식은 지원이 종료될 예정입니다.
<br/>
<code>query_hash</code> 와 <code>query_hash_alg</code> 필드를 이용한 생성 방식을 이용해주시기 바랍니다.
<br/><br/>
자세한 변경사항은 <a href="https://docs.upbit.com/changelog/open-api-%EB%B3%80%EA%B2%BD%EC%82%AC%ED%95%AD-%EC%95%88%EB%82%B4">공지사항</a>을 참조해주세요.
</aside>

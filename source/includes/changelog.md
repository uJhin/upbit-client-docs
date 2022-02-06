# Change Logs

## 2022

### 2022-02-06
Upbit Client Released: v1.3.1.0

- Update Upbit OPEN API Version 1.3.1
- [Upbit OPEN API 변경사항 안내](https://docs.upbit.com/changelog/open-api-%EB%B3%80%EA%B2%BD%EC%82%AC%ED%95%AD-%EC%95%88%EB%82%B4)를 참고하세요.
- 2022년 3월부터 인증방식 중 JWT 서명방식 지원 사항이 변경될 수 있기 때문에 3월 이후 인증절차 알고리즘이 변경될 수 있습니다.


### 2022-01-14
Upbit Client Released: v1.2.2.4

- Python Websocket Package 버전을 Release 하면서 v10.1 버전으로 반영
- Websocket Client 예제 코드 수정
- 성능 개편 및 소스 코드 리팩토링

## 2021

### 2021-12-06
Upbit Client Released: v1.2.2.2

- RestSharp 버전 업데이트: v105.1.0 -> 106.11.8-alpha.0.13
- Python urllib3 Package 버전 업데이트: v1.26.4 -> v1.26.5
- 그 외 원활한 형상관리를 위해 GitHub Repository에 Dependabot alerts와 CodeQL(Code scanning alerts) Action을 추가하였습니다.

### 2021-12-01
Update Client Released: v1.2.2.1

- Upbit OPEN API 버전 1.2.2 업데이트 반영
- Python Websocket Package 버전 업데이트: v8.1 -> v10.1
- 아래와 같은 이유 때문에 기존의 Python websocket 패키지 버전을 업데이트 했음을 참고하시기 바랍니다. **전체 코드상에는 지장이 없습니다.**
- *Python Websocket Package Issues: The aaugustin websockets library before 9.1 for Python has an Observable Timing Discrepancy on servers when HTTP Basic Authentication is enabled with basic_auth_protocol_factory(credentials=...). An attacker may be able to guess a password via a timing attack.*
- UpbitWebSocket 클래스에 `ping` 메소드 추가
- Websocket의 응답 형식에서 `deprecated` 된 필드들이 삭제됩니다.
- Websocket Ticker(현재가) 응답의 `trade_status` , `market_state_for_ios` 필드 제거
- 자세한 사항은 [여기](https://docs.upbit.com/changelog/open-api-%EA%B0%9C%EC%84%A0%EC%82%AC%ED%95%AD-%EC%95%88%EB%82%B4deprecated-%EB%90%9C-%ED%95%84%EB%93%9C-%EC%82%AD%EC%A0%9C)를 통해 확인 바랍니다.

### 2021-04-01
Update Client Released: v1.2.0.4

- `__init__.py` Docstring 추가
- `authentication.py` 소스 코드 리팩토링

### 2021-03-19
Update Client Released: v1.2.0.3

- Upbit OPEN API 버전 1.2.0 업데이트 반영: **Order** 섹션의 `전체 주문 조회` 항목을 참고하세요.
- `authentication.py` JWT 서명 알고리즘 방식 중 array 타입 파라미터 요청 시 발생하는 버그 픽스
- 모든 JSON 결과값에 `response` 키와 값을 추가하였습니다. **UpbitClient (Upbit Client 사용하기)** 섹션을 참고하세요.
- **에러 및 예외 처리 방식** 변경: 더 이상 `raise` 를 통해 예외를 발생시키지 않습니다. 모든 결과는 json 형식의 `result` 키 값을 통해 에러 메시지를 확인할 수 있도록 변경하였습니다. 자세한 사항은 **Errors** 섹션을 참고하세요.

### 2021-03-04
Update Client Released: v1.1.7.6

- `models.py` 내부 클래스들의 Docstring 파라미터 타입 수정
- 약간의 성능 개선
- 그 외 전체적인 소스 코드 리팩토링

### 2021-02-26
Update Client Released: v1.1.7.5

- `UpbitWebSocket` 클래스 파라미터 오타 수정: `ping_inverval` -> `ping_interval`
- `UpbitWebSocket` 클래스 기능 추가: `socket.connect` 섹션 참고
- 이전보다 원활한 패키지 버전 관리를 위해 `pkginfo.py` 모듈로 분리
- 그 외 부분적인 소스 코드 리팩토링

### 2021-02-23
Update Client Released: v1.1.7.3

- 전체적인 소스 코드 리팩토링

### 2021-02-20
Update Client Released: v1.1.7.0

- Upbit OPEN API 버전 1.1.7 업데이트 반영

### 2021-02-13
Update Client Released: v1.1.6.30

- 부분적인 소스 코드 리팩토링
- 성능 소폭 개선

### 2021-02-05
Update Client Released: v1.1.6.29

- `models.py` 소스 코드 리팩토링: 구조 변경
- 잘못된 요청을 보낼 시 하위 코드에서 `HTTPError` 예외를 발생하도록 수정
- WebSocket Payload Generate 부분 추가 (WebSocket 항목 참고)

### 2021-01-27
Update Client Released: v1.1.6.25

- 웹 소켓(Web Socket) 연결 끊김 문제 해결
- UpbitWebSocket 클래스에 ping 관리를 위한 `ping_interval` 및 `ping_timeout` 파라미터 추가

### 2021-01-26
Update Client Released: v1.1.6.23

- 모든 `response`에 요청 제한 수가 출력되도록 수정
- 웹 소켓(Web Socket) 클라이언트 모듈 추가
- `UpbitWebSocket` 항목 참고
- 그 외 전체적인 소스 코드 리팩토링

### 2021-01-22
Update Upbit OPEN API

- Upbit OPEN API가 업데이트 됨에 따라 아래와 같이 변경되었습니다.
- 주문 리스트 조회 (**GET** /v1/orders): `kind` 요청 파라미터 제거
- 변경 결과: `normal` (일반 주문), `watch` (예약 주문) 동시 조회

### 2021-01-18
Upbit Client Released: v1.1.6.16

- 유틸리티 모듈 `utils.py` 추가
- 주문 가능한 가격 유닛을 검증하는 기능 추가
- `validate_price` 함수 참고

### 2021-01-15
Upbit Client Released: v1.1.6.15

- 남은 요청 수 확인 기능 추가
- 본 문서의 `remaining_request` 파트 참고

### 2021-01-12
Upbit Client Released: v1.1.6.14

- `setup.py` 소스 코드 리팩토링
- [Python Upbit Client](https://github.com/uJhin/python-upbit-client) 저장소 생성 후 분기

### 2021-01-10
Upbit Client Released: v1.1.6.12

- `QUOTATION API` 관련 쿼리 파싱 부분 소스 코드 리팩토링
- `PyPI` 버전 체크 기능 추가

### 2021-01-08
Upbit Client Released: v1.1.6.10

- `uuids` 및 `txids` 쿼리 파싱 추가 구현 및 배포
- `identifiers` 쿼리 파싱 추가 구현 및 배포

### 2021-01-07
Upbit Client Released: v1.1.6.8

- Upbit OPEN API 버전이 1.1.6로 업데이트 되어 최신 버전에 맞춰 구현 및 배포

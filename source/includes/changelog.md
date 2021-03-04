# Change Logs

## 2021

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

# Utils (유틸리티 모듈)

## Validator

### validate_price(price) 원화 마켓 주문 가격 단위

> Example Code

```python
from upbit.utils import Validator

price = 20007
valid = Validator.validate_price(price)
print(valid)
```

> Result Example

```python
20000.0
```

원화 마켓은 호가 별 주문 가격의 단위가 다릅니다. 아래 표를 참고하여 해당 단위로 주문하여 주세요.


최소 호가 (이상) | 최대 호가 (미만) | 주문 가격 단위 (원)
--------------- | --------------- | ------------------
2,000,000       | -               | 1,000
1,000,000       | 2,000,000       | 500
500,000         | 1,000,000       | 100
100,000         | 500,000         | 50
10,000          | 100,000         | 10
1,000           | 10,000          | 5
100             | 1,000           | 1
10              | 100             | 0.1
0               | 10              | 0.01


예를 들어, 호가가 `20,000원` 일 경우 `19,950원`, `20,000원`, `20,050원` 으로 주문을 넣을 수 있으며,
`20,007원`, `20,105원` 등의 가격으로는 주문이 불가능 합니다.

### validate_price(price)
**staticmethod**

가격에 대한 값을 가격 단위에 맞춰 반환합니다.

Parameter  | Description
---------- | -----------
price *    | 가격


### result

Parameter        | Description
---------------- | -----------
validated_price  | 가격 단위에 맞춰진 가격

## 3번째 퍼즐 - Long 자료형 나눗셈

하루를 마이크로초로 나타낸 값을 밀리초로 나타낸 값으로 나누어 봅시다.<br/>
무엇을 출력할까요?

```
public class LongDivision {
	public static void main(String[] args) {
		final long MICROS_PER_DAY = 24 * 60 * 60 * 1000 * 1000;
		final long MILLIS_PER_DAY = 24 * 60 * 60 * 1000;
		System.out.println(MICROS_PER_DAY/MILLIS_PER_DAY);
	}
}
```

<br/>
### 풀이3 - Long 자료형 나눗셈

코드를 실행하면 5를 출력합니다.

이런 문제는 MICROS_PER_DAY가 오버플로되기 때문에 발생합니다. 계산 결과를 long 자료형에 넣는 것은 문제가 되지 않습니다. 문제는 곱셈 연산이 int 자료형들끼리 이루어지며 이 부분에서 오버플로가 발생하는 것입니다.

계산 결과가 이미 오버플로 되었으므로 MICROS_PER_DAY보다 200배 정도 작은 500654080이 할당됩니다. 그리고 이 값을 MILLIS_PER_DAY로 나누므로 5를 출력한 것입니다.

그렇다면 왜 int 자료형끼리 곱셈 연산이 수행된 걸까요?<br/>
곱셈에 사용된 숫자들이 모두 int 자료형이기 때문입니다.

이런 문제를 해결하는 방법으로는, 곱셈에 사용되는 첫 번째 숫자를 long 자료형으로 만들어 주면 됩니다.

```
public class LongDivision {
    public static void main(String[] args) {
        final long MICROS_PER_DAY = 24 * 60 * 60 * 1000 * 1000;
        final long MILLIS_PER_DAY = 24 * 60 * 60 * 1000;
        System.out.println(MICROS_PER_DAY/MILLIS_PER_DAY);
    }
}
```

<br/>
### 정리

**큰 숫자를 다룰 때는 오버플로를 주의하세요!**<br/>
변수의 자료형이 크다고 해서 오버플로가 일어나지 않는 것이 아닙니다. 내부에서 사용하는 변수의 자료형도 확인해야 합니다.



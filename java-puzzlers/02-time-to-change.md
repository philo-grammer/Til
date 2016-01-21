
## 2번째 퍼즐 - 변화를 위한 시간

다음 문제를 어떻게 풀지 생각해 보세요.

> 2달러에서 1.10달러를 빼면?


<br/>
다음과 같은 프로그램은 무엇을 출력할까요?
```
public class Change {
	public static void main(String args[]) {
		System.out.println(2.00 - 1.10);
	}
}
```

<br/>
### 풀이2 - 변화를 위한 시간

자바는 1.1을 정확하게 double로 표현할 수 없습니다.<br/>
따라서 1.1과 가장 근접한 double로 표현합니다.


**간단하게 정리하면 모든 소수가 float 또는 double로 표현될 수 있는 것은 아닙니다.**

```
// 좋지 않은 해결 방법 (여전히 이진 부동소수점 연산 사용)
System.out.printf("$.2f%n", 2.00, 1.10);
```

자바는 float 또는 double 자료형으로 정확한 연산을 할 수 없습니다.
따라서 금육 계산 같은 곳에서 사용하면 안됩니다.

<br/>
>##### 이진 부동소수점 연산

>자바는 '이진 부동소수점 연산'을 사용합니다. 이 방식은 계산이 빠르지만 미세한 오차가 있습니다. 물론 오차가 없는 '심진 부동소수점 연산'도 있지만, 자바 기본 자료형 연산에서 이를 지원하지 않습니다.

>다른 프로그래밍 언어에서도 2.0 - 1.1 을 실행해 보세요. 파이썬, 루비, 자바스크립트에서도 모두 0.89999999999999999를 출력합니다.

<br/>
int 또는 long 자료형 같은 정수 자료형을 이용하면 이런 문제를 해결할 수 있습니다.

```
System.out.pringln((200-110) + " cents");
```

**절대로 BigDecimal(double) 생성자를 사용하지 말고, BigDecimal(String) 생성자를 사용하세요.**

```
import java.math.BigDecimal;
public class Change{
	public class void main(String args[]) {
		System.out.println(new BigDecimal("2.00")
			.subtract(new BigDecimal("1.10")));
	}
}
```

<br/>

### 정리

**정확한 결과가 필요하다면 절대로 float이나 double 자료형을 사용하지 마세요.<br/>금융 계산 같은 곳에는 반드시 int, long, BigDecimal 자료형을 사용하기 바랍니다.**


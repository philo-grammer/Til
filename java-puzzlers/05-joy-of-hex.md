## 5번째 퍼즐 - 16진수의 즐거움

다음 코드는 16진수 2개를 더해서 16진수로 출력합니다.
무엇을 출력할까요?

```
public class JoyOfHex {
	public static void main(String[] args) {
		System.out.println(
			Long.toHexString(0x100000000L + 0xcafebabe));
	}
}
```

<br/>
### 풀이 5 - 16진수의 즐거움

코드를 실행하면 프로그램은 cafebabe를 출력합니다.

long 자료형으로 덧셈을 한 것이 아니라 int 자료형으로 덧셈을 했습니다.

10진수 음수는 뺄셈 기호가 앞에 있는지 확인하면 알 수 있습니다.<br/>
하지만 16진수와 8진수는 다릅니다. 이들은 뺄셈 기호가 붙지 않아도 음수일 수 있습니다.<br/>
16진수와 8진수 값은 상위 비트가 정의되면 음수로 인식합니다.

자바에서는 int 자료형이 long 자료형으로 변환될 때 기본 자료형 확장 변환이 일어납니다.

따라서 더하기 연산의 오른쪽 피연사자인 0xcafebabe는 long 자료형으로 변환되며 0xfffffffcafebabeL이 됩니다.<br/>
0xfffffffcafebabeL + 0x000000100000000L = 0x0000000cafebabeL

이 문제를 고치는 방법은 매우 간단합니다.<br/>
16진수 값도 long 자료형이라는 것을 알 수 있게 L을 붙여 주세요.<br/>
이렇게 하면 부호 확장으로 값이 바뀌는 것을 막을 수 있습니다.<br/>
따라서 1cafebabe를 정상적으로 출력하게 됩니다.

```
public class JoyOfHex {
	public static void main(String[] args) {
		System.out.println(
			Long.toHexString(0x10000000L + 0xcafebabeL));
	}
}
```

<br/>
### 정리

**다양한 진법의 숫자를 함께 연산하지 마세요.**


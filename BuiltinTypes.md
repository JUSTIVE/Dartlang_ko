# 내장 타입

Dart 다음의 타입을 지원합니다.

- 숫자
- 문자열
- 불리언
- 리스트
- 셋
- 맵
- 룬
- 심볼

위의 타입에 대해서는 리터럴을 이용하여 초기화 할 수 있습니다. 예를 들어, `this is a string`은 문자열 상수이고, `true`는 불리언 상수입니다.

이유는 Dart의 모든 변수는 객체이므로, 생성자를 이용하여 변수를 초기화 할 수 있습니다. 몇몇 내장 타입은 고유한 생성자를 가지고 있습니다. 예를 들어, `Map()`을 이용하여 맵을 만들 수 있습니다.

## 숫자

Dart 의 숫자는 두 종류가 있다.

### int

정수 값은 플랫폼에 따라 64비트를 초과할 수 없다. Dart VM에서는 -2$^{-63}$~2$^{63}-1$ 사이의 값을 가질 수 있다. Javascript로 컴파일된 Dart는 Javascript 숫자를 사용한다. 이는 2$^{-53}$~2$^{53}-1$ 사이의 값을 가질 수 있다.

### double

IEEE 754 표준에 정의된 64비트 실수이다.

`int`와 `double` 형은 `num`의 하위타입이다. `num`타입은 +,-,/,* 과 같은 기본 연산 뿐만 아니라 abs(), ceil(), floor()와 같은 연산 또한 지원한다. (>>와 같은 비트 연산자는 int에 정의되어 있다.) 만약 num과 이의 하위타입에 찾는 것이 없다면, `dart:math` 라이브러리에 있을 수 있다.

정수는 소수점이 없는 수이다. 다음은 정수 리터럴을 정의하는 예제이다.
```dart
var x = 1;
var hex = 0xDEADBEEF;
```
만약 숫자가 소수점을 포함한다면, 이는 실수이다. 다음은 실수 리터럴을 정의하는 예제이다.
```dart
var y = 1.1;
var exponents = 1.42e5;
```

Dart 2.1 부터는 정수 리터럴은 필요할 때 실수 리터럴로 자동으로 변한다.
> 버전 노트: Dart 2.1 이전에는 실수 문맥에서 정수를 쓰는 것이 에러였다.

다음은 String에서 숫자로, 혹은 그 반대로 하는 방법이다.
```dart
//문자열 - > 정수
var one = int.parse('1');
assert(one == 1);

//문자열 - > 실수
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

//정수 - > 문자열
String oneAsString = 1.toString();
assert(oneAsString == '1');

//실수 - > 문자열
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

정수 타입은 시프트 연산, &, | 연산과 같은 비트 연산자를 정의합니다.
```dart
assert((3<<1)==6); // 0011 << 1 == 0110
assert((3>>1)==1); // 0011 >> 1 == 0001
assert((3|4)==7); //0011 | 0100 == 0111
```
리터럴 숫자는 컴파일 타임 상수이다. 많은 수식 표현 또한 피연산자들이 컴파일 타임 상수인 경우 컴파일 타임 상수이다.
```dart
const msPerSecond = 1000;
const secondUntilRetry = 5;
const msUntilRetry = secondUntilRetry * msPerSecond;
```
## 문자열

Dart의 문자열은 UTF-16 코드 유닛의 연속이다. 작은따음표 혹은 큰 따옴표를 이용하여 문자열을 만들 수 있다.
```dart
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
```
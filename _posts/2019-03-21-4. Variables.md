# 변수

다음은 변수를 만들고 초기화하는 예제입니다.
```dart
var name = 'Bob';
```

변수는 레퍼런스를 저장합니다. `name`이라 불리는 변수는 "Bob" 이란 값을 가지는 `String` 객체의 레퍼런스를 포함하고 있습니다.

`name` 변수의 타입은 String으로 유추되나, 이를 지정하여 타입을 바꿀 수 있습니다. 만약 객체가 하나의 타입에 제한되지 않는다면, `Object` 나 `dynamic` 타입을 이용하세요.

```dart
dynamic name = 'Bob';
```
또 다른 옵션은 유추될 타입을 명시적으로 선언하는 것입니다.
```dart
String name = 'Bob';
```

## 기본 값

초기화되지 않은 변수들은 초기값으로 `null`을 가집니다. 숫자 타입의 변수일지라도 초기값은 `null`이 되는데, 이유는 Dart의 모든 것들은 객체이기 때문입니다.
```dart
int lineCount;
assert(lineCount == null);
```
## Final 과 Const

만약 변수를 바꿀 의도가 없다면, `var`대신 `final`이나 `const`를 형 앞에 붙이세요. `final` 변수는 한번만 정해질 수 있고, `const` 변수는 컴파일 타임 상수가 됩니다.
최상위 변수 혹은 클래스 변수는 처음 사용되어질 때에 초기화가 됩니다.

> 노트: 인스턴스 변수는 `final`이 될 수 있지만 `const`는 될 수 없습니다. `Final` 인스턴스는 생성자의 몸체가 시작하기 전(생성자의 인자 혹은 생성자의 초기값 변수에 의해 변수가 선언될 시점)에 초기화되어야 합니다.

다음은 final 변수를 만들고 정하는 예제입니다.

```dart
final name = 'Bob';
final String nickname = 'Bobby';
```
여러분은 final 변수의 값을 바꿀 수 없습니다.

```dart
name = 'Alice'; // 에러: final 변수는 한번만 정해질 수 있습니다.
```
변수에 `const`를 사용하여 컴파일 타임 상수를 사용하세요. 만약 const 변수가 클래스 레벨이면, `static const`로 표시하세요. 변수를 선언한 곳에 문자열 상수나, 상수 변수, 혹은 상수 숫자들의 계산 결과값 등의 컴파일 상수를 대입하세요.
```dart
var foo = const [];
final bar = const [];
const baz = []; // const []와 동일
```
`const`  선언 표현에서는 `const`를 생략할 수 있습니다. 위의 `baz`의 예를 보세요.

여러분은 `final`이 아닌 변수의 값을 바꿀 수 있습니다. 심지어는 상수값이었어도요.
```dart
foo = [1,2,3]; //const []였음
```
그러나 const 변수의 값은 바꿀 수 없습니다.
```dart
baz = [42]// 에러: Constant 변수는 값이 배정될 수 없습니다.
```
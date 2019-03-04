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
표현식의 값의 내부에 문자열을 `${표현}` 으로 대입할 수 있다. 만약 표현이 식별자이면, `{}`를 생략할 수 있다. 해당 객체의 문자열을 구하고 싶다면, 객체의 `toString`을 호출하라.
```dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
'Dart has string interpolation, ' +
'which is very handy');
assert('That deserves all caps. '+
'${s.toUpperCase()} is very handy!' == 
'That deseves all caps. STRING INTERPOLATION is very handy!');
```

> 노트: == 연산자는 두 객체가 같은지 시험한다. 두 문자열은 같은 코드열을 가지고 있으면 대신할 수 있다.

이웃한 문자열 리터럴은 `+` 연산자를 이용하여 이을 수 있다.
```dart
var s1 = 'String '
'concatenation'
" works even over line breaks.";
assert(s1 == 'String concatenation works even over '
    'line breaks.');
var s2 = 'the + operator '+'works, as well';
assert(s2 == 'the + operator works, as well');
```
여러 줄의 문자열을 만드는 다른 방법은 작은따음표 혹은 큰따옴표 세 개를 이용하는 것이다.
```dart
var s1 = '''
You can craete
multi-line strings like this one.
''';

var s2 = """ This is also a
multi-line string.""";
```
`r`접두어를 붙임으로써 "raw"문자열을 만들 수 있다.
```dart
var s = r'In a raw string, not even \n gets special treatment.';
```

문자열 상수는 보간된 표현의 평가값이 null, 숫자, 문자열, 불리언 컴파일 상수일 경우 컴파일 타임 상수입니다.
```dart
///이것은 문자열 상수이다.
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

//이것들은 문자열 상수로 작동하지 않음
var aNum = 0;
var aBool = true;
var aString = 'a string';
const aConstList = [1,2,3];

const validConstString = '$aConstNum $aConstBool $aConstString';
//const invalidConstString = '$aNum $aBool $aString $aConstList';
```

## 불리언

불리언 값을 표현하기 위해서는 Dart는 `bool`이라는 이름의 타입이 있다. 오직 두 객체만이 bool 타입을 가진다: 불리언 리터럴은 컴파일 타임 상수인  `true`와 `false`가 있다.

Dart의 타입 안정성은 `if(nonbooleanValue)`나 `assert(nonbooleanValue)`와 같은 코드를 쓸 수 없다는 것이다.
```dart
//빈 문자열 체크
var fullName = '';
assert(fullName.isEmpty);

//0 체크
var hitPoints = 0;
assert(hitPoints <= 0);

//null 체크
var unicorn;
assert(unicorn == null);

//NaN 체크
var iMeantToDoThis = 0 / 0;
assert(iMeantToDoThis.isNaN);
```

## 리스트

모든 프로그래밍 언어들의 가장 기본적인 컬렉션은 배열, 혹은 객체의 순서 집합일 것이다. Dart 에서는, 배열은 리스트 객체이고, 대부분의 사람들은 그들을 그냥 Dart 리스트라 부른다.

Dart 리스트 리터럴은 자바스크립트 배열 리터럴과 비슷해 보인다. 다음은 간단 한 Dart 리스트이다.
```dart
var list = [1,2,3];
```
>노트: Dart는 리스트가 List<int> 타입을 가지고 있다고 추정합니다. 만약 비-정수 객체를 이 리스트에 추가하려 한다면, 분석기 혹은 런타임은 에러를 발생할 것입니다.

리스트는 0-기반 인덱싱을 사용하며, 이는 0이 첫 요소의 인덱스이고, list.length -1 이 마지막 요소의 인덱스입니다. 또한 자바스크립트에서 그랬듯 리스트의 길이를 가져오고 요소를 참조할 수 있습니다.
```dart
var list = [1,2,3];
assert(list.length == 3);
assert(list[1]==2);

list[1] = 1;
assert(list[1]==1);
```
컴파일 타임 상수인 리스트를 만들기 위해서는 리스트 리터럴 앞에 const를 붙이세요.
```dart
var constantList = const [1,2,3];
//constantList[1] = 1;// 주석을 풀면 에러가 납니다.
```
리스트 타입은 리스트를 관리하는 많은 편리한 메소드들을 포함하고 있습니다.

## 셋

Dart에서의 셋은 고유한 요소의 비순서적인 집합이다. Dart는 셋 리터럴과 Set 타입을 통해 셋을 지원한다.

> 버전 노트: Set은 항상 Dart의 코어에 있었으나, Set 리터럴은 Dart2.2에 추가되었습니다.

다음은 Set 리터럴을 이요하여 만든 간단한 Dart Set이다.
```dart
var halogens = {'fluorine','chlorine','bromine','iodine','astatine'};
```
>노트: Dart는 halogens가 Set<String>타입을 가지고 있다고 유추합니다. 만약 이 셋에 다른 타입의 값을 넣으려고 한다면, 분석기 혹은 런타임이 오류를 발생할 것입니다.

빈 셋을 만들기 위해서는 {}앞에 형식 인자를 붙이거나 {}를 Set 타입에 대입하세요.
```dart
var names = <String>{};
// Set<String> names = {}; //이것도 동작합니다.
// var names = {}; //Map을 생성합니다. 셋이 아니라.
```
> 셋 혹은 맵? 맵 리터럴의 문법은 셋 리터럴과 비슷할 수 있습니다. 왜냐면 맵 리터럴이 먼저 등장했고, `{}`는 맵 타입의 기본값이기 때문입니다. 만약 {}혹은 배정할 변수에 타입 지정자를 빼먹었다면, Dart는 Map<dynamic, dynamic> 타입의 객체를 만들 것입니다.

이미 생성된 set에 새 요소를 추가할 때는 `add()`혹은 `addAll()` 메소드를 이용합니다.
```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
```
`.length`를 이용하여 셋에 있는 요소들의 개수를 구할 수 있습니다.
```dart
var elemtents = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
assert(elements.length == 5);
```
컴파일 타임 상수의 set을 만들기 위해서는 셋 리터럴 앞에 `const`를 붙이세요.
```dart
final constantSet = 
    const {'fluorine','chlorine','bromine','iodine','astatine'};
// constantSet.add('helium'); //이 주석을 풀면 에러가 발생합니다.
```

## 맵


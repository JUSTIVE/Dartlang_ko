# 키워드

다음의 키워드는 Dart 언어에서 특별히 취급하는 키워드의 모음이다.

|||||
|--|--|--|--|
|abstract$^2$| dynamic$^2$ |implements$^2$| show$^1$|
|as$^2$|else| import$^2$|static$^2$|
|assert|enum|in|super|
|async$^1$|export$^2$|interface$^2$|switch|
|await$^3$|extends|is|sync$^1$|
break|external$^2$|library$^2$|this
case|factory|mixin|throw|
catch|false|new|true
class|final|null|try
const|finally|on$^1$|typedef$^2$
continue|for|operator$^2$|var
covariant$^2$|Function$^2$|part$^2$|void
default|get$^2$|rethrow|while
deferred$^2$|hide$^1$|return|with
do|if|set$^2$|yield

이러한 단어들을 식별자로 사용하지 마라. 하지만 필요한 경우, 첨자가 달린 키워드들은 식별자로 쓸 수 있다.
1. 문맥적 키워드로 특정한 곳에서만 의미를 가진다. 이들은 어디서는 식별자로 사용 가능하다.
2. 내장 식별자이다. 자바스크립트 코드를 다트로 편하기 옮기기 위해서는, 대부분의 장소에서 이 키워드는 식별자로 사용이 가능하나, 이들은 클래스, 타입 이름, 혹은 import 접두어로 사용될 수는 없다.
3. 이들은 Dart 1.0 이후에 비동기 지원을 위해 추가된 제한된 예약어들이다. `async`, `async*`, `sync*`로 정의된 함수 내에서는 `await`이나 `yield`를 식별자로 사용 할 수 없다.
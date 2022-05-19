# - 느슨한 타입(loosely typed)의 동적(dynamic) 언어 
- JavaScript의 변수는 어떤 특정 타입과 연결되지 않으며, 모든 타입의 값으로 할당 및 재할당 가능하며 원시 값과 객체로 나뉜다.
```js
let foo = 42 // foo가 숫자
foo = 'bar' // foo가 이제 문자열
foo = true // foo가 이제 불리언
```
### - 원시 값
객체를 제외한 모든 타입은 불변 값(변경할 수 없는 값)을 정의한다.
1.  Boolean 타입  
논리 요소를 나타내며 `true`와 `false` 두 가지의 값을 가질 수 있다
2. Null 타입  
`null` 하나의 값만 가질 수 있다.
3. Undefined 타입  
값을 할당하지 않은 변수는 `undefined` 값을 가지고 있다.
4. Number 타입  
부동소수점 숫자 외에도 `+Infinity`, `-Infinity`, `NaN("Not a Number")` 세 개의 상징적인 값을 가진다.  
`±Infinity` 범위 내에서 가능한 가장 크거나 작은 수를 확인하려면 `Number.MAX_VALUE`와 `Number.MIN_VALUE` 상수를 사용할 수 있다.  
Number의 안전 한계는 `Number.MAX_SAFE_INTEGER`로 알아볼 수 있다.  
5. BigInt타입  
임의 정밀도로 정수를 나타낼 수 있는 JavaScript 숫자 원시 값  `BigInt` Number의 안전 한계를 넘어서는 큰 정수도 안전하게 저장하고 연산할 수 있다.  
    1. 정수 끝에 n을 추가하거나 생성자를 호출해 생성할 수 있다.  
    2. Number 안전 한계를 넘는 숫자에 대해 계산이 가능해졌다.  
    3. `+, *, -, **, % 연산자`를 사용할 수 있다.  
    4. `Number`와 같지는 않지만 유사하다.  
    5. `if, ||, &&, Boolean, !`처럼 **불리언** 변환이 발생하는 곳에서는 Number처럼 동작한다.  
    6. `Number`와 혼합해 연산할 수 없으며, 혼합해 사용 시 `TypeError`가 발생한다.
    
다음 예제는 `Number.MAX_SAFE_INTEGER` 밖으로 나가는 정수에서도 예상된 값을 반환 한다.
``` js  
> const x = 2n ** 53n;
9007199254740992n
> const y = x + 1n;
9007199254740993n
```
6. String 타입  
텍스트 데이터를 나타낼 때 사용하며 String은 16비트 부호 없는 정수 값 `"요소"`로 구성된 집합으로, 각각의 요소가 String의 한 자리를 차지한다. 첫 번째 요소는 인덱스 0에, 그 다음 요소는 인덱스 1, 그 다음은 2, ... 방식으로 String의 길이는 그 안의 요소 수와 같다.  
C 언어와 같은 일부 프로그래밍 언어와 달리 JavaScript 문자열은 생성한 후 바꾸는 것은 불가능하지만 원본 문자열을 사용해 새로운 문자열을 생성하는 것은 가능하다. 예시로,  
    - 원본 문자열에서 각각의 문자를 선택하거나 `String.substr()`을 사용해 생성한 부분문자열
    - `부분문자열 연결 연산자(+)`를 사용하거나  `String.concat()`을 사용해 두 개의 문자열을 합침  
- 다음과 같은 장점이 있습니다.
    - 연결 연산자를 통해 복잡한 문자열을 쉽게 만들 수 있다.  
    - 디버깅이 쉽다. (출력 내용이 항상 문자열의 값과 동일)  
    - 문자열은 많은 API(입력 칸 (en-US), 로컬 스토리지 값, responseText와 함께 사용하는 XMLHttpRequest 등등)의 공통 분모다.  
    - 규칙만 잘 정한다면 어떤 자료구조라도 문자열로 표현할 수 있다.  
- 단점은
    - 구분자를 사용하면 문자열로 리스트를 흉내낼 수도 있으나 구분자를 리스트의 요소로 사용하는 순간 리스트가 망가지고 만다 구분자를 구분하기 위해 이스케이프 문자를 선택하고, 등등... 이 모든 것이 각자의 규칙을 필요로 하고 불필요한 유지보수 부담이 생길 수도 있다.
    
    문자열은 텍스트 데이터에만 사용하고 복잡한 데이터를 표현해야 할 땐 문자열을 파싱해서 적합한 추상화로 덮어서 사용
7. Symbol 타입  
고유하고 변경 불가능한 원시 값이며 어떤 프로그래밍 언어들에선 "아톰"이라고 부르기도 한다.
"심볼" 데이터 형식은 값으로 익명의 `객체 속성(object property)`을 만들 수 있는 특성을 가진 `원시 데이터 형식(primitive data type)`입니다. 이 데이터 형식은 클래스나 `객체 형식(object type)`의 내부에서만 접근할 수 있도록 `전용(private) 객체 속성의 키(key)`로 사용됩니다.

### 객체(object)  
식별자로 참조할 수 있는 메모리 상의 값
객체 리터럴 구문을 사용해 제한적으로 속성을 초기화할 수의 있고, 속성을 추가 및 제거할 수 있다.  
속성 값은 다른 객체를 포함해 모든 타입을 사용할 수 있고 복잡한 자료구조의 구축이 가능하다.  
속성은 '키' 값으로 식별하며, 키 값은 문자열 값이나 심볼을 사용할 수 있다.
# JavaScript 형변환  
자바스크립트는 타입이 매우 유연한 언어이며 자바스크립트 엔진이 필요에 따라 `‘암시적변환’`을 개발자의 의도에 따라 `‘명시적변환’` 을 실행

- 암시적변환  
자바스크립트 엔진이 필요에 따라 자동으로 데이터타입을 변환

산술 연산자
더하기(+) 연산자는 숫자보다 문자열이 우선시 되기때문에, 숫자형이 문자형을 만나면 문자형으로 변환하여 연산  
(문자 > 숫자)
``` js
// 더하기(+)
number + number     // number
number + string     // string
string + string     // string
string + boolean    // string
number + boolean    // number
50 + 50;        //100
100 + “점”;     //”100점”
“100” + “점”;   //”100점”
“10” + false;   //”100"
99 + true;      //100
```
다른 연산자(-,*,/,%)는 숫자형이 문자형보다 우선시되기 때문에 더하기와 같은 문자형으로의 변환이 일어나지 않는다.  
(문자 < 숫자)
``` js
//다른 연산자(-,*,/,%)
string * number     // number
string * string     // number
number * number     // number
string * boolean    //number
number * boolean    //number
“2” * false; //0
2 * true; //2
```
동치 비교
아래의 예제는 엄격하지 않은 동치(==) 비교이며, 아래의 결과값은 좌우항 변환 할 경우 모두 ‘0 == 0 이기때문에’ 
``` js
`true` 이다.

null == undefined
“0” == 0
0 == false
“0” == false
```
여기서 유의해야 할 점은 위의 비교는 엄격하지 않은 동치(==) 비교일 경우이기 때문에, 두 값을 비교할 때 데이터타입을 변환하지 않는 엄격한 동치(===) 비교와 혼동되지 않도록 한다.

## 명시적변환  
개발자가 의도를 가지고 데이터타입을 변환

타입을 변경하는 기본적인 방법은 `Object(), Number(), String(), Boolean()` 와 같은 함수를 이용하는데 new 연산자가 없다면 사용한 함수는 타입을 변환하는 함수로써 사용된다.  
- A Type → Number Type  
`Number()`는 정수형과 실수형의 숫자로 변환
``` js
Number(“12345”);    //12345
Number(“2”*2);      //4
``` 
`parseInt()`는 정수형의 숫자로 변환한다. 만약 문자열이 `숫자 0` 으로 `시작하면 8진수로`인식하고(구형브라우저 O,신형브라우저 X), `0x, 0X` 로 시작한다면 해당 문자열을 16진수 숫자로 인식한다. 또한 앞부분 빈 공백을 두고 나오는 문자는 모두 무시되어 `NaN`을 반환
``` js
parseInt(“27”)      //27
parseInt(0033);     //27
parseInt(0x1b);     //27
parseInt(“ 2”);     //2
parseInt(“ 2ㅎ”);   //2
parseInt(“ ㅎ2”);   //NaN
```
`parseFloat()`는 부동 소수점의 숫자로 변환한다. `parseInt()`와는 달리 `parseFloat()`는 항상 10진수를 사용하며 `parseFloat()` 또한 앞부분 빈 공백을 두고 나오는 문자는 모두 무시되어 NaN을 반환한다.
``` js
parseFloat(“!123”); //NaN
parseFloat(“123.123456”); //123.123456
parseInt(“123.123456”); //123
parseFloat(“ 123.123456”); //123.123456
parseFloat(“ a123.123456”); //NaN
```
- A Type → String Type
다른 자료형을 문자타입으로 변형하는 방법은 아래와 같다.  
`String()`는 숫자를 문자열로 변환
``` js
String(123); //”123"
String(123.456); //”123.456"
```
`toString()`는 인자로 기수를 선택할 수 있다. 인자를 전달하지 않으면 10진수로 변환한다.
```js
let trans = 100;
trans.toString(); //”100"
trans.toString(2); //”1100100"
trans.toString(8); //”144"
let boolT = true;
let boolF = false;
boolT.toString(); //”true”
boolF.toString(); //”false”
```
`toFixed()`의 인자를 넣으면 인자값만큼 반올림하여 소수점을 표현하며 소수점을 넘치는 값이 인자로 들어오면 `0`으로 길이를 맞춘 문자열을 반환한다.
```js
let trans = 123.456789;
let roundOff = 99.987654;
trans.toFixed(); //”123"
trans.toFixed(0); //”123"
trans.toFixed(2); //”123.46"
trans.toFixed(8); //”123.45678900"
roundOff.toFixed(2); //”99.99"
roundOff.toFixed(0); //”100"
```
- A Type → Boolean Type
다른 자료형을 불린타입으로 변형하는 방법은 아래와 같다.

Boolean()은 값이 없거나 `0, -0, null, false, NaN, undefined, 빈 문자열 ("")`이라면 객체의 초기값은 `false` 그 외에 값은 `true`
```js
Boolean(100); //true
Boolean(“1”); //true
Boolean(true); //true
Boolean(Object); //true
Boolean([]); //true
Boolean(0); //false
Boolean(NaN); //false
Boolean(null); //false
Boolean(undefined); //false
Boolean( ); //false
```
# ==, === (동치 비교 및 동일성)
추상적(abstract) 같음 비교 (==)  
엄격한(strict) 같음 비교 (===): `Array.prototype.indexOf`, `Array.prototype.lastIndexOf` 및 `case` 절 매칭에 쓰임
-  ===를 사용하는 엄격한 같음  
두 값이 같은 지 비교. 어느 값도 비교되기 전에 어떤 다른 값으로 남몰래 변환되지 않으며 둘이 서로 다른 형이면,
둘은 같지 않다고 여긴다.  
둘이 같은 형이고 숫자가 아닌 경우, 같은 값이면 같다고 여긴다.  
둘이 숫자인 경우, 둘 다 `NaN`이 아닌 같은 값이거나 하나는 `+0` 또 하나는 `-0`인 경우 같다고 여긴다.
```js
var num = 0;
var obj = new String("0");
var str = "0";
var b = false;

console.log(num === num); // true
console.log(obj === obj); // true
console.log(str === str); // true

console.log(num === obj); // false
console.log(num === str); // false
console.log(obj === str); // false
console.log(null === undefined); // false
console.log(obj === null); // false
console.log(obj === undefined); // false
```
- ==를 사용하는 느슨한 같음  
느슨한 같음(loose equality)은 두 값이 같은 지 비교합니다, 두 값을 공통(common) 형으로 변환한 후에. 변환 후 (하나 또는 양쪽이 변환을 거칠 수 있음), 최종 같음 비교는 꼭 `===`처럼 수행됩니다.  
느슨한 같음은 대칭(symmetric)이다: `A == B`는 A 및 B가 어떤 값이든 항상 `B == A`와 같은 의미를 갖는다 (적용된 변환의 순서 말고는)  
`undefined 과 null`이 거의 같습니다. 즉, `undefined == null`은 `true`이고 `null == undefined`는 `true`다.

- 느슨한 타입(loosely typed)의 동적(dynamic) 언어의 문제점은 무엇이고 보완할 수 있는 방법에는 무엇이 있을지 생각해보세요.  
    1. 실행 도중에 변수에 예상치 못한 자료형이 들어와 TypeError를 발생할 수 있음.  
    2. 타입 관련 Error는 런타임 시 확인할 수 밖에 없기 때문에, 코드가 길고 복잡해질 경우 타입 에러를 찾기가 어려워짐  
이런 한 문제를 해결하기 위해 `TypeScript`나 `Flow` 등을 사용할 수 있다.
- undefined와 null의 미세한 차이들을 비교해보세요.
```js
typeof null             // 'object'
typeof undefined        // 'undefined'
null === undefined      // false
null == undefined       // true
null === null           // true
null == null            // true
!null                   // true
isNaN(1 + null)         // false
isNaN(1 + undefined)    // true
```
# 9장 타입변환과 단축 평가

## 9.1 타입 변환이란 ?

- 개발자가 의도적으로 값의 타입을 변환 하는 것을 명시적 타입 변환 또는 타입 캐스팅이라 한다.
  개발자의 의도와 관계없이 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환하는 것을 암묵적 타입변환 또는 타입강제 변환이라 한다.

  ```jsx
  var x = 10;
  // 명시적 타입 변환
  // 숫자를 문자열로 타입 캐스팅

  var str = x.toString();
  console.log(typeof str, str); // string 10

  console.log(typeof x, x); // number 10

  var str = x + "";
  console.log(typeof str, str); // string 10

  // x 변수와 값이 변경된 것은 아니다.
  console.log(typeof x, x); // number 10

  var str = x + "";
  console.log(typeof str, str); // string 10

  // x 변수와 값이 변경된 것은 아니다.
  console.log(typeof x, x); // number 10
  ```

  명시적 타입 변환, 암묵적 타입 변환이 기존 원시 값을 직접 변경하는 것은 아니다. 타입 변환이란 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것이다.
  암묵적 타입변환 → 기존 변수 값을 재할당하여 변경하는 것이 아니라 자바스크립트 엔진은 표현식을 에러 없이 평가하기 위해 피연산자의 값을 암묵적으로 타입 변환해 새로운 값을 만들어 단 한 번 사용하고 버린다.

  ## 9.2 암묵적 타입 변환

```jsx
// 피연산자가 모두 문자열 타입 이어야 하는 문맥
a = "10";
b = 5;
console.log(a + b); // '105'

// 피연산자가 모두 숫자 타입이어야 하는 문맥
c = 5;
d = "100";
console.log(c * d); // 500
```

→ 암묵적 타입 변환이 발생하면 문자열, 숫자, 불리언과 같은 원시 타입 중 하나로 타입을 자동 변환한다.

### 9.2.1 문자열 타입으로 변환

- ‘+’ 연산자는 피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작한다. 문자열 연결 연산자의 역할은 문자열 값을 만드는 것이다.

```jsx
1 + "2"; // '12'
```

(+) 연산자는 피연산자 중 하나 이상이 문자열이면 문자열 연결 연산자로 동작한다.

ex)

```jsx
// 숫자 타입
-0 + '' // '0'
-1 + '' // '-1'
NaN + '' // 'NaN'

// 불리언 타입
true + '' // 'true'
false + '' // 'false'

// 심벌 타입
(Symbol()) + '' // typeError

//객체 타입
({}) + '' // '[object Object]'
Math + ''// '[object Math]'
[] + '' // ''
[10, 20] + '' //'10,20'
```

### 9.2.2 숫자 타입으로 변환

```jsx
1 - "1"; // 0
1 * "10"; // 10
1 / "one"; // 'NaN'
```

```jsx
// 문자열 타입
+"" + // 0
  "0" + // 0
  "string" + // NaN
  // 불리언 타입
  true + // 1
  false + // 0
  // null 타입
  null + // 0
  // undefined 타입
  undefined + // NaN
  // 심벌 타입
  Symbol() + // TypeError
  // 객체
  {} + // NaN
  [] + // 0
  [10, 20] + // NaN
  function () {}; // NaN
```

→ 객체, 빈 배열이 아닌 배열, undefined는 NaN가 된다.

### 9.2.3 불리언 타입으로 변환

- if문이나 for문 같은 제어문 또는 삼항 조건 연산자의 조건식은 불리언 값으로 평가 되어야 하는 표현식이다.

```jsx
if ("") console.log(x); // 빈 문자열이라 값이 출력되지 않음!
```

ex)

```jsx
if (true) console.log("2");
if (0) console.log("3");
if ("str") console.log("4");
if (null) console.log("5");
// 2 4
```

→ `false` , `undefined` , `null` , `0, -0` , `NaN` , `''(빈문자열)`

위와 같은 Falsy값은 출력되지 않는다.

## 9.3 명시적 타입 변환

- 개발자의 의도에 따라 명시적으로 타입을 변경하는 방법이다.
  1. 생성자 함수(String, Number, Boolean)를 new 연산자 없이 호출하는 방법
  2. 빌트인 메서드를 사용하는 방법
  3. 암묵적 타입 변환

### 9.3.1 문자열 타입으로 변환

1. String 생성자 함수를 new 연산자 없이 호출하는 방법
2. Object.prototype.toString 메서드를 사용하는 방법
3. 문자열 연결 연산자를 이용하는 방법

```jsx
// 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 -> 문자열 타입
String(NaN); // "NaN"
String(Infinity); // "Infinity"

// 불리언 타입 -> 문자열 타입
String(true); // "true"

// 2. Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 -> 문자 타입
(1).toString(); // "1"
NaN.toString(); // "NaN"
Infinity.toStirng(); // "Infinity"

// 불리언 타입 -> 문자열 타입
true.toString(); // "true"

// 3. 문자열 연결 연산자를 이용하는 방법
// 숫자 타입 -> 문자열 타입
true + ""; // "true"
```

### 9.3.2 숫자 타입으로 변환

1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
3. (+) 단항 산술 연산자를 이용하는 방법
4. (\*) 산술 연산자를 이용하는 방법

```jsx
//1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 -> 숫자 타입
Number("0"); // 0
Number("10.53"); // 10.53
// 불리언 타입 -> 숫자 타입
Number(true); // 1

// 2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
// 문자열 타입 -> 숫자 타입
parseInt("0"); // 0
parseInt("10.53") + // 10.53
  // 3. (+) 단항 산술 연산자를 이용하는 방법
  // 문자열 타입 -> 숫자 타입
  "0"; // 0
+"10.53" + // 10.53
  // 불리언 타입 -> 숫자 타입
  true; // 1

// 4. (*) 산술 연산자를 이용하는 방법
// 문자열 타입 -> 숫자 타입
"0" * 1; // 0
"10.53" * 1; // 10.53
// 불리언 타입 -> 숫자 타입
true * 1; // 1
```

## 9.4 단축 평가

### 9.4.1 논리 연산자를 사용한 단축 평가

- 논리합(||) 또는 논리곱(&&) 연산자 표현식은 2개 피연산자 중 한쪽으로 평가된다.
  → 논리 연산의 결과를 결정하는 피연사자를 타입 변환하지 않고 그대로 반환한다.

```jsx
// 논리합(||) 연산자
"Cat" || "Dog"; // 'Cat'
false || "Dog"; // 'Dog'
"Cat" || false; // 'Cat'

// 논리곱(&&) 연산자
"Cat" && "Dog"; // 'Dog'
false && "Dog"; // false
"Cat" && false; // false
```

조건이 Truthy 값 일때 논리곱(&&) 연산자 표현식으로 if문 대체할 수 있다.

```jsx
var done = true;
var message = "";

// 주어진 조건이 true일 때 -> message에 "완료"를 할당
if (done) message = "완료";

// if 문은 단축 평가로 대체 가능하다.
// done true라면 message에 '완료'를 할당
message = done && "완료";
console.log(message); // 완료
```

조건이 Falsy 값일 때 논리합(||) 연산자 표현식으로 if 문 대체가 가능하다.

```jsx
var done = false;
var message = "";

// 주어진 조건이 false일 때
if (!done) message = "미완료";

// if 문은 단축 평가로 대체 가능하다.
// done이 false라면 message에 '미완료'를 할당

message = done || "미완료"; // done이 false이기 때문에 "미완료"를 출력
console.log(message); // 미완료
```

### 9.4.2 옵셔널 체이닝 연산자

옵셔널 체이닝 연산자 `?.` 는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

```jsx
var elem = null;

var value = elem?.value; // 변수 elem이 null이나 undefined인가?
console.log(value); // undefined
```

→ 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용하다.

### 9.4.3 null 병합 연산자

null 병합 연산자 `??` 는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다. → 변수의 기본값을 설정할 때 유용하다.

```jsx
var foo = null ?? "default string";
console.log(foo); // "default string"
```

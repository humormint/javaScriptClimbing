# 12장 함수

## 함수란?

입력을 받아 출력을 내보내는 일련의 과정으로 프로그래밍 언어에서 함수는 일련의 과정을 문으로 구현하고 코드 블록으로 감싸서 하는의 실행단위로 정의한 것이다.

```jsx
// f(x, y) = x + y
function add(x, y) {
  return x + y;
}

// f(2, 5) = 7
add(2, 5); // 7
```

`add` : 함수 이름

`(x, y)` : 매개 변수(parameter)

`(2, 5)` : 인수(argument)

`x + y` : 반환값(return value)

함수 정의

```jsx
function add(x, y) {
  return x + y;
}
```

```jsx
// 함수 호출
var result = add(2, 5);

// 함수 add에 인수 2, 5를 전달하면서 호출하면반환값 7을 반환한다.
consol.elog(result); // 7
```

## 12.2 함수를 사용하는 이유

1. 코드의 재사용이 용이하다.
2. 코드의 중복을 억제한다 → 유지보수의 편의성을 높이고 실수를 줄여 코드의 신뢰성을 높인다.
3. 함수에 이름(식별자)을 붙일 수 있다. → 코드의 가독성을 향상 시킨다.

## 12.3 함수 리터럴

객체를 객체 리터럴로 생성하는 것처럼 함수도 함수 리터럴로 생성할 수 있다.

```jsx
// 변수에 함수 리터럴을 할당

**var f** = function add(x, y) {
return x = y;
};
```

→ 함수는 객체이지만 일반 객체는 홀출할 수 없고 함수는 호출할 수 있다. 그리고 일반 객체에는 없는 ㅎ마수 객체만의 고유한 프로퍼티를 갖는다.

## 12.4 함수 정의

함수 선언문

```jsx
function add(x, y) {
  return x + y;
}
```

함수 표현식

```jsx
var add = function (x, y) {
  return x + y;
};
```

Function 생성자 함수

```jsx
var add = new Function("x", "y", "return x + y");
```

화살표 함수

```jsx
var add = (x, y) => x + y;
```

### 12.4.1 함수 선언문

```jsx
//함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 참조
//console.dir은 console.log 와 달리 함수 객체의 프로퍼티까지 출력한다.

consol.dir(add); // f add(x,y)

// 함수 호출
console.log(add(2, 5)); // 7
```

→ 함수 리터럴은 함수 이름을 생략할 수 있으나 함수 선언문은 함수 이름을 생략할 수 없다.

ex)

```jsx
function (x, y) { // 함수이름을 생략했기 때문에 에러가 발생한다.
return x + y;
}
// SyntaxError
```

→ 함수 선언문은 표현식이 아닌 문이다. 따라서 크롬 개발자 도구 콘솔에서 함수 선언문을 실행하면 undefined가 출력된다.

```jsx
// 기명 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석된다.
// 함수 선언문에서는 함수 이름을 생략할 수 없다.
function foo() {
  console.log("foo");
}
foo(); // foo

// 함수 리터럴을 피연산자로 사용하면 하수 선언문이 아니라 함수 리터럴 표현식으로 해석된다.
// 함수 리터럴에서는 함수 이름을 생략할 수 있다.
(function bar() {
  console.log("bar");
});
bar();
```

그룹 연산자 `()` 내에 있는 함수리터럴(bar)은 함수 선언문으로 해석되지 않고 험수 리터럴 표현식으로 해석된다.

자바스크립트 엔진은 별도로 생성된 함수 객체를 가리키는 식별자가 필요하다. 따라서 자바스크립트 엔진은 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체를 할당한다.

함수는 함수 이름으로 호출 하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다.

ex)

```jsx
var add = function add(x, y) {
  return x + y;
};
console.log(add(2, 5)); // 7
```

`var add` 에서 `add` 는 식별자이고 `function add` 에서 `add` 는 함수 이름이다.

### 12.4.2 함수 표현식

값의 성질을 갖는 객체를 일급 객체라 한다. 자바스크립트 함수는 일급 객체다.

→ 함수를 값처럼 자유롭게 사용할 수 있다.

```jsx
// 기명 함수 표현식

var add = function foo(x, y) {
  return x + y;
};
// 함수 객체를 가리키는 식별자로 호출
console.log(add(2, 5)); //7

// 함수 이름으로 호출하면 에러가 발생한다.
// 함수 이름은 함수 몸체 내부에서만 유효한 식별자이다.
```

### 12.4.3 함수 생성 시점과 함수 호이스팅

```jsx
// 함수 참조
console.dir(add); // f add(x, y)
console.dir(sub); // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // typeError

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x - y;
};
```

→ 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성시점이 다르기 때문에 함수 표현식으로 정의한 함수는 함수 표현식 이전에 호출할 수 없다.

→ 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 함수 호이스팅이라고 한다.

but, 함수 표현식은 변수에 할당되는 값이 함수 리터럴인 문이다. 따라서 변수할당문의 값은 할당문이 실행되는 시점, 즉 런타임에 평가되므로 함수 표현식의 함수 리터럴도 할당문이 실행되는 시점에서 평가되어 함수 객체가 된다. → 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다.

### 12.4.4 Function 생성자 함수

```jsx
var add = new Function("x", "y", "return x + y");
console.log(add(2, 5)); // 7
```

### 12.4.5 화살표 함수

→ ES6 에서 도입된 화살표함수는 function 키워드 대신 화살표를 이용해 간단하게 함수를 선언할 수 있다.

```jsx
// 화살표 함수
const add = (x, y) => x + y;
console.log(add(2, 5)); // 7
```

## 함수 호출

### 매개변수와 인수

함수를 실행하기 위해 필요한 값을 함수 외부에서 함수 내부로 전달할 필요가 있는 경우, 매개변수를 통해 인수를 전달한다. 인수는 값으로 평가될 수 있는 표현식이어야 한다.

```jsx
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 호출
// 인수 1과 2가 매개변수 x와 y에 순서대로 할당되고 함수 몸체의 문들이 실행된다.
var result = add(1, 2);
```

```jsx
function add(x, y) {
  console.log(x, y); // 2 5
  return x + y;
}

add(2, 5);

// add 함수의 매개변수 x, y는 함수 몸체 내부에서만 참조할 수 있다.
console.log(x, y); // ReferenceError: x is not defined
```

```jsx
function add(x, y) {
  return x + y;
}
console.log(add(2)); // NaN
```

→ x에는 인수 2가 전달되지만, 매개변수 y에는 전달할 인수가 없다.

→ x + y는 2 + undefined와 같으므로 NaN이 반환된다.

매개변수보다 인수가 더 많으면 초과된 인수는 무시된다

```jsx
function add(x, y) {
  return x + y;
}
console.log(add(2, 5, 10)); // 7
```

→인수 10은 무시된다.

### 12.5.2 인수 확인

```jsx
function add(x, y) {
  return x + y;
}
console.log(add(2)); // NaN
console.log(add("a", "b")); // 'ab'
```

→ 문법상 아무런 문제가 없기 때문에 위와 같이 실행되는 이유

1. 자바스크립트 함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않는다 → 인수 2개가 필요하지만 1개만 있어도 함수를 실행함
2. 자바스크립트는 동적 타입 언어이기 때문에 매개변수 타입을 사전에 지정할 수 없다.

매개 변수가 많은것은 함수가 여러가지 일을 하는 것이기 때문에 바람직하지 않고 함수는 한 가지 일만 해야하며 가급적 작게 만들어야 한다.

### 12.5.4 반환문

함수는 `return` 키워드와 표현식(반환값)으로 이뤄진 반환문을 사용해 실행 결과를 함수 외부로 반환할 수 있다.

```jsx
function multiply(x, y) {
  return x * y; // 반환문
}

// 함수 호출은 반환값으로 평가된다.
var result = multiply(3, 5);
console.log(result); // 15
```

→ `multiply` 함수는 두 개의 인수를 전달받아 곱한 결과값을 `return` 키워드를 사용해 반환한다. 함수는 `return` 키워드를 사용해 자바스크립트에서 사용 가능한 모든 값을 반환 할 수 있다. 함수 호출은 표현식이다.

반환문의 역할

1. 함수의 실행을 중단하고 함수 몸체를 빠져 나간다. → 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시된다.
2. 반환문은 return 키워드 뒤에 오는 표현식을 평가해 반환한다.

```jsx
function multiply(x, y) {
  return x * y; // 반환문
  // 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시된다.
  console.log("실행되지 않는다.");
}

// 함수 호출은 반환값으로 평가된다.
var result = multiply(3, 5);
console.log(result); // 15
```

반환문은 생략할 수 있으며 생략하면 암묵적으로 undefined가 반환된다.

```jsx
function foo() {
  // 반환문을 생략하면 암묵적으로 undefined가 반환된다.
}

console.log(foo()); // undefined
```

## 12.6 참조에 의한 전달과 외부 상태의 변경

```jsx
// 매개 변수 primitive는 원시 값을 전달 받고, 매개변수 obj는 객체를 전달 받는다.
function changeVa(primitive, obj) {
  primitive += 100;
  obj.name = "Kim";
}

// 외부 상태
var num = 100;
var person = { name: "Lee" };

console.log(num); // 100
console.log(person); // {name: "Lee"}

// 원시 값은 값 자체가 복사되어 전달되고 객체는 참조 값이 복사되어 전달된다.
changeVal(num, person);

// 원시 값은 원본이 훼손되지 않는다.
console.log(num); // 100

// 객체는 원본이 훼손된다.
console.log(person); // {name: "Kim"}
```

→ `changeVal` 함수는 매개변수를 통해 전달 받은 원시 타입 인수와 객체 타입 인수를 함수 몸체에서 변경한다.

재할당을 통해 할당된 원시 값을 새로운 원시값으로 교체했고, 객체 타입 인수를 전달 받은 매개변수 obj의 경우, 객체는 변경 가능한 값이므로 직접 변경할 수 있기 때문에 재할당 없이 직접 할당된 객체를 변경했다.

## 12.7 다양한 함수의 형태

### 12.7.2 재귀함수

→ 재귀 함수는 자기 자신을 호출하는 함수를 말한다.

ex) 10부터 0까지 출력하는 함수

```jsx
function countdown(n) {
  for (var i = n; i >= 0; i--) console.log(i);
}

console.log(10);
```

→ 반복문 없이 재귀 함수를 사용하여 구현할 수 있다

```jsx
function countdown(n) {
  if (n < 0) return;
  console.log(n);
  countdown(n - 1); // 재귀 호출
}

console.log(10);
```

재귀함수를 이용하면 팩토리얼을 간단히 구현할 수 있다.

```jsx
function factorial(n) {
  //탈출조건: n이 1 이하일 때 재귀 호출을 멈춘다.
  if (n <= 1) return 1;
  // 재귀 호출
  return n * factorial(n - 1);
}
console.log(factorial(5)); //120
```

### 12.7.3 중첩함수

```jsx
function outer() {
  var x = 1;

  // 중첩함수
  function inner() {
    var y = 2;
    // 외부 함수의 변수를 참조할 수 있다.
    console.log(x + y); // 3
  }
  inner();
}
outer();
```

### 12.7.4 콜백함수

```jsx
// n만큼 어떤 일을 반복한다.
function repeat(n) {
  // i를 출력
  for (var i = 0; i < n; i++) console.log(i);
}
repeat(5); // 0 1 2 3 4
```

→ `repeat` 함수는 매개변수를 통해 전달 받은 숫자 만큼 반복하여 `console.log(i)` 를 호출한다.

→ `repeat` 함수는 `console.log(i)` 에 강하게 의존하고 있어 다른 일을 할 수 없다. 다른 일을 부여하기 위해서는 함수를 새롭게 정의해야 한다.

```jsx
// n만큼 어떤 일을 반복한다.
function repeat1(n) {
  // i를 출력
  for (var i = 0; i < n; i++) console.log(i);
}
repeat1(5); // 0 1 2 3 4

// n만큼 어떤 일을 반복한다. (0부터 4까지 숫자중 홀수만 출력하고 싶을 때)
function repeat2(n) {
  for (var i = 0; i < n; i++) {
    // i가 홀수일 때만 출력한다.
    if (i % 2) console.log(i);
  }
}
repeat2(5); // 1 3
```

→ 함수의 합성으로 해결할 수 있다.

→ 함수의 공통된 로직은 미리 정의해 두고, 변경되는 로직은 추상화해서 함수 외부에서 내부로 전달하는 것이다.

```jsx
// 외부에서 전달받은 f를 n만큼 반복 호출한다.
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i); //i를 전달하면서 f를 호출
  }
}
var logAll = function (i) {
  console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) {
  if (i % 2) console.log(i);
};
// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1 3
```

→ `repeat` 함수는 변경되는 일을 함수 f로 추상화 했고 이를 외부에서 전달 받는다.

→ 이처럼 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 콜백함수라고 하며, 매개변수를 통해 함수의 외부에서 콜백함수를 전달받은 함수를 고차 함수라고 한다.

→ 고차함수는 콜백함수를 자신의 일부분으로 합성한다. → 콜백함수는 고차함수에 의해 호출되며 이때 고차함수는 필요에 따라 콜백함수에 인수를 전달할 수 있다.

→ 콜백함수는 비동기 처리, 배열 고차함수에서도 중요하게 사용된다.

### 12.7.5 순수함수와 비순수 함수

```jsx
var count = 0; // 현재 카운트를 나타내는 상태

// 순수함수 increase는 동일한 인수가 전달되면 언제나 동일한 값을 반환한다.
function increase(n) {
  return ++n;
}

// 순수 함수가  반환한 결과값을 변수에 재할당해서 상태를 변경
count = increase(count);
console.log(count); // 1

count = increase(count);
console.log(count); // 2
```

```jsx
var count = 0; // 현재 카운트를 나타내는 상태

// 비순수 함수
function increase() {
  return ++count;
}

// 비순수함수는 외부상태(count)를 변경하므로 상태 변화를 추적하기 어려워진다.
count = increase();
console.log(count); // 1

count = increase();
console.log(count); // 2
```

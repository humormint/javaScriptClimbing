# 10장 객체 리터럴

## 10.1 객체란?

→ 자바스크립트는 객체 기반 프로그래밍 언어이며, 자바스크립트를 구성하는 거의 모든 것이 객체다. 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식) 등은 모두 객체다.

원시값은 하나의 값만 나타내어 변경 불가능한 값이지만, 객체는 다양한 타입의 값을 하나의 단위로 구성한 복합적인 자료구조이기 때문에 변경가능한 값이다.

객체는 프로퍼티의 합으로 이루어져 있으며 프로퍼티는 키(key)와 값(value)로 이루어져 있다.

ex)

```jsx
var person = {
  name: "Lee", // 프로퍼티
  age: 20, // 프로퍼티
};
```

`name` , `age` → 프로퍼티 키

`'Lee'` , `20` → 프로퍼티 값

프로퍼티 값이 함수일 경우, 일반 함수와 구분하기 위해서 메서드(method)라 부른다.

ex)

```jsx
var counter = {
num: 0, // 프로퍼티
**increase: function () { // 메서드
this.num++;
}**
};
```

프로퍼티: 객체의 상태를 나타내는 값(data)

메서드: 프로퍼티를 참조하고 조작할 수 있는 동작(behavior)

## 10.2 객체 리터럴에 의한 객체 생성

C++나 자바 같은 클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성한다.

인스턴스: 클래스에 의해 생성되어 메모리에 저장된 실체, 객체는 클래스와 인스턴스를 포함한 개념이다. 클래스는 인스턴스를 생성하기 위한 템프릿 역할을 하며, 인스턴스는 객체가 메모리에 저장되어 실제로 존재하는 것에 초점을 맞춘다.

객체리터럴은 객체 생성 방법 중에서 가장 일반적이고 간단한 방법이다. 리터럴(literal)은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용하여 값을 생성하는 표기법이다.

→ 객체 리터럴은 중괄호 `({...})` 내에 0 개 이상의 프로퍼티이다.

```jsx
var person = {
  name: "Lee",
  sayHello: function () {
    console.log(`Hello My name is ${this.name}'.`); // this는 person
  },
};

console.log(typeof person); // object
console.log(person); // { name: 'Lee', sayHello: [Function: sayHello] }
```

## 10.3 프로퍼티

→ 객체는 프로퍼티 집합이며, 프로퍼티는 키와 값으로 구성된다.

```jsx
var person = {
  // 프로퍼티 키는 name, 프로퍼티 값은 'Lee'
  name: "Lee",
  // 프로퍼티 키는 age, 프로퍼티 값은 20
  age: 20,
};
```

프로퍼티는 `쉼표(,)` 로 구분한다.

프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름으로 식별자 역할을 한다. 프로퍼티 키는 일반적으로 문자열을 사용한다. 따라서 식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용해야한다.

→ 식별자 네이밍 규칙을 따르지 않는 프로퍼티 키를 사용하면 번거로운 일이 발생한다. 다음 예제를 살펴보자

ex)

```jsx
var person = {
  firstName: "Ji-hoon", // 식별자 네이밍 규칙을 준사하는 프로퍼티 키
  "last-name": "Lee", // 식별자 네이밍 규칙을 준수하지 않는 프로퍼티 키
};

console.log(person); // {firstName: "Ji-hoon", last-name: "Lee"}
```

`last-name` 은 식별자 네이밍 규칙을 준수하지 않는다. → 따라서 따옴표를 생락할 수 없다. 따옴표를 생략할 경우 (-) 연산자가 있는 표현식을 해석하기 때문이다.

```jsx
var foo = {
  "": "", // 빈 문자열도 프로퍼티 키로 사용할 수 있다.
};

console.log(foo); // {"": ""}
```

프로퍼티 키에 문자열이나 심벌 값 이외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다.

따라서 프로퍼티 키로 숫자 리터럴을 사용하면 따옴표는 붙지 않지만 내부적으로는 문자열로 변환된다.

```jsx
var foo = {
  0: 1,
  1: 2,
  2: 3,
};

console.log(foo); // {0: 1, 1: 2, 2: 3}
```

이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어 쓴다.

```jsx
var foo = {
  name: "Lee",
  name: "Kim",
};

console.log(foo); // {name: "Kim"}
```

## 10.4 메서드

프로퍼티 값이 함수일 경우 일반함수와 구분하기 위해 메서드라 부른다.

```jsx
var circle = {
  radius: 5, // 프로퍼티

  // 원의 지름
  getDiameter: function () {
    // 메서드
    return 2 * this.radius; // this는 circle을 가리킨다.
  },
};
console.log(circle.getDiameter()); // 10
```

## 10.5 프로퍼티 접근

```jsx
var person = {
  name: "Lee",
};

// 마침표 표기법에 의한 프로퍼티 접근
console.log(person.name); // Lee

// 대괄호 표기법에 의한 프로퍼티 접근
console.log(person["name"]); // Lee
```

→ 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열 이어야한다.

→ 따옴표로 감싸지 않으면 undefined를 반환한다.(값이 존재하지 않기 때문이다.)

## 10.6 프로퍼티 값 갱신

이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.

```jsx
var person = {
  name: "Lee",
};

// person 객체에 name 프로퍼티가 존재하므로 name 프로퍼티의 값이 갱신된다.
person.name = "Kim";

console.log(person); // {name: "Kim"}
```

## 10.7 프로퍼티 동적 생성

→ 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적을 생성되어 추가되고 해당 프로퍼티 값이 할당된다.

```jsx
var person = {
  name: "Lee",
};
// person 객체에는 age 프로퍼티가 존재하지 않는다.
// 따라서 person 객체에 age 프로퍼티가 동적으로 생성되고 값이 할당된다.

person.age = 20;

console.log(person); // {name: "Lee", age: 20}
```

## 10.8 프로퍼티 삭제

delete 연산자는 객체의 프로퍼티를 삭제한다.

```jsx
var person = {
  name: "Lee",
};

// 프로퍼티 동적 생성
person.age = 20;

delete person.age; // 해당 프로퍼티 삭제 가능
```

## 10.9 ES6에서 추가된 객체 리터럴의 확장 기능

### 10.9.1 프로퍼티 축약 표현

ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티를 생략 할 수 있다.

```jsx
// ES6
let x = 1,
  y = 2;

// 프로퍼티 축약 표현
const obj = { x, y };

console.log(obj); // {x: 1, y: 2}
```

### 10.9.2 계산된 프로퍼티 이름

문자열 또는 문자열로 타입 변환 할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있다. 이 때, 프로퍼티 키로 사용할 표현식을 대괄호로 묶어야 한다.

### 10.9.3 메서드 축약 표현

```jsx
// ES5
var obj = {
name: 'Lee',
**sayHi: function()** {
console.log('Hi!' + this .name);
}
};

obj.sayHi(); // Hi! Lee
```

```jsx
// ES6
const obj = {
name: 'Lee',

//메서드 축약 표현
**sayHi()** {
console.log('Hi!' + this .name);
}
};

obj.sayHi(); // Hi! Lee
```

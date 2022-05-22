# 25장 클래스

<br>

## 25.1 클래스는 프로토 타입의 `문법적 설탕`인가 ?

ES5 → 클래스 없이도 `생성자 함수`와 `프로토타입`을 통해 객체 지향 언어의 상속 구현이 가능!

ES6 → `클래스`는 프로그래머가 더욱 빠르게 학습할 수 있는 새로운 객체 생성 매커니즘을 제시!

→ 내부적인 동작은 동일하지만 더 보기 좋고 편리하게 개선된, 문법적 설탕(Syntactic sugar)이라고 볼 수도 있지만, 엄밀하게 말하면 `클래스`가 생성자함수를 완전히 대체한다고 볼 수 는 없기 때문에 단순히 문법적 설탕이라고 보기보다는 `새로운 객체 생성 매커니즘`으로 보는 것이 합당하다.

<br>

### 클래스와 생성자 함수의 차이점

- 클래스는 `new` 연산자 없이 호출하면 에러 발생, but 생성자 함수는 `new` 연산자 없이 호출하면 일반함수로서 호출됨
- 클래스는 상속을 지원하는 `extends`와 `super` 키워드를 제공하지만 생성자 함수는 `extends`와 `super`키워드를 지원하지 X

<br>

→ 클래스는 기존 객체 생성 메커니즘과 기능상 차이는 크게(완벽하게 같지는X) 없고 약간 더 보기쉽게 표현해준다.

(`함수`, `prototype`을 이용한 `상속기능`을 한번에 만들 수 있도록 도와주는 문법이다.)

<br>

## 25.2 클래스의 정의

클래스란 객체를 생산하는 틀이며 `class키워드` + `클래스 명(첫글자 대문자)` + `중괄호`로 선언한다.

```jsx
// 클래스 선언문

class Person {}
```

<br>

### 클래스와 생성자함수의 정의 방식 비교

생성자 함수로 정의

```jsx
// 생성자 함수
function Robot(name) {
  this.name = name;
}

Robot.prototype.sayYourName = function () { // 프로토 타입 메서드
  console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
};

const bot1 = new Robot('지훈');
console.log(bot1.sayYourName()); // 삐리비리. 제 이름은 지훈입니다. 주인님.
```
<br>

클래스로 정의

```jsx
class Robot {

// 생성자
    constructor(name) { 
        this.name = name;
    }

    sayYourName() { // 프로토 타입 메서드
        console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
    }
}

  const bot1 = new Robot('지훈')
  console.log(bot1.sayYourName()); // 삐리비리. 제 이름은 지훈입니다. 주인님.
```

→ 정의 방식은 형태적인 면에서 유사함

<br>

## 25.8 상속에 의한 클래스 확장

### 25.8.1 클래스 상속과 생성자 함수 상속

프로토타입 기반 상속 → 프로토타입 체인을 통해 `다른` 객체의 자산을 상속 받는 개념

but, 상속에 의한 클래스 확장 → `기존` 클래스를 상속받아 새로운 클래스를 확장하여 정의

```jsx
class Animal {
  constructor(age, weight) {
    this.age = age;
    this.weight = weight;
  }
  eat() {
    return "먹는다";
  }
  move() {
    return "움직인다";
  }
}

// 상속을 통해 Animal 클래스를 확장한 Bird 클래스 (동물의 공통 특성은 상속받고 fly속성 추가)
class Bird extends Animal {
  fly() {
    return "난다";
  }
}

const bird = new Bird(1, 5);
console.log(bird); // Bird { age: 1, weight: 5 }

// bird에 함수가 있는지 확인
console.log(bird.eat()); // 먹는다
console.log(bird.move()); // 움직인다
console.log(bird.fly()); // 난다
```

→ 동물의 공통속성 (나이, 무게, 먹는다, 움직인다)은 그대로 상속 받고 새의 고유한 속성 (난다) 추가할 수 있다.

→ 상속에 의한 클래스 확장은 `코드 재사용` 관점에서 매우 유용하다

<br>

### 25.8.2 extends 키워드

`extends` → 기존에 있던 class의 내용을 `상속받는 class`를 만들 수 있다.

```jsx
class 할아버지{
  constructor(name){
    this.성 = '채';
    this.이름 = name;
  }
}
```
<br>

할아버지 class를 상속받는 아버지 class

```jsx
class 할아버지 {
  constructor(name) {
    this.성 = "채";
    this.이름 = name;
  }
}

class 아버지 extends 할아버지 {}

const 아버지1 = new 아버지('영준');

console.log(아버지1); //아버지 { '성': '채', '이름': '영준' }
```

→ 할아버지라는 class를 그대로 상속받은 `아버지라는 class가 생성`

<br>

아버지 class에 `this`로 프로퍼티 추가

```jsx
class 할아버지{
  constructor(name){
    this.성 = '채';
    this.이름 = name;
  }
}

class 아버지 extends 할아버지{
  constructor(){
    this.나이 = 50;
  }
}

const 아버지1 = new 아버지()
console.log(아버지1);
```

<details>
<summary>console.log(아버지1)</summary>
<div markdown="1">

 ```jsx
     // ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor
    // super를 써야함
```

</div>
</details>
  
<br>

### 25.8.5 super 키워드

`super()`사용

```jsx
class 할아버지 {
  constructor(name) {
    this.성 = "채";
    this.이름 = name;
  }
}

class 아버지 extends 할아버지 {
  constructor() {
    super();
    this.나이 = 50;
  }
}

const 아버지1 = new 아버지();
console.log(아버지1); // 아버지 { '성': '채', '이름': undefined, '나이': 50 }
```

`super()`

→ extends로 상속중인 부모 class의 constructor()

→ 할아버지 class의 constructor()

→ 에러없이 `this`로 프로퍼티 추가 가능

<br>

아버지 class에 파라미터 사용하기

```jsx
class 할아버지 {
  constructor(name) {
    this.성 = "채";
    this.이름 = name;
  }
}

class 아버지 extends 할아버지 {
  constructor(name) {
    super(name);
    this.나이 = 50;
  }
}

const 아버지1 = new 아버지('영준');
console.log(아버지1); // 아버지 { '성': '채', '이름': '영준', '나이': 50 }
```
<br>

**super 사용시 주의할 점**

- 만약 파생 클래스(자식 클래스)에 생성자 함수를 사용하고 싶다면 반드시 super 함수를 사용해야합니다.
- 파생클래스에 생성자 함수가 없다면 super 함수가 자동으로 호출되어 부모 클래스의 프로퍼티를 상속 받게 합니다.
- 생성자 함수에서 this 값을 사용할 경우 `super` 함수는 반드시 `this 보다 먼저 실행`되어야 합니다.
- 파생 클래스(자식 클래스)가 아닌 클래스에서 사용하려고 해도 에러가 발생합니다.

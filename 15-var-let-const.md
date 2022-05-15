## var, let, const 선언, 할당, 범위

|  | var | let | const |
| --- | --- | --- | --- |
| 재선언 | O | X | X |
| 재할당 | O | O | X |
| 스코프 |  function | 블록레벨 | 블록레벨 |

블록레벨 스코프: 모든 코드블록(함수, if 문, for문 ...)을 지역 스코프로 인정하는 스코프

<br>

### 15.1 var 키워드로 선언한 변수의 문제점

`var`

→ 재선언 O, 재할당 O, 범위 function

<br>

### 15.1.1 변수 재선언(중복 선언) 허용

```jsx
  var 이름 = 'kim'; 
  var 이름 = 'park'
console.log(이름) // park // 재선언 가능
```
<br>

변수 재할당도 가능

```jsx
  var 이름 = 'kim'; 
  var 이름 = 'park'
	이름 = 'chae' // 재할당 
console.log(이름) // chae
```

→ `var 이름` →  `이름 = 'kim'` , `이름 = 'park` → 할당

→  `var 이름 = 'kim'` 해놓고 `이름 = 'chae'` → 재할당 가능

<br>

### 15.1.2 함수 레벨 스코프

var로 선언한 변수는 함수의 코드 블록만을 지역 스코프로 인정한다.

<br>

→ function안에서만 존재함

```jsx
function 함수() {
  var 이름 = 'kim'; // function안에서만 존재
  console.log(이름);  // kim
}
console.log(이름); // ReferenceError: 이름 is not defined
함수()
```

→ 함수 외부에서 var로 선언한 변수는 코드 블록 내에서 선언해도 모두 전역 변수가 된다.

```jsx
var 이름 = "지훈";

if (true) {
  // 이름 -> 전역 변수 
  var 이름 = "호준님"; // 재선언 
  // 의도치 않게 변수값이 변경 되는 부작용이 발생한다. (지훈 -> 호준님)
}
console.log(이름); // 호준님
```

<br>

## 15.2 let 키워드

`let`

→ 재선언 X, 재할당 O, 범위 : 블록 레벨

```jsx
let 나이 = 20;
let 나이 = 30; // error // 재선언 불가
```

```jsx
let 이름 ='지훈'

if(true){
let 이름 = '영웅'
let 성 ='채'
console.log(이름) // 영웅
}
console.log(이름); // 지훈
console.log(성); // ReferenceError: 성 is not defined
```

let 키워드로 선언한 변수는 모든 코드블록(함수, if문, for문 ...)을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.

<br>

## 15.3 const 키워드

`const`

→ 재선언 X, 재할당X, 범위 : 블록 레벨

→ 변하지 않는 값(상수)

<br>

### 15.3.4 const 키워드와 객체

const 변수는 원시값을 할당한 경우 값을 변경할 수 없지만 const 변수에 객체를 할당한 경우 값을 변경할 수 있다.

```jsx
const 사람 = {이름 : 'kim'}
사람.이름 = 'park'
console.log(사람) // {이름 : park}
```

→ const 키워드는 재할당을 금지할 뿐 “불변"을 의미하지 않는다.

<br>

## 15.4 var vs. let vs. const

변수 선언은 기본적으로 const를 사용하고 let은 재할당이 가능한 경우에 한정해서 사용하는 것이 좋다. 

- ES6 사용 → var을 사용하지 않는다.
- 재할당이 필요한 경우에 한해 let 사용, 이때 변수의 스코프는 최대한 좁게!
# 8장 제어문

control flow statement

제어문은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행함(반복문)

## 8.1 블록문

블록문 → 문을 중괄호로 묶은 것, 제어문이나 함수를 정의할 때 사용하는 것이 일반적이다.

```jsx
// 블록문
{
  var foo = 10;
}

// 제어문
var x = 1;
if (x < 10) {
  x++;
}

// 함수 선언문
function sum(a, b) {
  return a + b;
}
```

## 8.2 조건문

### 8.2.1 if... else 문

→ 조건식의 평가 결과(불리언 값)에 따라 실행할 코드 블록을 결정한다.

조건식 결과가 true일 경우 if 문의 코드 블록이 실행되고, false일 경우 else문의 코드 블록이 실행된다.

else if문과 else문은 옵션이다. 또한, if문과 else문은 2번 이상 쓸 수 없지만 else if 문은 여러 번 쓸 수 있다.

```jsx
var num = 2;
var kind;

// if 문
if (num > 0) {
  kind = "양수"; // 음수를 구별할 수 없다
}
console.log(kind); // 양수 (2 > 0이기 때문에)

// if else 문
if (num > 0) {
  kind = "양수";
} else {
  kind = "음수"; // 0은 음수가 아니다
}
console.log(kind); // 양수

// if ...else if 문
if (num > 0) {
  kind = "양수";
} else if (num < 0) {
  kind = "음수";
} else {
  kind = "영";
}
console.log(kind); // 양수
```

### 8.2.2 switch 문

→ 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 가지는 case문으로 실행 흐름을 옮긴다. switch 의 표현식과 일치하는 case문이 없다면 실행 순서는 default 문으로 이동한다. switch 문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다. 따라서 논리적 참, 거짓 보다는 다양한 case에 따라 실행할 코드 블록을 결정할 때 사용한다.

```jsx
// 월을 영어로 변환한다 (11 -> 'November')
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = "Jan";
  case 2:
    monthName = "Feb";
  case 3:
    monthName = "Mar";
  case 4:
    monthName = "Apr";
  case 5:
    monthName = "May";
  case 6:
    monthName = "Jun";
  case 7:
    monthName = "Jul";
  case 8:
    monthName = "Aug";
  case 9:
    monthName = "Sep";
  case 10:
    monthName = "Oct";
  case 11:
    monthName = "Nov";
  case 12:
    monthName = "Dec";
  default:
    monthName = "Invalid month";
}
console.log(monthName); // Invalid month
```

→ 11 일 경우 `Nov` 를 출력해야 하지만 `Invalid month` 가 출력된다. switch 문의 표현식의 평가 결과와 일치하는 case문으로 실행흐름을 이동하여 시행한 것은 맞지만 이후에, switch 문을 탈출하지 않고 switch 문이 끝날때까지 이후의 모든 case 문과 defualt 문을 실행했기 때문이다. → 폴스루

→ `monthName` 변수에 `Nov`가 할당된 후, switch 문을 탈출하지 않고 이후 `Dec`가 재할당되고 마지막으로 `Invalid month`가 재할당된 것이다.

→ 이를 해결하기 위해 `break` 문을 사용한다. `break` 문은 코드 블록에서 탈출하는 역할을 한다. 맨 마지막 `default` 문에는 `break` 문이 별도로 필요 없다.

```jsx
// 월을 영어로 변환한다 (11 -> 'November')
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = "Jan";
    break;
  case 2:
    monthName = "Feb";
    break;

  case 3:
    monthName = "Mar";
    break;
  case 4:
    monthName = "Apr";
    break;
  case 5:
    monthName = "May";
    break;
  case 6:
    monthName = "Jun";
    break;
  case 7:
    monthName = "Jul";
    break;
  case 8:
    monthName = "Aug";
    break;
  case 9:
    monthName = "Sep";
    break;
  case 10:
    monthName = "Oct";
    break;
  case 11:
    monthName = "Nov";
    break;
  case 12:
    monthName = "Dec";
    break;
  default:
    monthName = "Invalid month";
}
console.log(monthName); // Nov
```

## 8.3 반복문

### 8.3.1 for 문

→ 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행

```jsx
for (변수 선언문 또는 할당문; 조건식; 증감식) {
조건식이 참인 경우 반복 실행될 문;
}

// ex)
for (var i = 0; i <2; i++) {
console.log(i)
}
```

### 8.3.2 while 문

→ 주어진 조건식의 평가 결과가 참이면 코드블록을 계속해서 반복 실행한다.

→ for 문은 반복 횟수가 명확할때, while문은 반복횟수가 불명확할때 주로 사용한다.

→ while문은 조건문의 평가 결과가 거짓이 되면, 코드블록을 실햏하지 않고 종료한다.

```jsx
let count = 0;

// count가 3보다 작을때까지 코드블록을 계속 반복 실행

while (count < 3) {
  console.log(count); // 0 1 2
  count++;
}
```

### do... while 문

코드 블록을 한번은 무조건 실행하고 조건식을 평가한다. → 코드 블록은 무조건 한번 이상 실행된다.

```jsx
let count = 0;

// count가 3보다 작을때까지 코드블록을 계속 반복 실행
do {
  console.log(count); // 0 1 2
  count++;
} while (count < 3);
```

## 8.5 Continue 문

```jsx
→ 반복문의 코드블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
var string = "hello world";
var search = "l";
var count = 0;

// 문자열은 유사 배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l' 아니면 현 지점에서 실행을 중단하고 반복문으로 증감식으로 이동한다.
  if (string[i] !== search) continue; //
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count); // 3

// 참고로 String.prototype.march 메서드 사용해도 같은 동작을 한다.
const regexp = new RegExp(search, "g");
console.log(string.match(regexp).length); // 3
```

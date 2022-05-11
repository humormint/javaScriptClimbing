### 22.1 this 키워드

메서드(객체 내부의 함수)가 자신이 속한 객체의 프로퍼티를 참조하려면 자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.

this는 `자신이 속한 객체`나 `자신이 생성할 인스터스`(붕어빵)를 가리키는 자기 참조 변수다. this를 통해 자기가 속한 객체나 자신이 속한 객체나 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.

### 22.2 this 호출방식과 this 바인딩

함수 호출 방식

1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출

### 22.2.1 일반함수 호출

1) 기본적으로 일반함수로 호출된 this에는 전역객체가 바인딩된다. (중첩함수, 콜백함수 포함)

```jsx
 console.log(this) // window
        function 함수(){ 
            console.log(this) // window
        }
        함수() 
```

but, `strict mode` + 일반 함수 내에서 쓰면 `undefined` 출력

```jsx

        'use strict';  // 자바스크립트를 엄격하게 실행
        console.log(this) // undefined
        function 함수(){ 
            console.log(this) // undefined
        }
        함수() 
```

### 22.2.2 메서드 호출

2) this를 객체 내 함수(`메서드`)에서 쓰면 → 그 함수를 가지고 있는 객체를 뜻함(나를 포함하고 있는 객체)

```jsx
'use strict';  // 자바스크립트를 엄격하게 실행
        console.log(this)  

        **var 오브젝트 = {
            data : 'kim',
            함수 : function(){
                console.log(this) 
            }**
        }
        오브젝트.함수(); // {data: 'kim', 함수: ƒ}
```

`this` → `오브젝트`

객체 안에 객체를 넣으면

```jsx
'use strict';  // 자바스크립트를 엄격하게 실행
        console.log(this)  

        var 오브젝트 = {
            **data : {
            함수 : function(){
                console.log(this)
            }
        }**
    }
        오브젝트.data.함수(); // {함수: ƒ}
```

→ this는 그 함수를 가지고 있는 객체를 뜻함

3) 생성자 함수 안에서 쓰면 자신이 (미래에) 생성할 객체를 뜻한다.

생성자 함수에서 객체 생산하는 법

```jsx
var 어쩌구 = {}

        function 기계(){
        **this.이름 = 'kim'** // 새로 생성되는 오브젝트(instance)
        }
        var 오브젝트 = new 기계(); 
				// 콘솔창에 '오브젝트' 입력하면 -> 기계 {이름: 'kim'}
```

### 22.2.4 Function.prototype.apply/call/bind 메서드에 의한 간접 호출

`apply()`, `call()` → 함수를 호출하는 기능으로 함수를 호출하면 첫번째 인수로 전달한 특정 객체를 호출한 함수의 this에 바인딩 한다.

**call()**

`call()` 메서드의 인수에 this 로 사용할 값을 전달할 수 있다.

```jsx
var peter = {
  name : 'Peter Parker',
  sayName : function(){    
		console.log(this.name);
	}
}

var bruce = {
  name : 'Bruce Wayne',
}
peter.sayName.call(bruce); // Bruce Wayne

peter.sayName.call(peter); // Peter Parker

```

**apply()**

`apply()` 메서드의 인수에 this 로 사용할 값을 전달할 수 있으며, `배열`의 형태로도 전달할 수 있다.

```jsx
var peter = {
  name : 'Peter Parker',
  sayName : function(is, is2){    
		console.log(this.name+ ' is '+ is + ' or ' + is2);
	}
}

var bruce = {
  name : 'Bruce Wayne',
}

peter.sayName.apply(bruce, ['batman', 'richman']); // Bruce Wayne is batman or richman

peter.sayName.call(bruce, ['batman', 'richman']); // Bruce Wayne is batman,richman or undefined

```

**bind()**

`bind()` 는 this가 고정된 새로운 함수를 반환한다.

`peter.sayName()` → peter가 아니라 bruce가 출력, why? peter변수에  `sayName : sayName.bind(bruce)` 이기 때문에 bruce에 속박된다.

```jsx
function sayName(){
  console.log(this.name);
}

var bruce = {
  name: 'bruce',
  sayName : sayName
}

var peter = {
  name : 'peter',
  sayName : sayName.bind(bruce)
}

peter.sayName(); // bruce
bruce.sayName(); // bruce

```
this 키워드 

22.1 this 키워드

this 키워드는 함수 내에서 함수 호출 맥락(context)를 의미한다. 함수를 호출하면, 해당 함수 내부 코드에서 사용된 this는 호출한 함수를 소유하고 있는 객체로 바인딩된다. 함수를 선언할 때 사용된 this와 함수를 호출할 때 사용된 this는 다를 수 있다. 
함수를 선언할 때 사용된 this는 함수가 호출되는 방식에 따라 동적으로 결정된다.


22.1.1 함수 호출 방식과 this 바인딩

함수 호출 방식에 의해 this에 바인딩될 객체가 동적으로 결정된다. 함수 호출 방식은 다음과 같이 다양하다.

- 일반 함수 호출
- 메소드 호출
- 생성자 함수 호출
- Function.prototype.apply/call/bind 메소드에 의한 간접 호출


일반함수 호출 

일반 함수로 호출된 모든 함수(익명함수, 선언식 함수, 화살표 함수) 내부의 this에는 전역 객체가 바인딩된다. 브라우저 환경에서 전역 객체는 window 객체이다. 

```jsx
function foo() {
  console.log("foo's this: ", this); // window
}
foo();
```

메소드 호출

메소드 내부의 this에는 메소드를 호출한 객체, 즉 메소드를 프로퍼티로 가지고 있는 객체가 바인딩된다. 

```jsx
const person = {
  name: 'Lee',
  getName() {
    return this.name;
  }
};

console.log(person.getName()); // Lee
```

생성자 함수 호출

생성자 함수 내부의 this에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다. 

```jsx
function Circle(radius) {
  // 생성자 함수 내부의 this에 바인딩된 빈 객체를 가리킨다.
  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  };
}

// 반지름이 5인 Circle 객체를 생성

const circle = new Circle(5);

console.log(circle.getDiameter()); // 10
```

Function.prototype.apply/call/bind 메소드에 의한 간접 호출

apply, call, bind 메소드에 첫 번째 인수로 전달한 객체에 바인딩된다. 

```jsx
function getThisBinding() {
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

console.log(getThisBinding.call(thisArg)); // { a: 1 }
console.log(getThisBinding.apply(thisArg)); // { a: 1 }
console.log(getThisBinding.bind(thisArg)()); // { a: 1 }
```

22.1.2 화살표 함수와 this 바인딩

화살표 함수 내부에서 this를 참조하면 상위 스코프, 즉 상위(부모) 함수의 this를 가리킨다. 화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다. 

```jsx
// 화살표 함수
const foo = () => console.log(this);
foo(); // window
```

화살표 함수는 상위 스코프의 this를 그대로 활용할 수 있다. 

```jsx

const person = {
  name: 'Lee',
  sayHi() {
    // 화살표 함수
    const arrow = () => console.log(this);
    arrow();
  }
};

person.sayHi(); // { name: 'Lee', sayHi: f }
```

22.1.3 this 바인딩 우선순위

함수 호출 방식에 의해 this 바인딩 우선순위가 존재한다.

- new를 붙여서 호출(new 바인딩)
- call, apply, bind 메소드에 의한 간접 호출(명시적 바인딩)
- 메소드 호출(암시적 바인딩)
- 함수 호출(기본 바인딩)

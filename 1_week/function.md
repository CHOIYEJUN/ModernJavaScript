다양한 함수의 표현식 

#### 1. 즉시 실행 함수 (IIFE)

그게 뭐야?

```javascript
    (function() {
        console.log('hello');
    })();
````
함수 정의와 동시에 즉시 호출되는 함수를 즉시 실행 함수(IIFE, Immediately Invoked Function Expression)라고 한다.
즉시 실행 함수는 단 한 번만 호출되며 다시 호출할 수 없다.
이런식으로 사용한다.


왜 사용할까?

주로 한번만 실행되면 되는 함수에 사용한다. 

주로 초기화 코드 부분에 많이 사용하게 되는데, 

변수를 전역으로 선언하는 것을 피하기 위해 사용됩니다. 

```javascript
    (function() {
        var foo = 10; // 지역 변수
        var bar = 2; // 지역 변수
        console.log(foo * bar); // 20
    })();
    console.log(foo * bar); // ReferenceError: foo is not defined
````

#### 2. 재귀 함수 

    말그대로 자기 자신을 호출하는 함수를 재귀 함수라고 한다.
    재귀 함수는 반복문을 사용하지 않고도 반복적인 처리를 할 수 있다는 장점이 있다.
    하지만 재귀 함수는 호출 스택(Call Stack)을 사용하기 때문에 반복문에 비해 상대적으로 많은 메모리를 차지한다는 단점이 있다.
    따라서 재귀 함수는 호출 횟수가 적을 때나 스택의 메모리 한계를 넘지 않을 때 사용하는 것이 좋다.


#### 3. 중첩 함수

함수안에 함수가 있는 것. 

```javascript
        function outer() {
            var x = 1;
    
            // 중첩 함수
            function inner() {
                var y = 2;
                // 외부 함수의 변수를 참조할 수 있다.
                console.log(x + y); // 3
            }
    
            inner();
        }
    
        outer();
````


#### 4. 콜백 함수

>    함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 콜백 함수라고 한다. 
>
>    콜백 함수를 전달받은 함수는 이 콜백 함수를 필요에 따라 적절한 시점에 호출한다.
> 
>    콜백 함수를 전달받은 함수는 호출 시점을 결정하지 않고 단지 전달받은 콜백 함수를 호출할 뿐이다.
>
>    콜백 함수를 전달받은 함수는 호출 시점을 결정할 권한을 가지고 있다.
>
>    콜백 함수는 비동기 처리(Asynchronous processing)에 유용하게 사용된다.

```javascript
    function repeat(n, f) {
        for (var i = 0; i < n; i++) {
            f(i); // i를 전달하면서 f를 호출
        }
    }
    
    var logAll = function (i) {
        console.log(i);
    };
    
    // 반복할 때마다 서로 다른 동작을 하도록 콜백 함수를 전달한다.
    repeat(5, logAll); // 0 1 2 3 4
    
    var logOdds = function (i) {
        if (i % 2) console.log(i);
    };
    
    // 반복할 때마다 서로 다른 동작을 하도록 콜백 함수를 전달한다.
    repeat(5, logOdds); // 1 3
````




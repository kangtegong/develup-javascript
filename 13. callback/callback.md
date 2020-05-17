자 오늘은 중요한 이야기를 좀 할 겁니다. 
아니 뭐 맨날 중요하다고 해요 할 수도 있는데, 아 진짜 오늘은 진짜 중요하긴 해요.
바로 이 callback 함수인데요,

이 callback 함수는 처음에 배울 때는 좀 아리까리 할 수  있겠지만 리액트를 비롯한 웹 개발을 하시는 분들이라면 절대 
피할 수 없는 너무 중요한 이야기입니다.

callback에 대한 이야기를 하기 전에 
함수의 실행 순서에 대한 이야기를 좀 해야 할 거 같아요.

## 동기 vs 비동기

우리 이런 코드가 있다고 가정해봅시다.
그리고 여기서, 함수가 사람이라고 한 번 가정해봅시다.

function a() {
    console.log("a 실행");
}

function b() {
    console.log("b 실행");
}

function c() {
    console.log("c 실행");
}

function d() {
    console.log("d 실행");
}

a();
b();
c();
d();


이런 상황이라면, 마치 a b c가 일렬로 줄을 선 경우로도 빗댈 수 잇겠죠
그렇게
a가 먼저 처리되고
b가 먼저 처리되고
마지막으로 c가 처리되는 양상으로 이 코드가 실행된다고 할 수 잇겠죠.

이렇듯, 일반적인 상황이라면, 위에서 아래로
일반적으로는 a 다 끝났다는 전제 하에 b(); 실행될겁니다.
그쵸?

자 근데 여기서

근데 b가 엄청 오래 걸린다고 가정해봅시다.
예를 들어 b가 5초 뒤에 끝나는 함수라고 가정해보죠.

이런 경우 어떻게 될까?

function a() {
    console.log("a 실행");
}

function b() {
    console.log('오래 걸리는 b 실행');
}

function c() {
    console.log("c 실행");
}

a();
setTimeout(b, 3000);
c();

참고로 여기서 setTimeout은 
지정해준 특정 시간 이후에 어떤 함수나 코드를 실행하고 싶을 때 
쓰는 함수

첫번째 인자에는 실행하고 시킬 대상
두번째 인자에는 밀리세컨드 단위로 몇 밀리세컨드 뒤에 첫번째 인자를 실행시킬지를 써주면 됩니다.

어쨌든 이렇게 코드를 실행하게 되면
a- > c -> b 순으로 실행

즉,
a();가 바로 답을 내놓을 수 없는 상황이 아니라면, 천년만년 기다리고 있지 않는다
실행 순서가 보장이 안된다.

이는 자바스크립트의 특성 때문.

이런 특성을 처리 비동기 처리라고 함
그리고 반대는 동기처리

말하자면 비동기처리는 ~~이처럼 연속적으로 발생하는 이벤트를 담은 후 완료되는 순서대로 일을 처리하는 실행 순서가 확실하지 않는 것을 비동기적 방식이라 한다.
동기처리는 ~~이렇게 발생하는 하나의 이벤트가 모두 끝날 때까지 다른 이벤트를 처리하지 못하고 이벤트가 모두 완료 된 후 다음 이벤트를 동작하는 실행 순서가 확실한 것을 동기적 방식이라 부른다.

이 비동기처리가 무엇인지, 그리고 동기처리가 무엇인지는
자바스크립트 뿐만 아니라 프로그래밍에서 너무 중요한 개념이기 때문에
꼭 제대로 알아주시면 좋을 거 같아요.

예를 들어볼까요?
ajax 요청
페이스북 렌더링

여담이지만 자바스크립트에서 비동기처리가 발전한 이유 : 본질적으로는 싱글 쓰레드라서 그렇지만 좀 기능적인 면에서의 원인을 따져보자면
웹이라서 그렇다. 여러 자원들이 동일한 시간에 오지만은 않는다

---

function a(callback) {
    console.log("a 실행 시작");
    
    setTimeout(function() {
        console.log('Works!');
    }, 3000)
    callback();
}

function b() {
    console.log("이제서야 b 실행");
}

----

### 콜백함수

A callback function is a function passed into another function as an argument, 
which is then invoked inside the outer function to complete some kind of routine or action.

근데 순서 보장되어야 하는 경우
어떤 함수가 실행되기 위해서는 반드시 이전 함수의 마무리가 보장되어야만 하는 경우
도 있지 않겠어요?

이럴 경우 사용할 수 잇는 게 콜백함수입니다.
콜 백 : 영어로 뭐죠? : 다시 부른다. 이런 뜻이죠?

좀 이따 타이밍 맞춰서 오는 함수 부르면 그 때 오는 함수
만일 a라는 함수의 실행 뒤에 실행되어야 하는 b 함수가 있다면,
a함수가 이러는 거죠, 
야 b함수야, 일단 딴거 하고 있을게 내가 부르면 그 때 와.

그래서 콜백함수입니다.

### 콜백함수 만드는 방법

이 콜백함수는 나중에 부를 함수를 인자로 넣어줌으로서 실행 순서를 보장한다 
이렇게 할 수 있는 이유는?

> 이제는 계속말해서 지겨울듯 함수는 일급 객체니까

이 콜백 함수의 동작 원리를 좀 더 정확히 말씀드리자면
먼저 실행될 함수에게 다음 실행될 함수를 인자로 전달해주고

먼저 실행될 함수 안에서 실행해주는 겁니다.

즉, 실행할 함수를 인자로 갖고 와서 
먼저 실행할 함수를 지지고 볶고 나서 특정 시점에 실행해주겠다
이런 말이죠.

예를 들어볼까요?

(예제 1)

function a(callback) {
    setTimeout(function() {
        console.log("오래 걸리는 a 함수")
        callback();
    }, 2000);
}

function b() {
    console.log("b 함수 실행");
}

a(b);

(예제 2)

function plus(a, b) { 
  var sum = a + b;
  return sum;
}  

function print(result) {
  console.log(result);
}

print(plus(1,2));

이걸 

function plus(a, b, callback) {  // plus 함수 정의
  var sum = a + b;
  callback(sum);
}    

이렇게 바꾸기

특히 이벤트 처리 함수
어떤 이벤트가 일어나면, 어떤 함수 실행시켜라 하는 논리 작성 때 특히 많이 쓰임

---

## 콜백 지옥

근데 이러면, 눈치 빠른 분들은 이미 문제를 짐작할 수도 있겠짐나

a() b() c() d() 함수를 실행하고 싶은데 a는 5초 b는 4초 c는 3초 d는 2초 걸려 그럼 어떻게?


function one() {
  setTimeout(function() {
    console.log('1. First thing setting up second thing');
    setTimeout(function() {
      console.log('2. Second thing setting up third thing');
      setTimeout(function() {
        console.log('3. Third thing setting up fourth thing');
        setTimeout(function() {
          console.log('4. Fourth thing');
        }, 2000);
      }, 2000);
    }, 2000);
  }, 2000);
};

콜백 지옥
해결법

promise async  -> ES6

----


### 이벤트가 발생했을 때
Event Handling
#### 이벤트의 종류
#### HTML 태그로 달기
#### <script>태그 안에 이벤트 작성
#### 여러 이벤트 발생시키고 싶을 때 : addEventListener


https://github.com/kangtegong/React-Study/blob/master/%231%20JS%20for%20React/3.Async_and_Callback.md#react-with-django
https://medium.com/@oasis9217/%EB%B2%88%EC%97%AD-javascript-%EB%8F%84%EB%8C%80%EC%B2%B4-%EC%BD%9C%EB%B0%B1%EC%9D%B4-%EB%AD%94%EB%8D%B0-65bb82556c56
https://www.freecodecamp.org/news/javascript-callback-functions-what-are-callbacks-in-js-and-how-to-use-them/
https://dalkomit.tistory.com/65
https://webcoding.tistory.com/entry/JavaScript-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%BD%9C%EB%B0%B1%ED%95%A8%EC%88%98%EB%9E%80
https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/
https://medium.com/@oasis9217/%EB%B2%88%EC%97%AD-javascript-%EB%8F%84%EB%8C%80%EC%B2%B4-%EC%BD%9C%EB%B0%B1%EC%9D%B4-%EB%AD%94%EB%8D%B0-65bb82556c56
C

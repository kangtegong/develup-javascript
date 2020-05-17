자 오늘부터 본격적으로 이 ES6에 대해 다루어보도록 할겁니다
그러데 그 전에, 아직 JS 공부가 탄탄하게 된 것 같지 않으신 분들이 계신다면,
굳이 강의를 스탑하지는 마시구요, 복습과 병행하며 강의를 수강하시면 좋을 거 같아요.

어차피 이 강의에서 다룰 ES6도, 중요한 것들만 다루었다고는 하지만,
상대적으로 이해하기 쉬운 것부터 쪼금 복잡한 것 순서대로 구성이 되어 있거든요?

그니까 너무 걱정하지는 마세요.

자 일단 이 let과 const에 대해 이야기하기 전에 우리 let과 const가 나오게 된 이유에 대해 
먼저 얘기를 해 봅시다

## var의 문제점

우리는 지금까지 var를 이용해서 변수를 선언해왔죠.
물론 변수를 선언하는 방법에 아직까지는 var 밖에 소개를 안 드렸지만
이 var 로 변수를 선언하게 되면, 이런 문제점들이 있습니다.

1. 함수 스코프

스코프 시간 때 말씀 드렸지만 JS에서는 기본적으로 블록 스코프가 없기 때문에
블록 안에서 선언된 변수는 전역 변수로 취급받습니다.

따라서 젼역 변수가 많아질 수 밖에 없죠.
제가 전역변수의 남발은 절대 좋은게 아니라고도 말씀드렸죠?

```
if(true) {
    var num = 10;	// if 문 안에서만 쓰기 위한 변수
    console.log(num);
}

console.log(num);	// 전역변수로 취급받음
```

2. 중복된 이름 사용 가능

var의 두번 째 문제는 중복된 이름이 사용가능하다는 겁니다.
이는 의도치 않게 변수값의 변경이 일어날 가능성이 크다.

3. 변수의 불변성 보장이 안된다.

이건 어쩌면 2번과 맞물리는 문제기는 한데
개발을 하다보면, 너무 중요해서 값이 변경되어서는 안되는 변수, 
값이 수시로 변하는 유동적인 변수도 있지 않겠어요?

근데 var 로 변수를 선언하게 되면 
그냥 값을 대입하면 변수 안에 값이 갱신 되어 버리니까
변수의 불변성이 보장이 안되는 문제가 있습니다.

예를 들어볼까요

```
var num = 1;	// 변경하고 싶지 않은 변수
if(true) {
    var num = 10;
    console.log(num);
}
console.log(num);	// 값이 변해버림
```

## 블록 레벨 스코프 사용에 대한 요구 : let

자 이러한 불편함을 해결해줄 수 있는게 let과 const입니다

우선 let부터 알아보자면, let은 변수의 중복 선언이 안되구요,
let으로 선언한 변수는 블록 레벨 스코프를 가집니다.
이건 말보다 예제가 더 와닿을 거에요.

(예제)

## 변하지 않는 변수에 대한 요구 : const

다음은 const입니다. 이 const로 선언된 변수는 재할당을 통해 값이 바뀌지 않는다.
따라서 값이 변경되면 안되는 너무 중요한 변수에 대해 
의도치 않은 재할당을 방지해 주는 너무 기특한 변수입니다.
	
이것도 예를 들어볼까요?

블록 레벨 스코프
변하지 않는 값

주의할 점은 const는 반드시 선언과 동시에 할당이 이루어져야 한다는 거에요.

var로 선언해주면 선언만 해 주고, 값을 나중에 줄 수도 있었죠?

```
var num;
num = 3;
```
그런데 const에서는 `const 변수 = 고정으로 할당할 값` 이렇게 딱 고정을 해버려야 합니다.

```
const FOO = 123;
FOO = 456; // TypeError: Assignment to constant variable.
```

참고로 전역객체로 접근 X

## const와 배열/객체

객체 배열의 선언에도 const 물론 쓸 수 있음
배열, 객체 선언에서 const 는 권장하는 바임

객체의 경우 안의 key, property는 변경할 수 잇지만 
객체 자체의 재할당은 불가능하기 때문에 유용한 것

즉, 객체를 cosnt로 선언하게 되면 
그 틀은 const로 선언했기 때문에 재할당이 불가능하지만,
변경이 안되지만

그 안에 있는 값에 한정해서 값을 읽고 수정할 수 있게 되기 때문에 유용

const obj = {'key': 'value'};

// Attempting to overwrite the object throws an error
// Uncaught TypeError: Assignment to constant variable.
obj = {'key2': 'value2'};

// However, object keys are not protected,
// so the following statement is executed without problem
obj.key = 'value2'; // Use Object.freeze() to make object immutable

배열의 경우

// The same applies to arrays
const MY_ARRAY = [];
// It's possible to push items into the array
MY_ARRAY.push('A'); // ["A"]
// However, assigning a new array to the variable throws an error 
// Uncaught TypeError: Assignment to constant variable.
MY_ARRAY = ['B'];

## 결론

앞으로는 변수 사용할 때 let이나 const를 쓰자!!
변수 선언에는 기본적으로 const를 사용하고 let은 재할당이 필요한 경우에 한정해 사용하는 것이 좋다.
자 대망의 마지막 시간이네요, 정말 정말 긴 여정이었습니다ㅎㅎㅎ 그쵸?
마지막까지 파이팅해보도록 해요 우리

이번 시간에는 비동기처리에서 없어서는 안될 개념인 
Promise객체와 async, await에 대해서 알아보도록 할게요.

비동기처리에 대해서는 이미 한 번 다룬 적이 있죠? 
Callback함수 시간때 다룬적이 있습니다. 그쵸?

혹시라도 기억이 안나시는 분들은 해당 강의 빠르게 복습하고 오시길 바랄게요.
그 때 제가 강의에서 뭐라고 말씀드렸나면, 

callback함수로 떡칠을 해서 비동기처리를 하면은, callback 지옥이라는게 발생해서 가독성이 떨어지고
예외처리하는데에도 불편함이 있다 이렇게 말씀드렸을거에요.

그쵸?

그런 문제점을 보완하기 위해 나온 개념들을 오늘 배워볼 예정입니다.

미리 밀씀드리자면, 이 Promise라고 하는 객체는,
자세히 알려고 들면 좀 어려운 개념입니다.

딱 듣자마자 아! 한다기보다는 좀 연습을 통해 차츰 감을 잡아가는 개념에 가까워요.

때문에 이번 시간에는 굳이 길게 Promise 객체에 대해 깊이 다루기보다는
실용적인 측면에서의 Promise만 간략하게만 다루고 
ES7에 추가된 async, await 중심으로 말씀드리도록 할게요.

자 이 Promise는 뭐냐면 자바스크립트 비동기처리에 사용되는  객체라고 보시면 되는데,
비동기로 처리되길 원하는 코드를 Promise 인스턴스 안에 넣어주면 됩니다.
이렇게요. 

```
asncFunction = new Promise( () => { ... } );
```

좀 쉽게 설명을 드리자면, Promise가 영어로 무슨 뜻이죠? 약속 뭐 이런 뜻이죠?
나 이런 약속할거야, 이 안에 넣을 이 내용을 언젠간 처리할거라고 약속할게 라고 안에 쓰는 거죠.

그리고 약속은 지켜질 때도 있고 지켜지지 못할 때도 있잖아요? 
그래서 Promise 인스턴스 안에 함수를 쓸 적에는 두 개의 파라미터를 받게 되는데, 
바로 resolve와 reject입니다.

```
asncFunction = new Promise(resolve, reject) => { ... } );
```

resolve는 이 비동기함수가 잘 실행됐다! 하는 의미이고,
reject는 이 비동기함수가 에 뭔가 문제가 있다! 하는 의미를 전달하고 싶을 때 쓴다고 보시면 돼요

즉, Promise 객체를 이용해서 비동기처리를 하기 위해서는, 나 이런 약속 할거야 라고 
새롭게 만든 Promise 인스턴스 안에  비동기 실행될 코드를 써 주고, 

이 약속이 잘 지켜졌으면 "야 약속지켰다~" 하는 의미로 resolve를 호출하고
잘 안 지켜졌으면 "야 뭔가 문제가 생겼어" 하는 의미로 reject를 호출한다고 보시면 됩니다.


한 번 예를 들어볼까요?

```
function sayHello(name) {
	return new Promise((resolve, reject) => {
		setTimeout(()=>{
			console.log(`내 이름은 ${name}이야`);
			resolve();
		}, 2000)	
	}
	)
};

sayHello("민철");
```

```
function sayHello(name) {
	return new Promise((resolve, reject) => {
		setTimeout(()=>{
			console.log(`내 이름은 ${name}이야`);
			resolve(`${name}`)
		}, 2000)	
	}
	)
};

// 잘 실행된 경우, 즉 잘 resolve 되었을 경우 then 안에 있는 함수 실행
sayHello("민철")
	.then((name)=> console.log(`${name}아 안녕히가세요`));
```


자, 이런식으로 Promise객체를 이용해서 비동기처리를 할 수 있다는 걸 확인할 수 있을텐데,
그래도 아직은 뭔가 좀 익숙하지는 않죠, 그쵸?

아니, 비동기고 동기고간에, 몇 초가 걸리든 몇 분이 걸리든
비동기처리함수를 동기함수처럼 읽고 쓰고 싶다.
위에서 아래로 쭈루룩 쓰고 쭈루룩 읽고 싶다 하고 싶은 욕구가 있을 수 있지 않겠어요?

그래서 ES7에서 나온게 async await 입니다.
가장 간단하게 쓸 수 있는 방식이라고 보시면 되는데,
야, 이런 형태를 띄고 있다고 보시면 되요.

```
// 비동기로 실행할거다 라는 의미로 async를 함수이름 앞에 써 주고
async functionName (...) {
	// 이 부분은 기다림이 필요해 하는 의미로 await를 써주는거죠.
	const result = await asyncFunction()
}
```

```
function sayHello(name) {	
	return new Promise((resolve, reject) => {
		setTimeout(()=>{
			console.log(`내 이름은 ${name}이야`);
			resolve(`${name}`)
		}, 2000)	
	}
	)
};

async function greetings(name) {
	// sayHello는 반환값으로 name을 준다 : resolve(`${name}`)
	name = await sayHello("민철")
	console.log(`${name}아 안녕히가세요`)
}

greetings("minchul");

```


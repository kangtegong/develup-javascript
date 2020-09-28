# for ~ in 문

for~in 문법은 for문과 유사하지만, 반복할 수 있는 대상에 대해 조금 더 유용하게 사용할수 있는 문법이라고 보시면 됩니다.

여기서 반복할 수 있는 대상이란, 객체나 배열 등을 들 수 있겠네요.

형식은 아래와 같습니다.

```javascript
for 반복제어변수 in 반복할수있는대상 {
    // 반복제어변수로 반복하여 수행할 일
}
```

예를 들어볼까요?

```javascript
const obj = { a: 1, b: 2, c: 3 };

// obj 객체를 순회하며 obj 의 key를 담는다
for (const property in obj) {
    console.log(property);
}

// 결과
// a
// b
// c

for (const property in obj) {
    console.log(obj[property]);
}

// 결과
// 1
// 2
// 3
```

배열에 대해서도 마찬가지입니다.

```javascript
const arr = [1, 2, 3, 4, 5];
for (x in arr) {
    console.log(`index ${x}, value ${arr[x]}`);
}

// 결과: 배열의 인덱스 출력
// index 0, value 1
// index 1, value 2
// index 2, value 3
// index 3, value 4
// index 4, value 5
```

다만 배열에 대해서는 for in을 잘 사용하지는 않고, 배열 자체의 내장 메서드를 많이 사용하는 편입니다. :)

> <배열 갖고놀기> 강의를 참조해주세요~

## 참고

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in
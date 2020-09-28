# do ~ while 문

do ~ while문은 

> 일단 한 번 실행해보고(do), 그 다음에 반복할지 여부를 판단(while)해보자!

하는 문법입니다.

```javascipt
do 구문
while (조건식);
```

즉, 한 번 `구문`에 해당하는 내용을 실행시키고, 
그 다음에 `조건식`을 보고 `구문`을 반복실행할지 판단하는 문법이라고 보시면 됩니다.

먼저 조건식을 보고, 그 다음 실행할 구문을 보는 
while 문과 같은듯 다르죠?

```javascript
while (조건식) {
    구문
}
```

즉, do while문은 while문과는 달리 **최소 한 번의 실행은 보장하는 반복문**이라고 보시면 됩니다.

마지막으로 예제 보여드릴게요. 아래 예제는 [여기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/do...while)에서 가지고 온 예시입니다.

```javascript
let result = '';
let i = 0;

// 일단 먼저 do 에 있는 부분 실행
do {
  i = i + 1;
  result = result + i;
} while (i < 5);    // 그 다음 조건식 보기

console.log(result);
// expected result: "12345"
```

만약 `i`가 조건식, 즉 `(i < 5)`에 거짓이 되는 값을 가지고 있었다고 해도 한 번은 실행됩니다.

한 번 볼까요?

```javascript
let result = '';
let i = 6;

do {
  i = i + 1;
  result = result + i;
} while (i < 5);

console.log(result);
// expected result: 7
```

## 참고

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/do...while
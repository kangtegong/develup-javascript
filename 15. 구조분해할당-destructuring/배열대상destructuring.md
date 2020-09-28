# 배열을 대상으로 하는 디스트럭처링

배열도 결국엔 key값이 0부터 시작하는 정수이기 때문에 디스트럭쳐링 방식의 객체의 그것과 동일합니다 :)

아래 코드는 [여기](https://poiemaweb.com/es6-destructuring)를 참고하여 만들었습니다.

```javascript
const arr = [1, 2, 3];
const [one, two, three] = arr;
console.log(one, two, three); // 1 2 3

let [x, y, z] = [1, 2, 3];
console.log(x);     // 1
console.log(y);     // 2
console.log(z);     // 3

let [a, b, c = 3] = [1, 2];
console.log(x, y, z); // 1 2 3
```



## 참고

- https://poiemaweb.com/es6-destructuring
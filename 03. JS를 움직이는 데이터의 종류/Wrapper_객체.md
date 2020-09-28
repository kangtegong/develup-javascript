# Wrapper 객체

제가 수업시간때 다루었던 자료형으로는
number, string, boolean, undefined, null, object, symbol이 있었습니다.

이 중에서 number, string, boolean 자료형은 메서드로 다룰 수 있다고 말씀드렸는데, 여기서 의아한 점이 생기죠.

> 메서드를 가진다는 건 객체들이나 할 수 있는거 아니었나? 원시 자료형인 number, string, boolean, symbol이 어떻게 자료형을 가지지? 혹시 객체인가?

결론부터 말씀드리면 이 세 자료형에 대해서는,
이 세 원시타입 자료형을 **감싸주는** 객체인 Wrapper 객체(Number, String, Boolean, Symbol)가 존재합니다.

때문에 number, string, boolean 자료형으로 만든 변수들에 대해 메서드를 사용할 수 있고,

new를 이용해서 number, string, boolean 객체를 생성할 수도 있습니다.

아래처럼 말이죠.

```javascript
var num = new Number(123);
console.log(num);       // 123

var str = new String("hello");
console.log(str);       // hello

var bool = new Boolean(true);
console.log(bool);      // true
```

그리고 이렇게 생성한 Wrapper 객체(num, str, bool)은 각각 숫자 내장함수, 문자열 내장함수, boolean 내장함수를 적용할 수 있습니다.

```javascript
Number.isInteger(123)   //true
str.length              // 5
```



어떤 내장함수들이 있는지는 아래 링크에 남겨두도록 할테니, 혹시 궁금하시다면 찾아보시길 바랄게요 :) 

## 내장함수

- [boolean 내장함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
- [Number 내장함수](https://poiemaweb.com/js-number)
- [String 내장함수](https://poiemaweb.com/js-string)

## 참고

- https://velog.io/@kim-jaemin420/Wrapper-Object%EB%9E%98%ED%8D%BC-%EA%B0%9D%EC%B2%B4
- https://noritersand.github.io/javascript/javascript-%EB%9E%98%ED%8D%BC-%EA%B0%9D%EC%B2%B4-wrapper-objects/
- https://medium.com/@yms0214/%EC%9B%90%EC%8B%9C%EB%8D%B0%EC%9D%B4%ED%84%B0%ED%83%80%EC%9E%85-primitive-type-%EA%B3%BC-%EB%9E%98%ED%8D%BC%EA%B0%9D%EC%B2%B4-wrapper-object-d8cda814022d

# 내부함수의 this 바인딩을 해결하는 apply/call/bind

제가 강의에서 내부함수의 this는 무조건 전역객체에 바인딩된다고 말씀 드렸었죠?

이 문제를 해결할 수 있는 방법으로 apply, call, bind 가 있습니다.

이 부분은 한 방에 이해되게 너무 잘 정리된 블로그 글들이 있어 이 글들을 읽어보시길 권해드립니다 :)

1. [binding의 개념과 call, apply, bind의 차이점
](https://wooooooak.github.io/javascript/2018/12/08/call,apply,bind/)
2. [[함수호출] Call / Apply / Bind 메서드
](https://velog.io/@rohkorea86/this-%EC%99%80-callapplybind-%ED%95%A8%EC%88%98-mfjpvb9yap)
3. [apply, call, bind 호출](https://poiemaweb.com/js-this#4-applycallbind-%ED%98%B8%EC%B6%9C)

## 참조
- https://wooooooak.github.io/javascript/2018/12/08/call,apply,bind/
- https://velog.io/@rohkorea86/this-%EC%99%80-callapplybind-%ED%95%A8%EC%88%98-mfjpvb9yap
- https://poiemaweb.com/js-this#4-applycallbind-%ED%98%B8%EC%B6%9C
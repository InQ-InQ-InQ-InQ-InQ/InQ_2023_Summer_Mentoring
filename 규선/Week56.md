### 목표
- 스프링 시작하기
- 자바 틈틈히 공부하기
### 공부기록 및 내용
![](https://velog.velcdn.com/images/gyuseon/post/ee0ac62e-03b1-4d30-8393-3a09d6687787/image.png)

#### Optional
Java8부터 Optional<T>클래스를 사용해 NullPointerException(이하 NPE)를 방지할수 있도록 했다.
Optional<T> 클래스는 Integer나 Double클래스처럼 T타입의 객체를 포장해주는 래퍼클래스이다.
Optional<T>는 null이 올수 있는 값을 감싸는 Wrapper클래스로, 참조하더라도 NPE가 발생하지 않도록 도와준다.
즉, 예상치못한 NPE예외를 제공되는 메소드로 간단히 회피할 수 있어 복잡한 조건문 없이도 null값으로 인해 발생하는 예외를 처리할 수 있다.
  https://jdm.kr/blog/234
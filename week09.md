# Part 3. 라이브러리 활용
## Chapter 12. java.base 모듈
### 12.1 API 도큐먼트

- 라이브러리 : 클래스와 인터페이스의 집합
- **API(Application Programming interface)** 도큐먼트 : 자바 표준 모듈에서 제공하는 라이브러리 사용하기 위한 방법 기술

다음 URL을 방문하면 JDK 버전별로 사용할 수 있는 API 도큐먼트를 볼 수 있다.
```
https://docs.oracle.com/en/java/javase/index.html
```
자바 버전 선택 후 왼쪽 메뉴에서 [API Document] 버튼을 클릭하면 각 버전에 따른 API 도큐먼트 페이지가 열린다.   
여기서 **클래스 선언부, 구성 멤버, 필드, 생성자, 메소드** 등을 확인할 수 있다.

------

### 12.2 java.base 모듈

java.base는 모든 모듈이 의존하는 기본 모듈로, 모듈 중 유일하게 requires 하지 않아도 사용할 수 있다. 
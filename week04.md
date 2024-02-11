## Chapter 06. 클래스
### 6.1 객체 지향 프로그래밍

#### 객체(object)란?
- 물리적으로 존재하거나 개념적인 것 중에서 다른 것과 식별 가능한 것
- 속성(**필드, field**)와 동작(**메소드, method**)으로 구성

#### 객체 간의 관계
- 집합 관계
  - 완성품과 부품의 관계
  - 예) 자동차와 부품(엔진, 타이어, 핸들 등)의 관계
- 사용 관계
  - 다른 객체의 필드를 읽고 변경하거나 메소드를 호출하는 관계
  - 예) 사람과 자동차의 관계 (자동차에게 달린다, 멈춘다 등의 메소드 호출)
- 상속 관계
  - 부모와 자식 관계
  - 기계와 자동차의 관계

#### 객체 지향 프로그래밍의 특징
- 캡슐화 (Encapsulation)
  - 객체의 데이터(필드), 동작(메소드)을 하나로 묶고 실제 구현 내용을 외부에 감추는 것
  - 외부 객체는 객체 내부의 구조 알지 못하며 객체가 노출해서 제공하는 필드와 메소드만 이용 가능
  - 외부의 잘못된 사용으로 인해 객체가 손상되지 않도록 하기 위해 사용
- 상속 (Inheritance)
  - 부모 객체가 자기가 가지고 있는 필드와 메소드를 자식 객체에게 물려주어 사용할 수 있도록 하는 것
  - 코드의 재사용성 높여줌
  - 유지 보수 시간을 최소화시켜 줌
- 다형성 (Polymorphism)
  - 사용 방법은 동일하지만 실행 결과가 다양하게 나오는 성질
  - 자동 타입 변환과 재정의 기술이 필요

--------

### 6.2 객체와 클래스

- 객체 지향 프로그래밍에서 객체를 생성하려면 설계도에 해당하는 클래스(class)가 필요
- 클래스로부터 생성된 객체 : 인스턴스(Instance)
- 클래스로부터 객체를 만드는 과정 : 인스턴스화

----------

### 6.3 클래스 선언

- 객체 생성을 위한 설계도를 작성하는 작업

```java
package ch06.sec03;

public class SportsCar {
}

class Tire {
}
```

----------

### 6.4 객체 생성과 클래스 변수

*Student.java*
```java
package ch06.sec04;

public class Student {
}
```

*StudentExample.java*
```java
package ch06.sec04;

public class StudentExample {
	public static void main(String[] args) {
		Student s1 = new Student();
		System.out.println("s1 변수가 Student 객체를 참조합니다.");

		Student s2 = new Student();
		System.out.println("s2 변수가 또 다른 Student 객체를 참조합니다.");
	}
}
```

------

### 6.5 클래스의 구성 멤버

- 필드(Field)
  -  객체의 데이터를 저장하는 역할
- 생성자(Constructor)
  - 객체의 초기화 역할
  - 리턴 타입이 없고 이름은 클래스 이름과 동일
- 메소드(Method)
  - 객체가 수행할 동작
  - 객체와 객체간의 상호 작용을 위해 호출됨

-----------

### 6.6 필드 선언과 사용

#### 필드 선언
*Car.java*
```java
package ch06.sec06.exam01;

public class Car {
	//필드 선언
	String model;
	boolean start;
	int speed;
}
```

*CarExample.java*
```java
package ch06.sec06.exam01;

public class CarExample {
	public static void main(String[] args) {
		//Car 객체 생성
		Car myCar = new Car();

		//Car 객체의 필드값 읽기
		System.out.println("모델명: " + myCar.model);
		System.out.println("시동여부: " + myCar.start);
		System.out.println("현재속도: " + myCar.speed);
	}
}
```

#### 필드 사용
- 필드값을 읽고 변경

*Car.java*
```java
package ch06.sec06.exam02;

public class Car {
	//필드 선언
	String company = "현대자동차";
	String model = "그랜저";
	String color = "검정";
	int maxSpeed = 350;
	int speed;
}
```
*CarExample.java*
```java
package ch06.sec06.exam02;

public class CarExample {
	public static void main(String[] args) {
		//Car 객체 생성
		Car myCar = new Car();

		//Car 객체의 필드값 읽기
		System.out.println("제작회사: " + myCar.company);
		System.out.println("모델명: " + myCar.model);
		System.out.println("색깔: " + myCar.color);
		System.out.println("최고속도: " + myCar.maxSpeed);
		System.out.println("현재속도: " + myCar.speed);

		//Car 객체의 필드값 변경
		myCar.speed = 60;
		System.out.println("수정된 속도: " + myCar.speed);
	}
}
```

-----------

### 6.7 생성자 선언과 호출

#### 기본 생성자
- 클래스에 생성자 선언이 없으면 컴파일러는 기본 생성자(Default Constructor)를 바이트코드 파일에 자동 추가

#### 생성자 선언
- 객체를 다양하게 초기화하기 위해 개발자가 생성자 직접 선언 가능
- 리턴 타입이 없고 클래스 이름과 동일

*Car.java*
```java
package ch06.sec07.exam01;

public class Car {
	//생성자 선언
	Car(String model, String color, int maxSpeed) {
	}
}
```
*CarExample.java*
```java
package ch06.sec07.exam01;

public class CarExample {
	public static void main(String[] args) {
		Car myCar = new Car("그랜저", "검정", 250);
		//Car myCar = new Car();  //기본 생성자 호출 못함
	}
}
```

#### 필드 초기화



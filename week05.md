## Chapter 07. 상속
### 7.1 상속 개념

- 상속(Inheritance) : 부모 클래스의 필드와 메소드를 자식 클래스에게 물려주는 행위
- 이미 잘 개발된 클래스를 재사용해 새로운 클래스를 만드므로 중복되는 코드를 줄여 개발 시간 단축
- 수정을 최소화

------

### 7.2 클래스 상속

*Phone.java*
```java
package ch07.sec02;

public class Phone {
	//필드 선언
	public String model;
	public String color;

	//메소드 선언
	public void bell() {
		System.out.println("벨이 울립니다.");
	}

	public void sendVoice(String message) {
		System.out.println("자기: " + message);
	}
	
	public void receiveVoice(String message) {
		System.out.println("상대방: " + message);
	}

	public void hangUp() {
		System.out.println("전화를 끊습니다.");
	}
}
```

*SmartPhone.java*
```java
package ch07.sec02;

public class SmartPhone extends Phone {
	//필드 선언
	public boolean wifi;

	//생성자 선언
	public SmartPhone(String model, String color) {
		this.model = model;
		this.color = color;
	}

	//메소드 선언
	public void setWifi(boolean wifi) {
		this.wifi = wifi;
		System.out.println("와이파이 상태를 변경했습니다.");
	}

	public void internet() {
		System.out.println("인터넷에 연결합니다.");
	}
}
```

*SmartPhoneExample.java*
```java
package ch07.sec02;

public class SmartPhoneExample {

	public static void main(String[] args) {
		//SmartPhone 객체 생성
		SmartPhone myPhone = new SmartPhone("갤럭시", "은색");

		//Phone으로부터 상속받은 필드 읽기
		System.out.println("모델: " + myPhone.model);
		System.out.println("색상: " + myPhone.color);

		//SmartPhone의 필드 읽기
		System.out.println("와이파이 상태: " + myPhone.wifi);

		//Phone으로부터 상속받은 메소드 호출
		myPhone.bell();
		myPhone.sendVoice("여보세요.");
		myPhone.receiveVoice("안녕하세요! 저는 홍길동인데요.");
		myPhone.sendVoice("아~ 네, 반갑습니다.");
		myPhone.hangUp();
		
		//SmartPhone의 메소드 호출
		myPhone.setWifi(true);
		myPhone.internet();
	}
}
```

-----------

### 7.3 부모 생성자 호출

- 부모 클래스가 기본 생성자를 가지고 있는 경우

*Phone.java*
```java
package ch07.sec03.exam01;

public class Phone {
	//필드 선언
	public String model;
	public String color;

	//기본 생성자 선언
	public Phone() {
		System.out.println("Phone() 생성자 실행");
	}
}
```
*SmartPhone.java*
```java
package ch07.sec03.exam01;

public class SmartPhone extends Phone {
	//자식 생성자 선언
	public SmartPhone(String model, String color) {
		super();
		this.model = model;
		this.color = color;
		System.out.println("SmartPhone(String model, String color) 생성자 실행됨");
	}
}
```
*SmartPhoneExample.java*
```java
package ch07.sec03.exam01;

public class SmartPhoneExample {

	public static void main(String[] args) {
		//SmartPhone 객체 생성
		SmartPhone myPhone = new SmartPhone("갤럭시", "은색");
			
		//Phone으로부터 상속 받은 필드 읽기
		System.out.println("모델: " + myPhone.model);
		System.out.println("색상: " + myPhone.color);
	}
}
```
*결과*
```
Phone() 생성자 실행
SmartPhone(String model, String color) 생성자 실행됨
모델: 갤럭시
색상: 은색
```

- 부모 클래스가 매개변수를 갖는 생성자가 있는 경우

*Phone.java*
```java
package ch07.sec03.exam02;

public class Phone {
	//필드 선언
	public String model;
	public String color;

	//매개변수를 갖는 생성자 선언
	public Phone(String model, String color) {
		this.model = model;
		this.color = color;
		System.out.println("Phone(String model, String color) 생성자 실행");
	}
}
```
*SmartPhone.java*
```java
package ch07.sec03.exam02;

public class SmartPhone extends Phone {
	//자식 생성자 선언
	public SmartPhone(String model, String color) {
		super(model, color);        // 반드시 작성
		System.out.println("SmartPhone(String model, String color) 생성자 실행됨");
	}
}
```
*SmartPhoneExample.java*
```java
package ch07.sec03.exam02;

public class SmartPhoneExample {
	
	public static void main(String[] args) {
		//SmartPhone 객체 생성
		SmartPhone myPhone = new SmartPhone("갤럭시", "은색");
		
		//Phone으로부터 상속 받은 필드 읽기
		System.out.println("모델: " + myPhone.model);
		System.out.println("색상: " + myPhone.color);
	}
}
```
*결과*
```
Phone(String model, String color) 생성자 실행
SmartPhone(String model, String color) 생성자 실행됨
모델: 갤럭시
색상: 은색
```

---------

### 7.4 메소드 재정의
- 메소드 오버라이딩(Overriding)
    - 상속된 메소드를 자식 클래스에서 재정의
    - 해당 부모 메소드는 숨겨지고, 자식 메소드가 우선적으로 사용

- 규칙
  - 부모 메소드의 선언부와 동일해야 한다.
  - 접근 제한을 더 강하게 오버라이딩할 수 없다.
  - 새로운 예외를 throws할 수 없다.

- `super.method()`
  - 부모 메소드를 재사용
  - 자식 메소드의 중복 작업 내용을 없애는 효과를 가져온다

*Airplane.java*
```java
package ch07.sec04.exam02;

public class Airplane {
	//메소드 선언
	public void land() {
		System.out.println("착륙합니다.");
}

	public void fly() {
		System.out.println("일반 비행합니다.");
	}

	public void takeOff() {
		System.out.println("이륙합니다.");
	}
}
```
*SupersonicAirplane.java*
```java
package ch07.sec04.exam02;

public class SupersonicAirplane extends Airplane {
	//상수 선언
	public static final int NORMAL = 1;
	public static final int SUPERSONIC = 2;
	//상태 필드 선언
	public int flyMode = NORMAL;

	//메소드 재정의
	@Override
	public void fly() {
		if(flyMode == SUPERSONIC) {
			System.out.println("초음속 비행합니다.");
		} else {
			//Airplane 객체의 fly() 메소드 호출
			super.fly();
		}
	}
}
```
*SupersonicAirplaneExample.java*
```java
package ch07.sec04.exam02;

public class SupersonicAirplaneExample {
	public static void main(String[] args) {
		SupersonicAirplane sa = new SupersonicAirplane();
		sa.takeOff();
		sa.fly();
		sa.flyMode = SupersonicAirplane.SUPERSONIC;
		sa.fly();
		sa.flyMode = SupersonicAirplane.NORMAL;
		sa.fly();
		sa.land();
	}
}
```
*결과*
```
이륙합니다.
일반 비행합니다.
초음속 비행합니다.
일반 비행합니다.
착륙합니다.
```

----------

### 7.5 final 클래스와 final 메소드

- `final` 클래스
  - 최종적인 클래스이므로 더 이상 상속할 수 없는 클래스
  - 부모 클래스가 될 수 없어 자식 클래스를 만들 수 없다.
  - 대표적인 예 : `String` 클래스
- `final` 메소드
  - 최종적인 메소드이므로 오버라이딩할 수 없는 메소드
  - 자식 클래스에서 재정의할 수 없다.

###

----------

### 7.6 protected 접근 제한자

- 같은 패키지에서는 `default`처럼 접근이 가능하나, 다른 패키지에서는 자식 클래스만 접근을 허용
- 필드, 생성자 그리고 메소드 선언에 사용 가능
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

------------

### 12.3 Object 클래스

자바의 모든 클래스는 Object의 자식이거나 자손 클래스이므로 Object가 가진 메소드는 모든 객체에서 사용할 수 있다. 

#### 객체 동등 비교

- Object의 `equals()` 메소드는 객체의 번지를 비교하고 `boolean` 값을 리턴.
- Object의 `equals()` 메소드는 재정의해서 동등 비교용으로 사용되는데, 동등 비교란 객체가 비록 달라도 내부의 데이터가 같은지를 비교하는 것을 말함.

*Member.java*
```java
package ch12.sec03.exam01;

public class Member {
	public String id;

	public Member(String id) {
		this.id = id;
	}

	@Override
	public boolean equals(Object obj) {
		if(obj instanceof Member target) {
			if(id.equals(target.id)) {
				return true;
			}
		}
		return false;
	}
}
```

*EqualsExample.java*
```java
package ch12.sec03.exam01;

public class EqualsExample {
	public static void main(String[] args) {
		Member obj1 = new Member("blue");
		Member obj2 = new Member("blue");
		Member obj3 = new Member("red");

		if(obj1.equals(obj2)) {
			System.out.println("obj1과 obj2는 동등합니다.");
		} else {
			System.out.println("obj1과 obj2는 동등하지 않습니다.");
		}

		if(obj1.equals(obj3)) {
			System.out.println("obj1과 obj3은 동등합니다.");
		} else {
			System.out.println("obj1과 obj3은 동등하지 않습니다.");
		}
	}
}
```

*결과*
```
obj1과 obj2는 동등합니다.
obj1과 obj3은 동등하지 않습니다.
```

#### 객체 해시코드

- 객체 해시코드 : 객체를 식별하는 정수
- Object의 `hashCode()` 메소드는 객체의 메모리 번지를 이용해 해시코드를 생성하기 때문에 객체마다 다른 정수값을 리턴함.
- 두 객체가 동등한지를 비교할 때 주로 사용.

자바는 두 객체가 동등함을 비교할 때 `hashCode()`와 `equals()` 메소드를 같이 사용하는 경우가 많다. 

*Student.java*
```java
package ch12.sec03.exam02;

public class Student {
	private int no;
	private String name;

	public Student(int no, String name) {
		this.no = no;
		this.name = name;
	}

	public int getNo() { return no; }
	public String getName() { return name; }

	@Override
	public int hashCode() {
		int hashCode = no + name.hashCode();
		return hashCode;
	}

	@Override
	public boolean equals(Object obj) {
		if(obj instanceof Student target) {
			if(no == target.getNo() && name.equals(target.getName())) {
				return true;
			}
		}
		return false;
	}
}
```

*HashCodeExample.java*
```java
package ch12.sec03.exam02;

public class HashCodeExample {
	
	public static void main(String[] args) {
		Student s1 = new Student(1, "홍길동");
		Student s2 = new Student(1, "홍길동");

		if(s1.hashCode() == s2.hashCode()) {
			if(s1.equals(s2)) {
				System.out.println("동등 객체입니다.");
			} else {
				System.out.println("데이터가 다르므로 동등 객체가 아닙니다.");
			}
		} else {
			System.out.println("해시코드가 다르므로 동등 객체가 아닙니다.");
		}
	}
}
```

*결과*
```
동등 객체입니다.
```

#### 객체 문자 정보

- Object의 `toString()` 메소드는 객체의 문자 정보를 리턴.
- 객체의 문자 정보란 객체를 문자열로 표현한 값으로, *클래스명@16진수해시코드* 로 구성.
- 매개값이 기본 타입이거나 문자열일 경우 해당 값 그대로 출력, 객체라면 객체의 `toString()` 메소드 호출해서 리턴값 출력

#### 레코드 선언


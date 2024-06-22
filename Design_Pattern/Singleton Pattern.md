# 싱글톤 패턴(Singleton pattern)

## 개념
애플리케이션이 시작될 때 어떤 클래스가 최초 한번만 메모리를 할당하고 (static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴이다.즉  '하나'의  인스턴스만 생성하여 사용하는 패턴이다.



클래스의 생성자가 여러 번 호출되더라도 실제로 생성되는 객체는 하나이며 최초 생성 이후 호출된 생성자는 최초에 생성한 객체를 반환한다.

## 싱글톤 패턴을 왜 사용할까?
객체를 생성할 때마다 메모리 영역을 할당받아야 한다. 하지만 한번의 new를 통해 객체를 생성한다면 메모리 낭비를 방지할 수 있다. (메모리 측면에서는 이미 생성된 인스턴스를 활용하기 때문에 속도 측면에서도 이점) 또한 싱글톤으로 구현한 인스턴스는 '전역'이므로, 다른 클래스의 인스턴스들이 데이터를 공유하는 것이 가능한 장점이 있다.



이러한 장점이 있기 때문에 주로 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 사용된다.

- 인스턴스가 절대적으로 한 개만 존재하는 것을 보증하고 싶을 때 사용하기도 한다.
- ex) 데이터베이스에서 커넥션풀, 스레드풀, 캐시, 로그 기록 객체 등

## 싱글톤 패턴의 단점
- 전역에서 접근 가능 : 애플리케이션 내 어디서든 접근이 가능한 경우, 무분별한 사용을 막기 힘들다. 이로 인해 변경에 대한 복잡성이 증가할 수 있다.
- 결합도 증가  : 만약 싱글톤 인스턴스가 혼자 너무 많은 일을 하거나, 많은 데이터를 공유시키면 다른 클래스들 간의 결합도가 높아지게 되는데, 이때 개방-폐쇄 원칙이 위배된다.
- 테스트 복잡성 : 결합도가 높아지게 되면, 유지보수가 힘들고 테스트도 원활하게 진행할 수 없는 문제점이 발생한다.
- 멀티 스레드 환경 : 멀티 스레드 환경에서 동기화 처리를 하지 않았을 때, 인스턴스가 여러개 생성되는 문제도 발생할 수 있다.
- 상태 관리의 어려움 : 만약, 싱글톤 클래스가 상태를 가지고 있는 경우 전역에서 사용되어 변경될 수 있다. 이로 인해 예상치 못한 동작이 발생할 수 있다.

따라서, 반드시 싱글톤이 필요한 상황이 아니면 지양하는 것이 좋다.

## 싱글톤 패턴의 기본 구현(자바)
싱글톤 패턴을 적용할 경우 두 개 이상의 인스턴스는 존재할 수 없기 때문에 하나의 인스턴스만을 유지하기 위해 인스턴스 생성에 특별한 제약을 걸어둬야 한다.
- 객체 생성을 위한 new 생성자를 실행할 수 없도록 생성자에 private 접근 제어자를 지정한다.
- 유일한 단일 객체를 반환할 수 있도록 정적 메소드를 지원해야 한다.
- 또한 유일한 단일 객체를 참조할 정적 참조변수가 필요하다.
![img1 daumcdn](https://github.com/OkKim99/CS-Study/assets/89891488/6aa21e96-8267-4d30-9725-bf46ca1af60e)

public class Singleton {
    // 정적 참조 변수
    private static Singleton singletonObject;
    
    // private 생성자
    private Singleton() {}
	
    // getInstance()
    public static Singleton getInstance() {
        if (singletonObject == null) {
            singletonObject = new Singleton();
        }
        return singletonObject;
    }
}
- getInstance() 메서드는 singletonObject가 null이면 생성하고, null이 아니면 인스턴스를 반환한다. 이를 통해  단 하나만의 객체를 생성하여 사용할 수 있도록 한다. .


## 멀티스레드 환경에서싱글톤 패턴 구현 구현
멀티스레드 환경에서 싱글턴 패턴을 적용하면 여러 스레드가 동시에 접근하다가 하나만 생성되어야 하는 인스턴스가 두 개 생성되는 등 문제가 발생할 수 있다.

### 이른 초기화(Eager Initialization):
이른 초기화는 클래스가 로드될 때 인스턴스를 미리 생성한다. 실행과 동시에 객체가 인스턴스화하여 메모리를 점유하게 되는데 해당 **리소스를 사용하지 않는다면 자원 낭비일 뿐이다.**  만약 싱글톤 객체를 생성하는 비용이 크지 않은 경우 이른 초기화 방법을 적용할 수 있다.

public class Singleton {
	// 인스턴스를 클래스 로딩 시점에 생성
	private static Singleton singletonObject = new Singleton();

	// private 생성자
	private Singleton() {
	}

	// getInstance() : 인스턴스를 반환하는 메서드
	public static synchronized Singleton getInstance() {
		return singletonObject;
	}
}
### 게으른 초기화(Lazy Initialization)
여러가지 방법 중 쉬운 방법은 getInstance() 메서드에 sychronized키워드를 추가하여 동기화 하는 것이다. 싱글턴 패턴을 지연 초기화 (Lazy Initialization)  방식으로 구현 한다면  리소스를 효율적으로 사용할 수 있게 된다.
- 지연 초기화 (Lazy Initialization) : 초기에 생성되는 것이 아니라 객체가 필요할 때 인스턴스를 생성하는 방법.
public class Singleton {
    // 정적 참조 변수
    private static Singleton singletonObject;
    
    // private 생성자
    private Singleton() {}
	
    // getInstance() : 인스턴스를 반환하는 메서드
    public static synchronized Singleton getInstance() {
        if (singletonObject == null) {
            singletonObject = new Singleton();
        }
        return singletonObject;
    }
}
하지만 이 방법은 모든 스레드가 getInstance() 메서드를 호출할 때 동기화 작업(Lock)을 획득해야 하므로 성능 저하가 발생할 수 있다. 


### Double-Checked Locking(DCL)
Double-Checked Locking방법은  volatile 키워드와 synchronized 블록을 사용하여 인스턴스 생성의 경쟁 조건을 방지하면서, 한 번 인스턴스가 생성된 이후에는 빠른 접근을 보장하여 성능을 개선할 수 있다.



getInstance() 메서드를 사용할 때마다 동기화 작업을 하는 것이 아니라 기존 동기화 영역인 getInstance()에서 동기화 되는 영역을 줄여 초기화 시에만 동기화 작업을 수행한다.
- 동기화( synchronized )는 처음 인스턴스를 생성할 때만 사용되므로, 이후에는 성능 저하가 거의 없다.
- 
volatile 키워드를 사용하여 정적 참조 변수의 변경이 모든 스레드에 즉시 반영되도록 한다. 즉 **volatile 키워드와 synchronized  블록을 통한 더블 체크를 한다.**
- volatile 키워드가 붙은 변수는 객체의 초기화 과정이 올바른 순서로 실행되도록 보장

```
public class Singleton {
	// 정적 참조 변수, volatile 키워드 사용
	private static volatile  Singleton singletonObject;

	// private 생성자
	private Singleton() {
	}

	// getInstance()
	public static Singleton getInstance() {
		if (singletonObject == null) {
			synchronized (Singleton.class) {
				if (singletonObject == null) {
					singletonObject = new Singleton();
				}
			}
		}
		return singletonObject;
	}
}
```

- 그러나 마찬가지로 여러 스레드가 동시에 synchronized 블록에 접근하려고 할 때, 한 스레드를 제외한 나머지 스레드는 대기하게 된다.
### Bill Pugh Solution
**정적 내부 클래스(static inner class)를 사용**하여 싱글톤 패턴을 구현하는 이 방법은 가장 효율적이고 **권장되는 방법**중 하나이다.
```
public class Singleton {

    // private 생성자로 외부에서 인스턴스 생성 불가
    private Singleton() { }

    // 정적 내부 클래스
    private static class SingletonHelper {
        // Singleton 인스턴스를 정적 final 변수로 선언
        private static final Singleton INSTANCE = new Singleton();
    }

    // getInstance 메서드를 통해 Singleton 인스턴스를 반환
    public static Singleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```
SingletonHelper라는 정적 내부 클래스는 Singleton 클래스가 로드될 때 바로 로드되지 않고, **getInstance() 메서드가 호출될 때 SingletonHelper 클래스가 로드**되고 그 시점에 **정적(staitc) 변수인 INSTANCE 변수가 초기화**된다.
- INSTANCE는 정적(staitc) 변수이기 때문에 클래스 로딩시점에서 한번만 호출된다.

싱글톤 패턴에서 중요한 점은 클래스의 인스턴스가 단 하나만 존재해야 하며, 그 인스턴스가 변경되지 않아야 한다는 것으로 final을 사용하면 이런 요구사항을 충족할 수 있다.
- final 키워드가 붙은 변수는 반드시 선언과 동시에 초기화해야 하며 초기화 된 이후에 변경될 수 없다.

클래스 로딩 과정은 Java 언어 명세에 따라 스레드로부터 안전하며, 클래스 로딩과 초기화는 JVM에 의해 보장되므로 여러 스레드가 getInstance()를 호출 하더라도 INSTANCE 변수는 한번만 초기화 된다. ( 스레드 안전성 )
- JVM의 클래스 초기화 과정에서 보장되는 원자적 특성을 이용해 초기화 순서를 보장하고, 초기화가 한 번만 이루어지도록하여 싱글톤의 초기화 문제에 대한 책임을 JVM에게 떠넘길 수 있다.
  
개발자가 직접 동기화 문제에 대한 코드를 작성하면서 회피하려고 한다면 구조가 그만큼 복잡해지고 비용 문제가 발생할 수 있다. synchronized 키워드를 사용하지 않으므로, 성능 상의 부정적인 영향을 미치지 않는다.
- 클래스 로딩 메커니즘 덕분에 추가적인 동기화가 필요 없다.

Bill Pugh Singleton은 이러한 JVM의 특성을 이용하여 멀티 스레드 환경에서도 안전하게 싱글톤 인스턴스를 제공해 준다.
- 싱글톤 패턴 구현의 권장되는 방법이지만, 자바 리플렉션과 직렬화를 통해 싱글톤이 파괴될 수 있다.

====
### Enum
Java의 enum 타입은 여러 가지 특별한 특성은 Singleton 구현할 때 enum 타입을 사용한 유용하여 Singleton 구현 시 권장되는 방식이다.
- enum 타입은 Java 언어 사양에 의해 **단 하나의 인스턴스만 생성될 수 있도록 보장**된다. JVM에 의해 괸리 되므로 리플렉션이나 직렬화/역직렬화와 같은 방식으로 인스턴스를 추가로 생성할 수 없다.
- enum의 **생성자는 자동으로 private**이 되며, 외부에서 인스턴스를 생성할 수 없다.
- enum 타입은 기본적으로 **직렬화 가능한 객체** 로 추가적인 코드를 작성할 필요 없이 직렬화와 역직렬화를 자동으로 처리된다. 
이러한 Enum의 성질을 이용하면 인스턴스 관리와 관련된 코드가 전혀 없기 때문에 간결하게 싱글톤 패턴을 구현할 수 있다.
```
public enum Singleton {
    INSTANCE;
}
```

하지만 Enum은 다른 클래스를 상속할 수 없고, 다른 클래스도 Enum을 상속할 수 없다는 성질은 유연성이 떨어져 특정 상황에서는 적합하지 않을 수 있고 객체 지향 설계에서 다형성을 활용해야 하는 경우에는 사용하기 어렵다는 단점이 있다.

===
**Reference**
- https://ittrue.tistory.com/563
- https://gyoogle.dev/blog/design-pattern/Singleton%20Pattern.html
- https://dahye-jeong.gitbook.io/java/java/design_pattern/singleton_pattern

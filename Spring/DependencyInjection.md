# DI(Dependency Injection) 의존성 주입

## 1) 의존성 주입이란?

- 의존성 주입은 객체 지향 프로그래밍에서 의존하는 객체를 직접 생성하거나 관리하지 않고 외부에서 주입받는 것을 의미
- 즉, 의존성을 클래스 내부에서 생성하거나 결정하지 않고, 외부에서 주입받아 사용하는 방식입니다.
- 의존성 주입을 통해 객체간의 결합도를 줄이고 코드의 재활용성을 높일 수 있습니다.

## 2) 의존성 주입 방식

사용 방식은 총 3가지가 있습니다.

- 필드 주입(Field Injection)
- 수정자 주입(Setter Based Injection)
- 생성자 주입(Constructor Based Injection)

### 1. 필드 주입

클래스에 선언된 필드에 생선된 객체를 주입해주는 방식입니다.

사용방법은 스프링에서 제공하는 @Autowired 어노테션을 주입할 필드 위에 명시해줍니다.

```
@Component
public class HasaCalculator {
	@Autowired
	Calculator calculator;
}
```

오랫동안 잘 사용했지만 최근엔 여러가지 이유로 지양하고 있습니다.

### 2. 수정자 주입

클래스의 Setter를 통해서 의존성을 주입해주는 방식입니다.

객체가 변경될 가능성이 있는 경우에 사용합니다.

```
@Component
public class HasaCalculator {
	Calculator calculator;

	@Autowired
	public void setCalculator(Calculator calculator) {
		this.calculator = calculator;
	}
}
```

### 3. 생성자 주입

생성자 주입은 의존성을 주입받는 클래스의 생성자를 통해 의존성을 주입하는 방법입니다. 생성자의 호출 시점에 1회 호출 되는 것이 보장됩니다. 이 방법은 객체가 생성될 때 의존성을 한번에 주입받기 떄문에 의존성 주입 후에 변경이 불가능하다는 점에서 불변성을 확보할 수 있다는 장점이 있습니다.

```
@Component
public class HasaCalculator {

	private final Calculator calculator;

	public HasaCalculator(Calculator calculator) {
		this.calculator = calculator;
	}
}
```

클래스의 생성자가 1개일 경우 위 코드처럼 @Autowired를 생략할 수 있습니다.

## 정리

스프링에서는 위 3가지 방법 중 생성자 주입 방식을 권장하고 있습니다.

간단하게 @Autowired 어노테이션만 붙여주는 방식이 더 쉽고 편할 것 같은데 왜 생성자 주입을 권하고 있을까요??

그 이유는 여러가지가 있습니다.

1. 순환 참조를 방지할 수 있다.

순환 참조란 A객체는 B객체를 참조하고, B객체는 A객체를 서로 동시에 참조하고 있을 때 발생합니다.

필드 주입과 수정자 주입은 실행 중에 runtime 에러가 발생하고 생성자 주입은 실행 시점에서 compile 에러가 발생합니다.

죽 실행 시점에서 에러가 발생하기 때문에 개발자는 실제 서비스가 되기 전, 순환 참조 문제를 해결 할 수 있습니다.

2. 객체의 불변성(immutable)

생성자로 의존성을 주입할 때 final로 선언이  가능하고, 이로인해 런타임에서 의존성을 주입받는 객체가 변할 일이 없어지게 됩니다.

3. 테스트에 용이하다.

독립적으로 인스턴스화가 가능한 POJO를 사용하면 DI 컨테이너 없이도 의존성을 주입하여 사용할 수 있습니다.

위 3가지 이유로 스프링에서는 필드 주입, 수정자 주입 보다는 생성자 주입 방식을 권장하고 있습니다.     

### 참고    
https://dlalstn1023.tistory.com/7

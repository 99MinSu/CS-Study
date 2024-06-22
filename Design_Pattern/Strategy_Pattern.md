Strategy_Pattern
==
## 개념

객체의 행위를 변경하고 싶은 경우 직접 수정하지 않고 전략(캡슐화한 알고리즘)을 변경해줌으로써 유연하게 확장하는 패턴

## 장점

- 유연성: 알고리즘을 독립적으로 변경할 수 있어 코드의 유연성과 재사용성을 높입니다.
- 캡슐화: 알고리즘을 캡슐화하여 클라이언트 코드의 복잡성을 줄입니다.
- 개방-폐쇄 원칙: 새로운 전략을 추가하더라도 기존 코드를 수정할 필요가 없습니다.

## 단점

클래스 수 증가: 알고리즘마다 별도의 클래스를 정의해야 하므로 클래스 수가 증가할 수 있습니다.

## 예제: 대중교통 수단을 이용한 전략 패턴

### 1. 전략 인터페이스 정의

```java
public interface TransportationStrategy {
    void travel();
}

```

### 2. 구체적인 전략 클래스 구현

```java
public class BusStrategy implements TransportationStrategy {
    @Override
    public void travel() {
        System.out.println("Traveling by bus...");
    }
}

public class AirplaneStrategy implements TransportationStrategy {
    @Override
    public void travel() {
        System.out.println("Traveling by airplane...");
    }
}

public class BicycleStrategy implements TransportationStrategy {
    @Override
    public void travel() {
        System.out.println("Traveling by bicycle...");
    }
}

public class TaxiStrategy implements TransportationStrategy {
    @Override
    public void travel() {
        System.out.println("Traveling by taxi...");
    }
}

```

### 3. 컨텍스트 클래스 정의

컨텍스트 클래스는 현재 사용 중인 전략을 관리하고, 클라이언트가 전략을 설정할 수 있도록 합니다.

```java
public class TravelContext {
    private TransportationStrategy strategy;

    public void setStrategy(TransportationStrategy strategy) {
        this.strategy = strategy;
    }

    public void travel() {
        strategy.travel();
    }
}

```

### 4. 클라이언트 코드

```java
public class Main {
    public static void main(String[] args) {
        TravelContext context = new TravelContext();

        // 버스를 이용
        context.setStrategy(new BusStrategy());
        context.travel();  // Output: Traveling by bus...

        // 비행기를 이용
        context.setStrategy(new AirplaneStrategy());
        context.travel();  // Output: Traveling by airplane...

        // 자전거를 이용
        context.setStrategy(new BicycleStrategy());
        context.travel();  // Output: Traveling by bicycle...

        // 택시를 이용
        context.setStrategy(new TaxiStrategy());
        context.travel();  // Output: Traveling by taxi...
    }
}

```

### 요약

- **전략 인터페이스 (`TransportationStrategy`)**: 대중교통 수단의 공통 인터페이스입니다.
- **구체적인 전략 클래스 (`BusStrategy`, `AirplaneStrategy`, `BicycleStrategy`, `TaxiStrategy`)**: 각각의 대중교통 수단을 구현합니다.
- **컨텍스트 클래스 (`TravelContext`)**: 현재 사용 중인 전략을 관리하고 클라이언트가 전략을 설정할 수 있도록 합니다.
- **클라이언트 코드 (`Main`)**: 클라이언트는 `TravelContext` 객체에 원하는 전략을 설정하고 `travel()` 메서드를 호출합니다.

### 위 예제에서의 장점

- **유연한 알고리즘 선택**:
    - 다양한 대중교통 수단(버스, 택시, 비행기, 자전거 등)을 미리 구현해 두고, 클라이언트가 필요에 따라 어떤 수단을 사용할지 선택할 수 있습니다.
    - 예시: `TravelContext` 객체에 다양한 전략을 설정하고 `travel()` 메서드를 호출하여 원하는 대중교통 수단을 사용할 수 있습니다.
- **코드의 재사용성 증가**:
    - 공통 인터페이스(`TransportationStrategy`)를 통해 다양한 전략을 정의함으로써, 코드의 재사용성을 높일 수 있습니다.
    - 새로운 대중교통 수단을 추가할 때 기존 코드를 수정할 필요 없이 새로운 전략 클래스만 추가하면 됩니다.
- **유지보수 용이성**:
    - 알고리즘(전략)을 독립적인 클래스에 캡슐화함으로써, 특정 알고리즘이 변경되거나 개선되더라도 다른 알고리즘에 영향을 미치지 않습니다.
    - 예시: `BusStrategy` 클래스의 구현을 변경하더라도 `AirplaneStrategy`, `BicycleStrategy`, `TaxiStrategy` 클래스에는 영향을 주지 않습니다.
- **확장성**:
    - 새로운 전략을 추가하기 쉽습니다. 새로운 대중교통 수단을 추가할 때 기존 코드를 변경할 필요 없이 새로운 전략 클래스만 추가하면 됩니다.
    - 예시: 새로운 교통 수단 `TrainStrategy`를 추가하고, 이를 `TravelContext`에 설정하여 사용할 수 있습니다.

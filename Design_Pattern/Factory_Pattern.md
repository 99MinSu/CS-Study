팩토리 패턴
======
팩토리(Factory) 패턴 = 공장 패턴팩토리 패턴은 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴이다.

자바에서 팩토리 패턴을 사용하는 간단한 예시를 들어 설명하겠습니다. 이 예시에서는 `Shape` 인터페이스와 이를 구현하는 `Circle`, `Square`, `Rectangle` 클래스, 그리고 `ShapeFactory` 클래스를 사용합니다.

### 1. `Shape` 인터페이스 정의

```java
public interface Shape {
    void draw();
}

```

### 2. `Circle` 클래스

```java
public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

```

### 3. `Square` 클래스

```java
public class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Square");
    }
}

```

### 4. `Rectangle` 클래스

```java
public class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Rectangle");
    }
}

```

### 5. `ShapeFactory` 클래스

`ShapeFactory` 클래스는 `Shape` 객체를 생성하는 역할을 합니다.

```java
public class ShapeFactory {

    // 팩토리 메소드
    public Shape getShape(String shapeType) {
        if (shapeType == null) {
            return null;
        }
        if (shapeType.equalsIgnoreCase("CIRCLE")) {
            return new Circle();
        } else if (shapeType.equalsIgnoreCase("SQUARE")) {
            return new Square();
        } else if (shapeType.equalsIgnoreCase("RECTANGLE")) {
            return new Rectangle();
        }
        return null;
    }
}

```

### 6. 팩토리 패턴 사용 예시

이제 `ShapeFactory`를 사용하여 `Shape` 객체를 생성하고 사용하는 예시를 보겠습니다.

```java
public class FactoryPatternDemo {
    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        // Circle 객체 생성 및 사용
        Shape shape1 = shapeFactory.getShape("CIRCLE");
        shape1.draw();

        // Square 객체 생성 및 사용
        Shape shape2 = shapeFactory.getShape("SQUARE");
        shape2.draw();

        // Rectangle 객체 생성 및 사용
        Shape shape3 = shapeFactory.getShape("RECTANGLE");
        shape3.draw();
    }
}

```

### 결과 출력

위의 코드를 실행하면 다음과 같은 결과가 출력됩니다.

```css
Drawing a Circle
Drawing a Square
Drawing a Rectangle

```

### 설명

- `Shape` 인터페이스는 공통 메서드인 `draw()`를 정의합니다.
- `Circle`, `Square`, `Rectangle` 클래스는 `Shape` 인터페이스를 구현하여 각각의 `draw()` 메서드를 정의합니다.
- `ShapeFactory` 클래스는 `Shape` 객체를 생성하는 팩토리 역할을 합니다. 클라이언트 코드에서는 `ShapeFactory`의 `getShape()` 메서드를 사용하여 필요한 `Shape` 객체를 생성합니다.
- 클라이언트 코드(`FactoryPatternDemo` 클래스)는 객체 생성 로직을 알 필요 없이 `ShapeFactory`를 통해 `Shape` 객체를 생성하고 사용합니다.

이처럼 팩토리 패턴을 사용하면 객체 생성 로직을 분리하여 코드의 유연성과 재사용성을 높일 수 있습니다.

### 팩토리 패턴을 사용하지 않는 경우

팩토리 패턴을 사용하지 않는 경우, 클라이언트 코드가 객체를 직접 생성합니다. 다음은 앞서 예시에서 팩토리 패턴을 사용하지 않은 코드입니다.

```java
public class NoFactoryPatternDemo {
    public static void main(String[] args) {
        // Circle 객체 생성 및 사용
        Shape shape1 = new Circle();
        shape1.draw();

        // Square 객체 생성 및 사용
        Shape shape2 = new Square();
        shape2.draw();

        // Rectangle 객체 생성 및 사용
        Shape shape3 = new Rectangle();
        shape3.draw();
    }
}

```

### 문제점

1. **객체 생성 코드의 중복**:
    - 각 클래스 객체를 생성하는 코드가 반복됩니다. 객체 생성 로직이 변경되면 모든 클라이언트 코드에서 수정이 필요합니다.
2. **유연성 부족**:
    - 새로운 `Shape` 클래스를 추가하거나 기존 클래스의 생성 로직을 변경할 때, 모든 클라이언트 코드에 영향을 미칩니다.
    - 예를 들어, 새로운 `Triangle` 클래스를 추가하려면 모든 관련 클라이언트 코드에서 `new Triangle()`을 추가해야 합니다.
3. **코드 유지보수 어려움**:
    - 객체 생성 로직이 분산되어 있어 유지보수가 어렵습니다. 생성 로직을 변경하거나 새로운 객체를 추가할 때 일관성을 유지하기 어렵습니다.
4. **의존성 증가**:
    - 클라이언트 코드가 구체적인 클래스에 직접 의존하게 되어 클래스 간 결합도가 높아집니다. 이는 코드 변경 시 영향을 받는 범위가 넓어지는 결과를 초래합니다.

### 팩토리 패턴을 사용한 경우

팩토리 패턴을 사용하면 객체 생성 로직이 팩토리 클래스에 캡슐화되어 클라이언트 코드가 객체 생성 방식에 대해 알 필요가 없습니다. 앞서 제시한 팩토리 패턴 사용 예시를 다시 살펴보겠습니다.

```java
public class FactoryPatternDemo {
    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        // Circle 객체 생성 및 사용
        Shape shape1 = shapeFactory.getShape("CIRCLE");
        shape1.draw();

        // Square 객체 생성 및 사용
        Shape shape2 = shapeFactory.getShape("SQUARE");
        shape2.draw();

        // Rectangle 객체 생성 및 사용
        Shape shape3 = shapeFactory.getShape("RECTANGLE");
        shape3.draw();
    }
}

```

### 장점

1. **객체 생성 코드의 중복 제거**:
    - 객체 생성 로직이 `ShapeFactory`에 캡슐화되어 중복이 제거됩니다. 변경이 필요할 때 한 곳만 수정하면 됩니다.
2. **유연성 향상**:
    - 새로운 `Shape` 클래스를 추가하거나 생성 로직을 변경할 때 `ShapeFactory` 클래스만 수정하면 되므로 클라이언트 코드는 영향을 받지 않습니다.
    - 예를 들어, 새로운 `Triangle` 클래스를 추가하려면 `ShapeFactory`에 `Triangle`을 반환하는 로직만 추가하면 됩니다.
3. **코드 유지보수 용이**:
    - 객체 생성 로직이 한 곳에 집중되어 있어 유지보수가 용이합니다. 일관성을 유지하기도 쉽습니다.
4. **의존성 감소**:
    - 클라이언트 코드가 구체적인 클래스에 의존하지 않고 추상화된 팩토리 메서드를 사용하므로 결합도가 낮아집니다. 이는 코드 변경 시 영향을 받는 범위를 줄여줍니다.

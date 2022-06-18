
# 팩토리 패턴 이해하기:star:


✅ 팩토리 메소드 패턴 : 
> 객체를 생성하기 위해 인터페이스를 만든다.
> 어떤 클래스의 인스턴스를 만들지 서브클래스에서 결정하도록 한다.
> 팩토리 메소드를 이용하면 인스턴스를 만드는 일을 서브 클래스로 미룰 수 있다.


예제) 피자를 주문하는 예제
1. Creator 클래스인 PizzaStore를 만든다. 이 클래스는 createPizza 라는 팩토리 메소드를 실행해서 pizza를 생성한다.


```java

public abstract class PizzaStore {
    public Pizza orderPizza(String type) {
        Pizza pizza = createPizza(type);

        pizza.prepare();
        pizza.bake();
        pizza.box();

        return pizza;
    }

    abstract Pizza createPizza(String type);
}

```

2.PizzaStore를 확장해 각 지점을 만들고 지점마다 피자를 만드는 것을 책임지도록 createPizza 팩토리 메소드를 오버라이딩 한다.

```java
public class NYPizzaStore extends PizzaStore {
    @Override
    Pizza createPizza(String item) {
        if ("cheese".equals(item)) {
            return new NYStyleCheesePizza();
        } else if ("veggie".equals(item)) {
            return new NYStyleVeggiePizza();
        } else if ("clam".equals(item)) {
            return new NYStyleClamPizza();
        } else {
            return null;
        }
    }
}

```

```
public class ChicagoPizzaStore extends PizzaStore {
    @Override
    Pizza createPizza(String item) {
        if ("cheese".equals(item)) {
            return new ChicagoStyleCheesePizza();
        } else if ("veggie".equals(item)) {
            return new ChicagoStyleVeggiePizza();
        } else if ("clam".equals(item)) {
            return new ChicagoStyleClamPizza();
        } else {
            return null;
        }
    }
}

```
3.product 클래스인 Pizza를 만들고 이 클래스를 확장해 구상 클래스를 만들어보기.

```java
public abstract class Pizza {
    String name;
    String dough;
    String sauce;

    void prepare() {
        System.out.println("preparing~~ " + name);
    }

    void bake() {
        System.out.println("baking~~");
    }

    void box() {
        System.out.println("boxing~~");
    }
    
    public String getName() {
        return name;
    }
}


```

4. Product 클래스인 Pizza를 확장해 3가지 시카고 피자를 만들었다.

```java
public class ChicagoStyleCheesePizza extends Pizza {
    public ChicagoStyleCheesePizza() {
        name = "ChicagoStyleCheesePizza";
    }
}

```

```java
public class ChicagoStyleClamPizza extends Pizza {
    public ChicagoStyleClamPizza() {
        name = "ChicagoStyleClamPizza";
    }
}

```

```java
public class ChicagoStyleVeggiePizza extends Pizza {
    public ChicagoStyleVeggiePizza() {
        name = "ChicagoStyleVeggiePizza";
    }
}

```

5. main 메소드에서 예제 실행
```java
PizzaStore nyStore = new NYPizzaStore();
PizzaStore chicagoStore = new ChicagoPizzaStore();

Pizza nyCheesePizza = nyStore.orderPizza("cheese");
Pizza nyClamPizza = nyStore.orderPizza("clam");

Pizza chicagoCheesePizza = chicagoStore.orderPizza("cheese");
Pizza chicagoClamPizza = chicagoStore.orderPizza("clam");

```

```java
preparing~~ NYStyleCheesePizza
baking~~
boxing~~
preparing~~ NYStyleClamPizza
baking~~
boxing~~
preparing~~ ChicagoStyleCheesePizza
baking~~
boxing~~
preparing~~ ChicagoStyleClamPizza
baking~~
boxing~~

```

지점과 주어진 타임(cheeze, clam)에 따라 다른 피자를 만드는 걸 볼 수 있다.

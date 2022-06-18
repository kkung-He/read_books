
# 팩토리 패턴 이해하기:star:


## ✅ 팩토리 메소드 패턴 : 
>
> 객체를 생성하기 위해 인터페이스를 만든다.
> 어떤 클래스의 인스턴스를 만들지 서브클래스에서 결정하도록 한다.
> 팩토리 메소드를 이용하면 인스턴스를 만드는 일을 서브 클래스로 미룰 수 있다.
> 

</br>

## ✅ 추상 팩토리 패턴 목적:
>
> 구체적인 클래스를 명시하지 않고 관련된 혹은 의존적인 객체들을 생성 할 수 있는 인터페이스 제공
> 

문제 
- 객체를 생성하는 'new'의 문제 : new는 인터페이스가 아니라 실제 클래스를 생성
- - OCP 에 어긋남: not closed for modification
</p>    1. 생성할 객체가 늘어나면 코드 수정 필요
</p>    2. 클래스가 많아지거나 변경되면 클라이언트 측 변경이 많아짐

</br>
=> 인터페이스를 바탕으로 만들면 여러 변화에 대응할 수 있다. (다형성 덕분)
새로운 구상 형식을 써서 확장 해야 할 때는 어떻게 해서든 다시 열 수 있게 만들어야 한다.<- <u>바뀌는 부분을 찾아내서 바뀌지 않는 부분과 분리해야 한다는 원칙 적용</u>


</br>
</br>

## ✅ 구현 
예제) 피자를 주문하는 예제
</br>
orderPizza 메소드 : 피자 종류를 고르고 그에 맞게 피자를 만드는 코드 추가
</br>

```java

Pizza orderPizza(String type) {

    Pizza pizza;


    **if(type.equals("cheese")) pizza = new CheesePizza();**

    **else if(type.equals("greek")) pizza = new GreekPizza();**

    **else if(type.equals("pepperoni")) pizza = new PepperoniPizza();**       



    pizza.prepare();

    pizza.bake();

    pizza.cut();

    pizza.box();

    return pizza;

} 

```

* if ~ else if  부분은 계속 바뀐다! 피자 종류를 추가한다든지, 잘 나가지 않아서 삭제한다든지! 
</br>
=> 캡슐화가 필요하다! 그리고새로 만들 객체에는 **팩토리(Factory)** 라는 이름을 붙이기로 한다.

</br>
간단한 피자 팩토리를 만든다
</br>
```java
public class SimplePizzaFactory {

	public Pizza createPizza(String type) { // 이런 경우에는 static메소드로 선언하는 경우가 종종 있음.

		Pizza pizza = null;

		if (pizza.equals("cheese"))
			pizza = new CheesePizza();

		if (pizza.equals("pepper"))
			pizza = new PepperoniPizza();

		if (pizza.equals("clam"))
			pizza = new ClamPizza();

		if (pizza.equals("veggie"))
			pizza = new VeggiePizza();

		return pizza;

	}

}

```

</br>
바뀐 PizzaStore 클래스
</br>
```java
public class PizzaStore {

	SimplePizzaFactory simplePizzaFactory;

	public PizzaStore(SimplePizzaFactory simplePizzaFactory) {

		this.simplePizzaFactory = simplePizzaFactory;

	}

	public Pizza orderPizza(String type) {

		Pizza pizza;

		pizza = simplePizzaFactory.createPizza(type);

		pizza.prepare();

		pizza.bake();

		pizza.cut();

		pizza.box();

		return pizza;

	}

}

```

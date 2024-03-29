# 어댑터패턴 이해하기 :star2:

</br>
</br>

## 🎨 이해 : 변장

<img width="414" alt="어댑터패턴 이해" src="https://user-images.githubusercontent.com/98209409/177018636-cdb9cf9e-0980-488c-9403-1a8c1b837d19.PNG">

출처 : https://swk3169.tistory.com/255

</br>
</br>

## 🎨 클래스 다이어그램 

<img width="700" alt="adapter pattern 2" src="https://user-images.githubusercontent.com/98209409/176467346-2a83e8d6-ed7c-42d8-bcf3-e90361132ee4.png">

출처 : https://byulmuri.wordpress.com/2010/07/26/adapter-pattern/  

</br>
</br>

## ✅ 타겟, 어댑터, 어댑티
타겟 : 클라이언트는 타겟만을 알고 있다. 즉 다른 인터페이스는 이 타겟으로 변환되어야 한다. </p>
어댑터 : 어댑티를 타겟으로 변환해주는 중간 매개체 </p>
어댑티 : 변환이 될 대상 </p>


</br> 
</br>

나의 의견 : 변신 시켜야 하는 애를 데리고 가서 원하는 모습으로 꾸며준다. </p>

</br>
</br>

## ✅ 정의
> 한 클래스의 인터페이스를 클라이언트에서 사용하고자 다른 인터페이스로 변환한다 </p>
> 어댑터를 이용하면 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 쓸 수 있다. </p>

</br>
</br>

## ✅ 클라이언트에서 어댑터를 사용하는 방법 </p>
>1. 클라이언트에서 타깃 인터페이스로 메소드를 호출해서 어댑터에 요청을 보낸다. </p>
>2. 어댑터는 어댑티 인터페이스로 그 요청을 어댑티에 관한 (하나 이상의) 메소드 호출로 변환한다. </p>
>3. 클라이언트는 호출 결과를 받긴 하지만 중간에 어댑터가 있다는 사실을 모른다. </p>

</br>
</br>

```java

public class TurkeyAdapter implements Duck {

	Turkey turkey;

	public TurkeyAdapter(Turkey turkey) {

		this.turkey = turkey;

	}

	@Override
	public void quack() {

		turkey.gobble();

	}

	@Override
	public void fly() {

		turkey.fly();

	}

}

```


</br>
</br>

## ✅ 객체 어댑터
> 어댑티를 어댑터가 객체고 갖고 있다. (구성) </p>
> 객체 구성(composition)을 사용한다 </p>
> 어댑티 뿐만 아니라 그 서브 클래스에 대해서도 어댑터 역할을 할 수 있다는 장점이 있다. </p>
</br>

<img width="700" alt="객체 어댑터" src="https://user-images.githubusercontent.com/98209409/176469115-e78466a6-9795-44af-952d-e75bfba9a2c1.png">

출처 : https://aaronryu.github.io/2019/02/27/adapter-decorator-facade-pattern/

</br>

```java

class Adapter implements TargetInterface {
    private Adaptee adaptee; 
    // ... adaptee 함수를 활용해 TargetInterface 의 함수를 구현합니다.
}
```

</br>
</br>

## ✅ 클래스 어댑터
> 다중 상속을 사용한다. 즉 자바에서는 적용할 수 없는 어댑터라 할 수 있다. (자바는 다중상속 불가) </p>
> 타겟이 인터페이스가 아닌 클래스 이다. 즉 다른 클래스로 대체할 수 없다. 타겟과 어댑터가 단단히 엮인다.  </p>
> 어댑티 전체를 다시 구현하지 않아도 된다는 장점이 있다.</p>
> 또한 어댑티의 행동을 오버라이드 할 수 있다.</p>

</br>

<img width="700" alt="클래스 어댑터" src="https://user-images.githubusercontent.com/98209409/176468935-63deee8f-bd2f-4fc5-adda-50472f825d2a.png">

출처 : https://aaronryu.github.io/2019/02/27/adapter-decorator-facade-pattern/

</br>

```java
class Adapter extends Target, Adaptee {
    // ... adaptee 함수를 활용해 Target 의 함수를 확장합니다.
    //클래스 어댑터에선 타겟과 어댑티 클래스 둘 모두를 상속 받는 서브 클래스를 만들어 요청 처리
}
```
</br>
</br>

## ✅ 객체 어댑터와 클래스 어댑터 장단점

</br>

<img width="511" alt="객체 어댑터 클래스어댑터" src="https://user-images.githubusercontent.com/98209409/177019446-03c0ceb6-0f36-4a19-823a-7ea837783b3f.PNG">

출처 : https://bb-dochi.tistory.com/80

</br>
</br>

클래스 어댑터에서는 어댑터를 만들 때 타겟과 어댑티 모두의 서브 클래스로 만들고, </p>
객체 어댑터에서는 구성을 통해서 어댑티에 요청을 전달한다는 점을 제외하면 별다른 차이점이 없다.

</br>
</br>




# 퍼사드패턴 이해하기 :star2:

</br>
</br>

## ✅ 이해 : 묶음
> 퍼사드(facade) : 겉으로 드러난 표면  </p>
집에 홈시어터가 있다. 홈시어터로 영화를 보려면 많은 과정 필요! 스크린 내리고-> 프로젝터 키기 -> 프로젝터와 연결 -> ... </p>
-> 필요시마다 객체 생성 및 객체의 메소드를 호출해야한다. </p>
-> 퍼사드는 얘를 watchMovie() 메소드 하나로 묶을 수 있다. </p>
-> 즉, 단순화된 인터페이스를 통해 서브시스템을 더 쉽게 사용 할 수 있도록 하기 위한 용도로 쓰인다!

</br>
</br>


## ✅ 정의
> 서브시스템의 일련의 인터페이스를 통합 인터페이스로 묶어 준다.  </p>
> 고수준 인터페이스도 정의하므로 서브시스템을 더 편리하게 사용할 수 있다.(복잡한 추상화 필요없음) </p>
> 즉, 퍼사드 패턴을 사용하려면 어떤 서브시스템에 속한 일련의 복잡한 클래스들을 단순화하고 통합한 클래스를 만들어야 한다.  </p>
> 복잡한 서브 시스템과 분리

</br>

<img width="860" alt="퍼사드패턴" src="https://user-images.githubusercontent.com/98209409/176871529-97bbe8b3-cd02-4b9a-aaed-7d43570e668d.png">

출처 : https://m.hanbit.co.kr/channel/category/category_view.html?cms_code=CMS8616098823

</br>

```java

public class Facade {

    private Package1 p1;
    private Package2 p2;
    private Package3 p3;

    Facade() {
        p1 = new Package1();
        p2 = new Package2();
        p3 = new Package3();
    }

    public void processFacade() {
        p1.process();
        p2.process();
        p3.process();
    }
}
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.processFacade();

    }


```
소스 출처 : https://joomn11.tistory.com/67

</br>



</br>

## ✅ 디자인 원칙

> 최소 지식 원칙 (Demeter(디미터) 혹은 데메테르 의 법칙) : 정말 친한 친구하고만 얘기하라! </p>
> 어떤 객체든 그 객체와 상호작용하는 클래스의 개수에 주의해야 하며, </p>
> 그런 객체들과 어떤식으로 상호작용을 하는지에도 주의를 기울여야 한다.</p>
</br>

> 객체 간의 상호작용을 줄이는 4가지 가이드라인 : 다음 4종류 객체의 메소드만 호출 </p>
>  1. 객체 자체 </p> 
>  2. 메소드에 매개변수로 전달된 객체 </p>
>  3. 해당 메소드에서 생성하거나 인스턴스를 만든 객체 </p>
>  4. 그 객체에 속하는 구성요소(멤버변수로 저장되는 객체) </p>

</br>
</br>

## ✅ 예시

```java
public class Car {

	Engine engine; // 이 클래스의 구성요소. 이 구성요소의 메소드는 호출해도 된다.

	public Car() {}

	public void start(Key key) { // 매개변수로 전달된 객체의 메소드는 호출해도 된다.

		Doors doors = new Doors(); // 새로운 객체 생성. 이 객체의 메소드는 호출해도 된다.

		boolean authorized = key.turns(); // 매개변수로 전달된 객체의 메소드는 호출해도 된다.

		if (authorized) {

			engine.start(); // 이 객체의 구성요소의 메소드는 호출해도 된다.

			updateDashboardDisplay(); // 객체 내에 있는 메소드는 호출해도 된다.

			doors.lock(); // 직접 생성하거나 인스턴스를 만든 객체의 메소드는 호출해도 된다.

		}

	}

	public void updateDashboardDisplay() {}

}

```

출처: https://swk3169.tistory.com/256 

</br>
</br>

## ✅ 각 패턴과 용도 

데코레이터 패턴 : 인터페이스는 바꾸지 않고 책임(기능)만 추가 </p>
어댑터 패턴 : 한 인터페이스를 다른 인터페이스로 변환 </p>
퍼사드 패턴 : 인터페이스를 간단하게 바꿈

</br>
</br>



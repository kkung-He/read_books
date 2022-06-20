
## 싱글톤 패턴 이해하기 🌟

</br>

## 🎯 용도
> 스레드 풀, 캐시, 대화상자, 사용자 설정 혹은 레지스트리를 처리하는 객체, 로그 기록용 객체, 디바이스
> 드라이버 등 객체 중에 하나만 있으면 되는 경우 사용 (오히려 2개면 좋지 않다!)
</br>
</br>


## ✅ 고전적 싱글톤패턴 구현

</br>
- 생성자는 private 으로 설정하고, 객체를 부를 때에는 따로 static 함수를 사용한다. 인스턴스가 있을 경우에는 그대로 그 인스턴스를 반환하고, 인스턴스가 없을 경우에는 생성하여 인스턴스를 반환하면 된다. 

</br>
</br>

```java

public class Singleton {
    private static Singleton uniqueInstance;

    private Singleton() {}
    
    public static Singleton getInstance() {
        if (uniqueInstance == null) {
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
    }
}
```
</br>

## ✅ 게으른 인스턴스 생성(Lazy instantiation)
uniqueInstance에 하나밖에 없는 인스턴스가 저장, uniqueInstance가 null 이어서아직 인스턴스가 만들어지지 않았다면 private로 선언된 생성자를 이용해서 Singleton객체를 만든다음 uniqueInstance 변수에 객체를 대입한다.
</br>
이렇게 하면 인스턴스가 필요한 상황이 닥치기 전에는 아예 인스턴스를 생성하지않게되고 이런 방법을 게으른 인스턴스 생성(lazy instantiation)이라고 부른다.

</br>

## :exclamation: 게으른 인스턴스 생성의 문제 , 초콜릿 공장
대부분 초콜릿 공장에는 초콜릿 끓이는 장치(초콜릿 보일러)를 컴퓨터로 제어한다. 이 보일러에서는 초콜릿과 우유를 받아서 끓이고 초코바를 만드는 단계로 넘겨준다.
</br>
여기에 최신형 초콜릿 보일러를 제어하기 위한 클래스가 있다. 코드를 보면 잘못된 실수를 하지 않기 위해 여러가지 장치가 되어있음을 알 수있다.
</br>

```java
public class ChocolateBoiler {
    private boolean empty;
    private boolean boiled;
    
    public ChocolateBoiler() {
        empty = true; // 이 코드는 보일러가 비어있을 때만 동작한다
        boiled = false; 
    }
    
    public void fill() {
        if(isEmpty()) { // 보일러가 비어있을 때만 재료를 가득 채운다. 원료를 가득 채우고 나면 boiled 를 false 로 돌려놓는다.
            empty = false;
            boiled = false;
            // 보일러에 우유/초콜릿을 혼합한 재료를 집어넣음
        }
    }
    
    /**
    * 보일러에 들어있는 재료를 다음 단계로 넘긴다.
    */
    public void drain() {
        if(!isEmpty() && isBoiled()) {  // 보일러가 가득 차있고 다 끓여진 상태에서만 보일러에 들어있는 재료를 다음 단계로 넘긴다. 보일러를 다 비우고 나면 empty 플래그를 다시 true로 설정한다.
            // 끓인 재료를 다음 단계로 넘김
            emtpy = true;
        }
    }
    
    /**
    * 보일러에 들어있는 재료를 끓인다. 
    */
    public void boil() {
        if(!isEmpty() && !isBoiled()) { // 보일러가 가득 차있고 아직 끓지 않은 상태만 초콜릿과 우유가 혼합된 재료로 끓인다. 재료를 다 끓이면 boild를 true로 설정한다.
            emtpy = true;
        }
    }
    
    public boolean isEmpty() {
        return empty;
    }
    
    public boolean isBoiled() {
        return boiled;
    }
}
```
</br>

위의 코드는 괜찮아 보인다. 그러나 만약에 ChocolateBoiler의 인스턴스 여러개가 각기 생성되면 어떤 문제가 발생할까?  </p>

- 보일러에 들어있는 재료가 끓고 있는데 재료를 부어 버릴 수 있다. </p>
- 재료를 동시에 다음 단계로 넘겨서 다음 단계에 문제가 생길 수 있다.  </p>
=> 위의 문제를 해결하기 위해 ChocolateBoiler에 싱클톤 패턴을 적용 할 수 있다. </p>

</br>

```java
public class ChocolateBoiler {
    private boolean empty;
    private boolean boiled;
    private ChocolateBoiler uniqueInstance;
    
    private ChocolateBoiler() {
        empty = true; // 이 코드는 보일러가 비어있을 때만 동작한다
        boiled = false; 
    }
    
    public static ChocolateBoiler getInstance() {
        if(uniqueInstance == null) {
            uniqueInstance = new ChocolateBoiler();
        }
        
        return uniqueInstance;
    }
    
    public void fill() {
        if(isEmpty()) { // 보일러가 비어있을 때만 재료를 가득 채운다. 원료를 가득 채우고 나면 boiled 를 false 로 돌려놓는다.
            empty = false;
            boiled = false;
            // 보일러에 우유/초콜릿을 혼합한 재료를 집어넣음
        }
    }
    
    public void drain() {
        if(!isEmpty() && isBoiled()) {
            // 끓인 재료를 다음 단계로 넘김
            emtpy = true;
        }
    }
    
    public void boil() {
        if(!isEmpty() && !isBoiled()) {
            emtpy = true;
        }
    }
    
    public boolean isEmpty() {
        return empty;
    }
    
    public boolean isBoiled() {
        return boiled;
    }
}
```
</br>

아까 앞에서 보았던 것과 같은 싱글톤 패턴을 적용하면 하나의 인스턴스만 생성하게 강제 할 수 있다.

</br>

## 📝 정의
> 싱글톤 패턴은 해당 클래스의 인스턴스가 하나만 만들어지고, 어디서든지 그 인스턴스에 접근 할 수 있도록 하기 위한 패턴

</br>

- 반드시 생성은 클래스 자신을 통해 하도록 하여, 다른 어떤 클래스에서도 자신의 인스턴스를 추가로 만들지 못하도록 한다.
- 싱글톤은 '게으르게' 생성할 수 있다. 클래스의 객체가 자원을 많이 잡아먹는 경우에 유용하다.

## :exclamation: 문제 발생


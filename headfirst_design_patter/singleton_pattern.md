
## 싱글톤 패턴 이해하기 🌟

</br>

## 📝 정의
> 싱글톤 패턴은 해당 클래스의 인스턴스가 하나만 만들어지고, 어디서든지 그 인스턴스에 접근 할 수 있도록 하기 위한 패턴

</br>

- 반드시 생성은 클래스 자신을 통해 하도록 하여, 다른 어떤 클래스에서도 자신의 인스턴스를 추가로 만들지 못하도록 한다.
- 싱글톤은 '게으르게' 생성할 수 있다. 클래스의 객체가 자원을 많이 잡아먹는 경우에 유용하다.

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
    // 객체가 초기화되지 않은 경우에는 객체를 초기화해준다.
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


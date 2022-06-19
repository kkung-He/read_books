
## 싱글톤 패턴 이해하기 🌟

## 🎯 용도
> 스레드 풀, 캐시, 대화상자, 사용자 설정 혹은 레지스트리를 처리하는 객체, 로그 기록용 객체, 디바이스
> 드라이버 등 객체 중에 하나만 있으면 되는 경우 사용
</br>
</br>

## ✅ 고전적 싱글톤패턴 구현법

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

## 📝 정의
> 싱글톤 패턴은 해당 클래스의 인스턴스가 하나만 만들어지고, 어디서든지 그 인스턴스에 접근 할 수 있도록 하기 위한 패턴

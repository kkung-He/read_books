# 어댑터패턴 이해하기 :star2:

</br>
</br>

## ✅ 정의
> 한 클래스의 인터페이스를 클라이언트에서 사용하고자 다른 인터페이스로 변환한다 </p>
> 어댑터를 이용하면 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 쓸 수 있다. </p>
> 어댑터를 사용함으로써 클라이언트와 구현된 인터페이스를 분리시킬수 있으며, </p>
> 나중에 인터페이스가 바뀌더라고 그 변경 내역은 어댑터에 캡슐화되기 때문에 클라이언트는 바뀔 필요가 없다. </p>

</br>
</br>

## ✅ 어댑터의 2가지 종류
- 타겟{Target) : 내가 사용하고 싶은 애 </p>
- 어댑티(Adaptee) : 내 의사와 관계없이 제공받은 애 </p>

</br>
</br>

## ✅ 객체 어댑터
> 객체 구성(composition)을 사용한다 </p>
> 어댑티 뿐만 아니라 그 서브 클래스에 대해서도 어댑터 역할을 할 수 있다는 장점이 있다. </p>

</br>
</br>

## ✅ 클래스 어댑터
> 다중 상속을 사용한다. 즉 자바에서는 적용할 수 없는 어댑터라 할 수 있다. (자바는 다중상속 불가) </p>
> 어댑티 전체를 다시 구현하지 않아도 된다는 장점이 있다.</p>
> 또한 어댑티의 행동을 오버라이드 할 수 있다.</p>
> 특정 어댑티 클래스에서만 적용된다는 단점이 있다.</p>
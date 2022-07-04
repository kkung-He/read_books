# 상태(state) 패턴 이해하기 :star2:

</br>
</br>

## 🎯 의도
> 스테이트 패턴에서는 필요한 기능을 인터페이스로 만들고, </p>
> 모든 상태를 캡슐화시켜서 해당 인터페이스를 구현하도록 만든다.</p>
> 스테이트 패턴을 사용하면 각 상태별 기능의 동작을 명확하게 분리 할 수 있다.

</br>
</br>

## ✅ 정의
> 상태패턴을 사용하면 객체 내부 상태가 바뀜에 따라서 객체의 행동을 바꿀 수 있다. </p>
> 마치 객체의 클래스가 바뀌는 것과 같은 결과를 얻을 수 있다.</p>

> => 각 상태마다 클래스를 분리하여 정의하고, 구성 관계를 통해 여러 상태 객체를 바꿔가면서 사용함으로써 </p>
클라이언트는 Context의 메소드를 호출 하는 것만으로도 상태 관련 작업을 처리 할 수 있다. </p>
> => if, switch 문과 같은 분기문을 패턴을 이용해 캡슐화, 분리 한다고 생각하면 된다. 

</br>
</br>

## ✅ 구조
<img width="589" alt="스테이트 패턴" src="https://user-images.githubusercontent.com/98209409/177044901-6497c778-6a7c-4e23-bbb2-18b5406b5ed2.png">

출처 : https://yiyj1030.tistory.com/404

</br>

전략 패턴과 동일한 구조를 가진다.

</br>
</br>

## ✅ context(상황), state(상태), concreteState(구체적 상태) 
> context </p>
> 여러가지 내부 상태를 가질 수 있는 클래스 </p>
> request가 호출되면 상태 객체에게 그 작업을 위임한다. </p>

> state </p>
> 모든 구상 상태 클래스에 대한 공통 인터페이스를 정의한다. </p>
> 모든 상태 클래스에서 이를 구현하기 때문에 바꿔가면서 사용할 수 있다. </p>

> concreteState </p>
> context로 부터 전달된 요청을 처리하는 구상 상태 클래스 </p>
> 각각의 구상 클래스들은 요청을 처리하는 방법을 자기 나름의 방식으로 구현한다.
> context에서 상태를 바꾸기만 하면 행동도 같이 바뀌게 된다. 

</br>
</br>

## ✅ 뽑기 기계
> 뽑기 기계는 동전없음, 동전있음, 알맹이 매진, 알맹이 판매 의 4가지 상태를 가질 수 있다.</p>
> 동전 투입, 동전 반환, 손잡이 돌리기, 알맹이 배출 의 4가지 행동을 가지고 있다. </p>
> 행동 실행 시 상태가 변한다.


```java

public class GumballMachine{
    final static int SOLD_OUT = 0;
    final static int NO_QUARTER = 1;
    final static int HAS_QUARTER = 2;
    final static int SOLD = 3;
    
    int state = SOLD_OUT;
    int count = 0;
    
    ..
    public GumballMachine(int count) {
      this.count = count;
      if(count > 0) {
      state = NO_QUARTER;
      }  
    }
    
}
 
```
</br>

-> 이 상황에서 각각의 행동을 구현하려면 행동에 해당하는 메소드에서 if문으로 state의 상태에 따라 행동을 분기해야 한다. </p>
-> 이럴 경우 상태 클래스가 추가 될때마다 모든 메소드에서 코드를 추가해야 하는 불편함이 있다! </p>
-> 바뀌는 부분은 캡슐화! 

```java
//계속해서 바뀌는 부분 

if(상태 == 동전있음) {
} else if(상태 == 동전없음) {
} else if(상태 == 알맹이 판매 {
} else if(상태 == 알맹이 매진) {
}

```
이를 분리 하려면 각 상태의 행동을 별도의 클래스에 집어넣고 모든 상태에서 각각 자기가 할 일을 구현하게 하면 된다. </p>


</br>
</br>

```java

================================>

//변경된 코드
public class GumballMachine{
    //상수 대신 상태 클래스를 사용
    State soldOutState; 
    State noQuarterState;
    State hasQuarterState
    State soldState;
    
    State state = soldState;
    int count = 0;
    
    public GumballMachine(int numberGumballs){
    	soldOutState = new SoldOutState(this); 
    	noQuarterState = new NoQuarterState(this);
    	hasQuarterState = new HasQuaterState(this);
    	soldState = new SoldState(this);
        
        this.count = numberGumballs;
        if(numberGumballs > 0)
        	state = noQuarterState;
    }
    
    public void insertQuarter(){
    	//조건문이 전부 사라지고 현재 상태 객체에 위임
        state.insertQuarter();
    }
    
    public void ejectQuarter(){
        state.ejectQuarter();
    }
    
    public void turnCrank(){
        state.turnCrank();
        state.dispense();
    }
    
    ..
    
    //해당 메소드를 사용해 다른 객체에서 상태 변경 가능
   	void setState(State state){
    	this.state = state;
    }
    
    
    //..각 State 객체를 위한 getter 메소드 등등..
    
}

```

</br>
</br>


## ✅ 개선점

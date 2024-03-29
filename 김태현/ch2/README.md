# 2. 동작 파라미터화 코드 전달하기
코딩은 불편함과 문제를 해결해나가는 과정.

### 느끼는 불편함: 자주 바뀌는 요구사항에 관하여 평범한 정적인 파라미터들로는 효과적으로 대응할 수 없다.
#### 해결책 => 동적 파라미터화(아직 어떻게 실행할 것인지 결정하지 않은 코드 블록)를 적용하여 유연하게 대응한다.

#### 자바에서 동적 파라미터화를 구현하는 과정: 
교재에서는 전략 디자인 패턴을 이용. 전략 디자인 패턴이란 각 알고리즘을 캡슐화하는 알고리즘 패밀리를 정의해둔 다음 런타임에 알고리즘을 선택하는 기법.

1. 동작을 수행하기 위해 갖추길 원하는 형태를 가진 알고리즘 패밀리를 인터페이스를 이용하여 생성
2. 위 인터페이스를 상속받으며 원하는 동작을 수행하게 하는 클래스(전략)를 생성.
3. 생성한 클래스의 인스턴스를 함수의 파라미터로 이용하여 동적 파라미터를 이용하게됨.

### 해결책 평가:
코드의 유연성이 매우 좋아짐.
#### 또다시 불편한 점: 단순한 동작을 수행하기 위해서 진행되는 과정들이 너무 복잡하다. 코드 또한 반복되는 부분이 증가하며 지저분해짐.
#### 해결책: 해당 과정을 간소화 시키자:

##### 방법 1: 익명 클래스 이용
평가: 어느정도의 복잡함은 해결. 하지만 여전히 많은 공간을 차지하는 코드들.

##### 방법 2: 람다 표현식 이용
평가: 몹시 간단해진 코드. 유연성과 간결함을 동시에 얻을 수 있음. 
불편한 점을 억지로 꼽자면 람다 표현식에 관련하여 학습을 하여 어떤 것이 간소화 된것인지 이해해야할 필요가 있음.


### 결론: 동적 파라미터화는 자바 api의 많은 메서드에서 이용할 정도로 많은 유연성을 제공하는 방법이니 코드를 짤때 적극 활용해보도록 하며, 상황에 따라 익명 클래스 사용, 람다 표현식 사용을 적용하여 코드에 간결성 또한 적용해보자.

## 예제 코드
```java
public interface ApplePredicate { 
    boolean test (Apple apple);
}
public static List<Apple> filterApples(List<Apple> inventory, ApplePredicate p) {
    List<Apple> result = new ArrayList<>();
    for (Apple apple : inventory) {
        if(p.test(apple)) {
            result.add(apple);
        }
    }
    return result;
}
public class AppleLightWeightRedColor implements ApplePredicate {
    public boolean test(Apple apple) {
        return RED.equals(apple.getColor()) 
                && apple.getWeight() < 150;
    }
}

List<Apple> redApples = filterApples(inventory, new ApplePredicate() {
            public boolean test(Apple apple) {
                return RED.equals(apple.getColor());
        }
});

List<Apple> redApples = filterApples(inventory,
        (Apple apple) -> RED.equals(apple.getColor()));
```

```java
public String processFile() throws IOEception {
	try(BufferedReader br = 
                  new BufferedReader(new FileReader("data.txt"))) {
	   return br.readLine();	
    }
}
public interface BufferedReaderProcessor {
	String process(BufferedReader b) throws IOException;
}
public String processFile(BufferedReaderProcessor p) throws IOException {
  try(BufferedReader br = 
                  new BufferedReader(new FileReader("data.txt"))) {
	   return p.process(br);	
    }
}
String oneLine = processFile((BUfferedReader br) -> br.readLine()); 
String twoLine = processFile((BUfferedReader br) -> br.readLine() + String oneLine = processFile((BUfferedReader br) -> br.readLine()); 
);
```

# 제네릭
* 타입을 파라미터화해서 컴파일시 구체적인 타입이 결정되도록 하는 것

## 제네릭을 사용하므로 얻는 이점
```java
List list = new ArrayList();
list.add("hello");
String str = (String) list.get(0);

List<String> list = new ArrayList<String>();
list.add("hello");
String str = list.get(0);
```
* 컴파일시 강한 타입 체크를 할 수 있다. 실행시 타입 에러가 나는 것이 아닌 컴파일시 미리 타입을 체크해서 에러를 사전에 방지한다.
* 위 코드처럼 타입 변환을 제거할 수 있다.

# solidity정리

## 데이터 타입
* data type : boolean, bytes, address, uint
* reference type : string, Arrays, struct
* mapping type

## 함수의 종류
1. Parameter와 Return 값이 없는 function 정의
```solidity
function changeA1() public{
  a=5;
}
```
2. Parameter는 있고, Return값이 없는 function정의
```solidity
function changeA2(uint256 _value) public{
  a=_value;
}
```
3. Parameter와 Return값이 모두 있는 경우
```solidity
function changeA3(uint256 _value) public returns(uint256){
  a=_value;
  return a;
}
```

## 접근제어자

* public : 모든 곳에서 접근가능
* external : public처럼 모든곳에서 접근 가능하나, external이 정의된 자기자신 컨트랙 내에서 접근 불가
* private : 오직 private이 정의된 자기 컨트랙에서만 가능(private이 정의된 컨트랙을 상속 받은 자식도 불가능)
* internal : private처럼 오직 internal이 정의된 자기 컨트랙에서만 가능하고, internal이 정의된 컨트랙을 상속

1. public 예시 (배포를 했을 때 외부에서 접근가능)
```solidity
uint 256 public a=5;
```
2. private 예시 (배포를 했을 때 외부에서 접근불가능)
```solidity
uint 256 public a=5;
```

* 컨트랙트 예제
```solidity
contract Public_example{
  uint256 public a = 3;
  function changeA(uint256 _value) public{
    a = _value;
  }
  
  function get_a() view public returns(uint256){
    return a;
  }
}

contract Public_example_2{
  Public_example instance = new Public_example();
  
  function changeA_2(uint256 _value) public{
    instance.changeA(_value);
  }
  
  function use_pulbic_example_a() view public returns(uint256){
    return instance.get_a();
  }
}
```

## View와 Pure
* view : function 밖의 변수들을 읽을 수 있으나 변경 불가능
* pure : function 밖의 변수들을 읽지 못하고, 변경도 불가능
* view 와 pure 둘 다 명시 안할 경우 : function 밖의 변수들을 읽어서 변경해야함
* 컨트랙트 예제
```solidity
contract example{
  uint256 public a = 1;
  
  //1. view
  function read_a() public view returns(uint256){
    return a+2;
  }
  
  //2. pure
  function read_a2() public pure returns(uint256){
    uint256 b = 1;
    return 4+2+b;
  }
  
  //3. pure, view x
  function read_a3() public returns(uint256){
    a = 13;
    return a;
  }
}
```

## 4개의 저장영역과 String
* storage : 대부분의 변수, 함수들이 저장되며, 영속적으로 저장이되어 가스 비용이 비싸다.
* memory : 함수의 파라미터, 리턴값, 레퍼런스 타입이 주로 저장된다.
* colldata : 주로 external function의 파라미터에서 사용된다.
* stack : EVM(Ethereum Virtual Machine)에서 stack data를 관리할 때 쓰는 영역으로 1024Mb 제한적이다.
* 컨트랙트 예제
```solidity
contract example{
  function get_string(string memory_str) public pure returns(string memory){
    return _str;
  }
  
  //uint같은 datatype에서는 memory가 default임.
  function get_uint(uint256 _ui) public pure returns(uint256 memory){
    return _ui;
  }
}
```

## instance
* 서로 다른 컨트랙트를 연결하기 위해 사용함
* 컨트랙트 예제
```
contract A{
  uint256 public a = 5;
  
  function change(uint256 _value) public{
    a = _value;
  }
}

contract B{
  A instance = new A();
  //A컨트랙트의 a변수를 읽음
  function get_A() public view returns(uint256){
    return instance.a();
  }
  //A컨트랙트의 a변수에 _value값을 입력
  function change A(uint256 _value) public{
    instance.change(_value);
  }
}
```

## constructor
* 컨트랙트를 인스턴스로 만들 때 값을 초기화하는 역할을 함
* 컨트랙트 예제
```
contract A{
  string public name;
  uint256 public age;
  
  //생성자 정의
  constructor(string memory _name, uint256 _age){
    name = _name;
    age = _age;
  }
  //name,age변경 함수
  function change(string memory _name, uint256 _age) public {
    name = _name;
    age = _age;
  }
}

contract B{
  A instance = new A("Alice", 52);
  //위에 생성한 인스턴스에 접근해서 값을 바꾸는 함수
  function change(string memory _name, uint256 _age) public{
    instance.change(_name, _age);
  }
  //생성한 인스턴스의 값을 호출하는 함수
  function get() public view returns(string memory, uint256){
    return (instance.name(),instance.age());
  }
}
```

## 상속
* 컨트랙트 예제
```solidity
//부모 컨트랙트
contract Father{
  string public familyName = "Kim";
  string public givenName = "Jung";
  uint256 public money = 100;
  
  constructor(string memory _givenName) public{
    givenName = _givenName;
  }
  
  function getFamilyName() view public returns(string memory){
    return familyName;
  }
  
  function getGivenName() view public returns(string memory){
    return givenName;
  }
  
  function getMoney() view public returns(uint256){
    return money;
  }
}

//자식 컨트랙트 is Father를 통해 상속
contract Son is Father("James"){
  //("James")를 통해 상속과 통시에 construct가 적용됨
}
```
## 오버라이딩 Overriding
* 상속을 받고 함수를 다시 선언하는것
* 컨트랙트 예제
```solidity
contract Father{
  string public familyName = "Kim";
  string public givenName = "Jung";
  uint256 public money = 100;
  
  constructor(string memory _givenName) public{
    givenName = _givenName;
  }
  
  function getFamilyName() view public returns(string memory){
    return familyName;
  }
  
  function getGivenName() view public returns(string memory){
    return givenName;
  }
  
  function getMoney() view virtual public returns(uint256){
  //virtual이 자식 컨트랙트에서 오버라이딩이 가능하게 함
    return money;
  }
}

contract Son is Father("James"){
  //constructor() Father("James"){
  //}
  //constructor 오버라이딩 가능
  
  uint256 public earning = 0;
  
  function work() public {
    earning += 100;
  }
  
  //virtual이 자식 컨트랙트에서 override를 통해 오버라이딩을 함
  function getMoney() view override public returns(uint256){
    return money;
  }
}
```

## 두개 이상 상속
* 컨트랙트 예제
```solidity
contract Father{
  uint256 public fatherMoney = 100;
  function getFatherName() public pure returns(string memory){
    return "KimJung";
  }
  function getMoney() public view virtual returns(uint256){
    return fatherMoney;
  }
}
contract Mother{
  uint256 public motherMoney = 500;
  function getMotherName() public pure returns(string memory){
    return "Leesol";
  }
  function getMoney() public view virtual returns(uint256){
    return motherMoney;
  }
}
contract Son is Father, Mother{
//Mother와 Father의 getMoney가 겹치기 때문에 오버라이딩 해야함.
  function getMoney() public view override(Father, Mother) returns(uint256){
    //두개의 컨트랙트에서 상속받기 때문에 override(Father, Mother)를 넣어줘야함
    return fatherMoney+motherMoney;
  }
}
```

## event
* print가 없기 때문에 event를 통해 값을 출력할 수 있음
* event로 값을 출력할 때 블록안에 저장됨
* 컨트랙트 예제
```solidity
contract{
  event info(string name, uint256 money);
  
  function sendMoney() public{
    emit info("KimDaeJin", 1000);
    //보내는 사람, 보내는 금액을 저장함
    //호출되면 블록체인의 블록에 저장이 됨.
  }
}
```
* logs의 info와 데이터가 들어간 것을 볼 수 있음

## index
* event내에서 사용할 수 있는 키워드
* 특정한 event의 값을 들고 올 때 사용됨
* 컨트랙트 예제
```solidity
 event numberTracker(uint256 num, string str);
 event numberTracker2(uint256 indexed num, string str);
 //num을 통해 특정 이벤트를 가져올 수 있음
 //10개의 이벤트가 있고 5번째의 이벤트가 필요할 때 해당 이벤트를 가져올 수 있음
 
 uint256 num = 0;
 function PushEvent(string memory _str) public {
  emit numberTracker(num_str);
  emit numberTracker2(num,_str);
  num++;
 }
```
web3js를 통해 값을 불러옴
```javascript
  sync function getEvent(){
    let events = await lecture14.getPastEvents('numberTracker2',{filter:{num:[2,1]},fromBlock:1,toBlock:'latest'}).log(events)
    //numberTracker : event이름
    //filter : indexed를 적용한 num을 통해 블록을 가져옴
    //fromBlock, toBlock 블록 첫번째부터 마지막까지 탐색
    
    let events = await lecture14.getPastEvents('numberTracker',{filter:{num:[2,1]},fromBlock:1,toBlock:'latest'}).log(events)
    //index를 안써줬기 때문에 모든 값이 출력됨
  }
```

## super
* 함수를 오버라이딩할 때 사용하는것
* 컨트랙트 예제
```solidity
contract Father{
  event FatherName(string name);
  function who() public virtual{
    emit FatherName("KimDaeho");
  }
}

contract Son is Father{
  event sonName(string name);
  function who() public override{
    super.who(); //부모 컨트랙트의 who를 그대로 가져옴
    emit sonName("KimJin");
  }
}
```

## 상속의 순서
* 컨트랙트 예제
```solidity
contract Father{
  event FatherName(string name);
  function who() public virtual{
    emit FatherName("KimDaeho");
  }
}

contract Mother{
  event MotherName(string name);
  function who() public virtual{
    emit MotherName("leeSol");
  }
}
contract Son is Father, Mother{
  function who() public override(Father, Mother){
    super.who(); 
    //두개의 컨트랙트를 상속받고 있을 때 MotherName을 가져옴(가장 최근에 상속받았기 때문에)
    //Mother와 Father의 순서를 바꾸면 FatherName이 
  }
}
```

## Mapping(맵핑)
* 특정 키값을 정의하고 키값에 대응되는 값을 반환받도록 하는것
* 컨트랙트 예제
```solidity
contract example{

  mapping(uint256=>uint256) private ageList;
  mappint(string=>uint256) private priceList;
  mapping(uint256=>string) private nameList;

  function setAgeList(uint256 _index, uint256 _age) public{
    ageList[_index] = _age;
  }
  
  function getAge(uint256 _index) pulbic view returns(uint256){
    return ageList[_index];
  }
  
  function setNameList(uint256 _index, string memory _name) public{
    nameList[_index] = _name;
  }
  
  function getName(uint256 _index) public view returns(string memory){
    return nameList[_index];
  }
  
  function setPriceList(string memory _itemName, uint256 _price) public{
    priceList[_itemName] = _price;
  }
  
  function getPriceList(string memory _index) public view returns(uint256){
    return priceList[_index];
  }
}
```

## 배열
* 컨트랙트 예제
```solidity
contract example{
  //사이즈 제한없음
  uint256[] public ageArray;
  //사이즈 10개 제한
  uint256[10] public ageFixedSizeArray;
  
  function AgeLength() public view returns(uint256){
    return ageArray.length; 
  }
  //0->50 / 1 -> 70 / length : 2
  function AgePush(uint256 _age)public{
    ageArray.push(_age);
  }
  
  //1 -> 70
  function AgeGet(uint256 _index)public view returns(uint256){
    return ageArray[_index];
  }
  
  //0->50 / length : 1      (가장 최근의 값을 삭제함)
  function AgePop()public {
    ageArray.pop();
  }
  
  //0->0 / 1 -> 70 / length : 2 (인덱스로 원하는 값 삭제함)
  function AgePop(uint256 _index)public {
    delete ageArray[_index];
  }
  
  //0->90 / 1 -> 70 / length : 2 (인덱스로 원하는 값 변경 없는 인덱스를 선택하면 에러)
  function AgeChange(uint256 _index, uint256 _age) public{
    ageArray[_index] = _age;
  }
}  
```



[solidity강좌](https://www.youtube.com/channel/UCuTGg-K1DY9cl8YtBKbQR9A)

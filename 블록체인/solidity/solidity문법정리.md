# solidity정리

## 데이터 타입
* data type : boolean, bytes, address, uint
* reference type : string, Arrays, struct
* mapping type

## 함수의 종류
1. Parameter와 Return 값이 없는 function 정의

<details>
  
```solidity
function changeA1() public{
  a=5;
}
```
  
</details>  
  
2. Parameter는 있고, Return값이 없는 function정의
<details>

```solidity
function changeA2(uint256 _value) public{
  a=_value;
}
```
  
</details>  
 
  
3. Parameter와 Return값이 모두 있는 경우
<details> 

```solidity
function changeA3(uint256 _value) public returns(uint256){
  a=_value;
  return a;
}
```
  
</details>

## 접근제어자

* public : 모든 곳에서 접근가능
* external : public처럼 모든곳에서 접근 가능하나, external이 정의된 자기자신 컨트랙 내에서 접근 불가
* private : 오직 private이 정의된 자기 컨트랙에서만 가능(private이 정의된 컨트랙을 상속 받은 자식도 불가능)
* internal : private처럼 오직 internal이 정의된 자기 컨트랙에서만 가능하고, internal이 정의된 컨트랙을 상속

1. public 예시 (배포를 했을 때 외부에서 접근가능)
<details> 
  
```solidity
uint 256 public a=5;
```

</details>   
  
2. private 예시 (배포를 했을 때 외부에서 접근불가능)

<details> 

```solidity
uint 256 public a=5;
```
</details> 

* 컨트랙트 예제

<details> 

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
  
</details> 

## View와 Pure
* view : function 밖의 변수들을 읽을 수 있으나 변경 불가능
* pure : function 밖의 변수들을 읽지 못하고, 변경도 불가능
* view 와 pure 둘 다 명시 안할 경우 : function 밖의 변수들을 읽어서 변경해야함
* 컨트랙트 예제

<details> 

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
  
</details> 

## 4개의 저장영역과 String
* storage : 대부분의 변수, 함수들이 저장되며, 영속적으로 저장이되어 가스 비용이 비싸다.
* memory : 함수의 파라미터, 리턴값, 레퍼런스 타입이 주로 저장된다.
* colldata : 주로 external function의 파라미터에서 사용된다.
* stack : EVM(Ethereum Virtual Machine)에서 stack data를 관리할 때 쓰는 영역으로 1024Mb 제한적이다.
* 컨트랙트 예제

<details> 

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
  
</details> 

## instance
* 서로 다른 컨트랙트를 연결하기 위해 사용함
* 컨트랙트 예제

<details> 

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
  
</details> 

## constructor
* 컨트랙트를 인스턴스로 만들 때 값을 초기화하는 역할을 함
* 컨트랙트 예제

<details> 
  
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
  
</details> 

## 상속
* 컨트랙트 예제

<details> 

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
  
</details> 

## 오버라이딩 Overriding
* 상속을 받고 함수를 다시 선언하는것
* 컨트랙트 예제
<details> 

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
  
</details> 

## 두개 이상 상속
* 컨트랙트 예제

<details>   

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
  
</details> 

## event
* print가 없기 때문에 event를 통해 값을 출력할 수 있음
* event로 값을 출력할 때 블록안에 저장됨
* 컨트랙트 예제

<details> 

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
  
</details> 

* logs의 info와 데이터가 들어간 것을 볼 수 있음

## index
* event내에서 사용할 수 있는 키워드
* 특정한 event의 값을 들고 올 때 사용됨
* 컨트랙트 예제

<details> 

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
  
</details> 

web3js를 통해 값을 불러옴

<details> 

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
  
</details> 

## super
* 함수를 오버라이딩할 때 사용하는것
* 컨트랙트 예제

<details> 

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
  
</details> 

## 상속의 순서
* 컨트랙트 예제

<details> 

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
  
</details> 

## Mapping(맵핑)
* 특정 키값을 정의하고 키값에 대응되는 값을 반환받도록 하는것
* 컨트랙트 예제

<details> 

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
  
</details> 

## 배열
* 컨트랙트 예제

<details> 

```solidity
contract example{
  //사이즈 제한없음
  uint256[] public ageArray;
  //사이즈 10개 제한
  uint256[10] public ageFixedSizeArray;
  //배열값 미리 정의
  string[] public nameArray = ["Kal","Jhon","Kerri"];
  
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
  
</details> 

## Mapping과 Array주의할 점
* 받은 값이 이후에 변경되어도 업데이트를 해서 적용을 해줘야함
* 컨트랙트 예제

<details> 

```solidity
contract example{
  uint256 num = 89;
  mapping(uint256 => uint256) numMap;
  uint256[] numArray;
  
  function changeNum(uint256 _num) public{
    num = _num;
  }
  
  function showNum() public view returns(uint256){
    return num;
  }
  
  function numMapAdd() public{
    numMap[0] = num;
  }
  
  function showNumMap() public view returns(uint256){
    return numMap[0];
  }
  
  function numArrayAdd() public{
    numArray.push(num);
  }
  
  function showNumArray() public view returns(uint256){
    return numArray[0];
  }
}
```
  
</details> 

## struct
* 컨트랙트 예제

<details> 

```solidity
contract example{
  struct Character{
    uint256 age;
    string name;
    string job;
  }
  
  mapping(uint256=>Character) public CharacterMapping;
  Character[] public CharacterArray;
  
  function createCharacter(uint256 _age, string memory _name, string memory _job) pure public returns(Character memory){
    return Character(_age,_name,_job);
  }
  
  //CharaterArray를 다루기 위한 함수
  function createCharacterMapping(uint256 _key, uint256 _age, string memory _name, string memory _job) public {
    CharacterMapping[_key] = Character(_age,_name,_job);
  }
  function getCharacterMapping(uint256 _key) public view returns(Character memory) {
    return CharacterMapping[_key];
  }
  function createCharacterArray(uint256 _key, uint256 _age, string memory _name, string memory _job) public {
    CharacterArray.push(Character(_age, _name, _job));
  }
  function getCharacterArray(uint256 _index) public view returns(Character memory){
    return CharacterMapping[_index];
  }
  
}
```
  
</details> 

## if 조건문
* case1 : if-else
* case2 : if-else if-else
* 컨트랙트 예제

<details> 

```solidity
contract example{
  string private outcome = "";
  function isIt5(uint256 _number) public returns(string memory){
    if(_number == 5){
      outcome = "Yes, it is 5";
      return outcome;
    }else{
      outcome = "No, it is not 5";
      return outcome;
    }
  }
  
  function isIt5or3or1(uint256 _number) public returns(string memory){
    if(_number == 5){
      outcome = "Yes, it is 5";
      return outcome;
    }else if(number == 3){
      outcome = "Yes, it is 3";
      return outcome;
    }else if(number == 1){
      outcome = "Yes, it is 1";
      return outcome;
    }else{
      outcome = "No, it is not 5,3,1";
      return outcome;
    }
  }
}
```
  
</details> 

## 반복문
```
for(초기값; 값이 얼마나 forloop을 돌아야하는지; forloop 한번 돌때마다 값의 변화;){
  forloop내용
}

while(값이 얼마나 whileloop을 돌아야하는지){
whileloop내용
whileloop 한번 돌때마다 값의 변화;
}

do{
  dowhileloop 내용
}while(값이 얼마나 do-while loop을 돌아야하는지
```
  
* 컨트랙트 예제

<details> 

```solidity
contract example{
  event CountryIndexName(uint256 indexed _index, string _name);
  string[] private countryList = ["South Korea","North Korea","USA", "china","Japan"];
  
  function forLoopEvents() public{
    for(uint256 i=0; i<countryList.length; i++){
      emit CountryIndexName(i,countryList[i]);
    }
  }
  
  function whileLoopEvents() public {
    uint256 i=0;
    while(i<countryList.length){
      emit CountryIndexName(i,countryList[i]);
      i++;
    }
  }
  
  function doWhileLoopEvents() public {
    uint256 i=0;
    do{
      emit CountryIndexName(i,countryList[i]);
      i++;
    }while(i<countryList.length);
  }
}
```
                                  
</details> 

## Linear Search
* 배열을 
* 컨트랙트 예제
<details> 
  
```solidity
contract example{
  event CountryIndexName(uint256 indexed _index, string _name);
  string[] private countryList = ["South Korea", "North Korea","USA", "China","Japan"];
  
  function linearSearch(string memory _search) public view returns(uint256, string memory){
    for(uint256 i=0; i<countryList.length;i++){
      //solidity에는 문자열을 비교하는 기능이 없음 그래서 hash값으로 변환해서 비교해야함
      if(keccak256(bytes(countryList[i])) == keccak256(bytes(_search))){
        return (i,countryList[i]);
      }
    }
    return (0,"Nothing");
}
```
                                                
</details> 

## 에러핸들러
* 에러핸들러 : require, revert, assert, try/catch
* 0.4.22 ~ 0.7.x    
* assert : gas를 다 소비한 후, 특정한 조건에 부합하지 않으면 (false일 때)에러를 발생시킨다.
* revert : 조건없이 에러를 발생시키고, gas를 환불 시켜준다.
* require : 특정한 조건에 부합하지 않으면(false일 때) 에러를 발생시키고, gas를 환불 시켜준다.
* 컨트랙트 예제
<details> 
  
```solidity
contract example{
  //3000000gas  가스를 소비하고 반환은 안해줌
  function assertNow() public pure{
    assert(false);
  }
  //21322gas 소모한 gas를 제외하고 반환해줌
  function revertNow() public pure{
    revert("error!!");  //조건이 없기 때문에 //if를 써서 사용하거나 require를 사용함
  }
  //21338gas   require = if+revert
  function requireNow() public pure{
    require(false, "occurred");
  }
  
  function onlyAdults(uint256 _age) public pure returns(string memory){
    if(_age < 19){
      revert("You are not allowed to pay for the cigarette");
    }
    return "Your payment is scceeded";
  }
  
  function onlyAdults2(uint256 _age) public pure returns(string memory){
    require(_age>19,"You are not allowed to pay for the cigarette");
    return "Your payment is scceeded";
  }
  
}
```
  
</details> 
  
* 0.8.1 ~
* assert : 오직 내부적 에러 테스트 용도, 불변성 체크 용도.
* assert가 에러를 발생시키면 panic(uint256)이라는 에러타입의 에러 발생
* assert에러는 0으로 나눈경우, empty array에서 pop을 한 경우 등 발생한다.
* 컨트랙트 예제
  
<details> 
  
```solidity
contract example{
  //0.8 이상에서는 gas를 환불해줌
  function assertNow() public pure{
    assert(false);
  }
  
  function revertNow() public pure{
    revert("error!!");  //조건이 없기 때문에 //if를 써서 사용하거나 require를 사용함
  }
  
  function requireNow() public pure{
    require(false, "occurred");
  }
}
```
  
</details>
  
*try/catch
* 0.6버전 이후
* 기존의 에러 핸들러 assert/revert/require는 에러를 발생시키고 프로그램을 끝냄
* try/catch를 사용하면 에러가 나도 프로그램을 종료시키지 않고 대처를 하게 만들 수 있다.


* tyr/cath특징
1. try/catch문 안에서 assert/revert/require을 통해 에러가 난다면 catch는 에러를 잡지 못하고, 개발자가 의도한지 알고 정상적으로 프로그램을 끝낸다.
2. 3가지 catch (catch Error, catch Panic, catch)
3. 쓰는 곳 
  * 외부 스마트 컨트랙을 함수로 부를 때 : 다른 스마트 컨트랙을 인스턴스화해서, try/catch문이 있는 스마트 컨트랙트에 사용
  * 외부 스마트 컨트랙을 생성 할 때 : 다른 스마트컨트랙을 인스턴스화 생성 할 때 씀



## modifier
* revert나 require를 넣어서 사용함
* 컨트랙트 예제
  
<details> 
  
```solidity
contract example{
  modifier onlyAdults{
    revert("You are not allowed to pay for the cigarette");
    _; //함수가 적용되는 자리
  }
  
  function BuyCigarette() public onlyAdults returns(string memory){
    return "Your payment is succeeded";
  }
  
  modifier onlyAdults2(uint256 _age){
    require(_age>18,"You are not allowed to pay for the cigarette");
  }
  
  function BuyCigarette2(uint256 _age) public onlyAdults2(_age) returns(string memory){
    return "Your payment is succeeded";
  }
  
}
```
  
</details> 

## SPDX 라이센스/주석
* SPDX-License_identifier의 목적
1. 라이센스를 명시해줌으로써 스마트컨트랙에 대한 신뢰감을 높일 수 있음
2. 스마트 컨트랙 소스코드가 워낙 오픈되어 있으니, 저작권과 같은 관련된 문제를 해소

* 주석
1. 블록단위 : 보통 블록단위의 주석은 스마트컨트랙, 함수 등 많은 양의 설명
2. 행단위 : 행단위는 변수 바로 옆에 쓰여서 짤막짤막한 설명 


## payable, msg.value와 이더를 보내는 3가지 함수(send, transfer,call)
* Payable
* Payable은 이더/토큰과 상호작용 시 필요한 키워드라고 생각하면 간단하다.
* 즉 send, transfer, call을 이용하여, 이더를 보낼 때 Payable이라는 키워드가 필요하다
* 이 Payable은 주로 함수, 주소, 생성자에 붙여서 사용한다.

* msg.value
* msg.value는 송금보낸 코인의 값이다.
* 이더를 보내는 3가지 방법
  * send : 2300 gas를 소비, 성공여부를 true 또는 false로 리턴한다. error를 보내지 못하는 단점
  * transfer : 2300gas를 소비, 실패시 에러를 발생
  * call : 가변적인 gas 소비(gas값 지정 가능), 성공여부를 true 또는 false로 리턴. 재진입 공격에 취약함. 2019년 12월 이후부터는 call 사용을 추천
* 컨트랙트 예제
  
<details>  
  
```solidity
contract example{
  event howMuch(uint256 _value);
  
  function sendNow(address payable _to) public payable{
    bool sent = _to.send(mst.value);
    require(sent,"Failed to send either");
    emit howMuch(msg.value);
  }
  
  function transferNow(address payable _to) public payable{
    _to.transfer(msg.value);
    emit howMuch(msg.value);
  }
  
  function callNow(address payable _to) public payable{
    // ~ 0.7
    // (bool sent, ) = _to.call.gas(1000).value(msg.value)("");
    // require(sent, "Failed to send either");
    
    // 0.7 ~
    (bool sent, ) = _to.call{value: msg.value, gas:1000}("");
    require(sent, "Failed to send Ether");
    emit howMuch(msg.value);
  }
}
```
  
</details> 

## balance와 msg.sender
* 주소.balance
* 주소.balance는 해당 특정 주소의 현재 갖고있는 이더의 잔액을 나타낸다.(msg.value는 송금액)
* 주소.balance와 같은 형태로 사용한다.

* msg.sender
* msg.sender는 스마트컨트랙을 사용하는 주체라고 볼 수 있다.
* msg.sender는 call vs delegate call에서 주요 내용이다.

* 컨트랙트 예제
  
<details> 
  
```solidity
contract MobileBanking{
  event SendInfo(address _msgSender, uint256 _currentValue);
  event MyCurrentValue(address _msgSender, uint256 _value);
  event CurrentValueOfSomeone(address _msgSender, address _to, uint256 _value);
  
  function sendEther(address payable _to) public payable{
    require(msg.sender.balance>=msg.value, "Your balance is not enough");
    _to.transfer(msg.value);
    emit SendInfo(msg.sender,(msg.sender).balance);
  }
  
  function checkValueNow() public{
    emit MyCurrentValue(msg.sender, msg.sender.balance);
  }
  
  function checkUserMoney(address _to) public{
    emit CurrentValueOfSomeone(msg.sender, _to, _to.balance);
  }
}
```
  
</details> 
  
## payable 생성자 적용, msg.sender로 권한 부여
* 컨트랙트 예제

  
<details> 
  
```solidity
contract MobileBanking{
  
  
  address ownaer;
  //배포를 할 때 컨트랙트에 돈을 보냄
  constructor() payable{
    owner = msg.sender;
  }
  
  modifier onlyOwner{
    //owner에 저장된 주소와 msg.sender가 같은 경우에만 동작
    require(msg.sender == owner, "Only Owner!");
    _;
  }
  
  event SendInfo(address _msgSender, uint256 _currentValue);
  event MyCurrentValue(address _msgSender, uint256 _value);
  event CurrentValueOfSomeone(address _msgSender, address _to, uint256 _value);
  
  function sendEther(address payable _to) public payable{
    require(msg.sender.balance>=msg.value, "Your balance is not enough");
    _to.transfer(msg.value);
    emit SendInfo(msg.sender,(msg.sender).balance);
  }
  
  function checkValueNow() public{
    emit MyCurrentValue(msg.sender, msg.sender.balance);
  }
  
  function checkUserMoney(address _to) public{
    emit CurrentValueOfSomeone(msg.sender, _to, _to.balance);
  }
}
```
  
</details> 
  
## fallback/receive함수
* fallback 함수
1. 무기명 함수, 이름이 없는 함수이다.
2. external 필수
3. payable
  
* fallback함수를 쓰는 이유
1. 스마트 컨트랙이 이더를 받을 수 있게 한다.
2. 이더 받고 난 후 어떠한 행동을 취하게 할 수 있다.
3. call함수로 없는 함수가 불려질 때, 어떤한 행동을 취하게 할 수 있다.
  
* 0.6 이후 fallback은 receve와 fallback의 두가지 형태로 나눠진다.
* receive는 순수하게 이더만 받을 때 작동한다.
* fallback은 함수를 실행하면서 이더를 보낼 때, 불려진 함수가 없을 때 작동한다.

## call
* call : 로우레벨 함수
1. 송금하기
2. 외부 스마트 컨트랙 함수 부르기
3. 가변적인 gas
4. 이스탄불 하드포크, 2019년 12월 이후 gas가격 상승에 따른, call 사용 권장/ send transfer = 2300gas
5. re-entrancy(재진입) 공격위험 있기에, Checks_Effects_Interactions_pattern 사용
  
  
## call vs delegate call
* Delegate call:
1. msg.sender가 본래의 스마트컨트랙 사용자를 나타낸다.
2. delegate call이 정의된 스마트 컨트랙(즉 caller)이 외부 컨트랙의 함수들을 마치 자신의 것처럼 사용(실질적인 값도 caller에 저장)

  
## enum
* enum : 사람이 읽을 수 있게, 사용자/개발자에 의해 정의된 상수세트 타입(uint8 = 0~255(2^8-1))
* 컨트랙트 예제

<details>
  
```
contract example{
  enum CarStatus{
    TurnOff,
    TurnOn,
    Driving,
    Stop
  }  
  
  CarStatus public carStatus;
  
  constructor(){
    carStatus = CarStatus.TurnOff;
  }
  
  event carCurrentStatus(CarStatus _carStatus, uint256 _carStatusInInt);
  
  function turnOnCar() public{
    require(carStatus == CarStatus.TurnOff, "To turn on, your car must be turned off");
    carStatus = CarStatus.TurnOn;
    emit carCurrentStatus(carStatus, uint256(carStatus));
  }
  
  function DrivingCar() public{
    require(carStatus == CarStatus.TurnOn, "To drive a car, your car must be turned on");
    carStatus = CarStatus.Driving;
    emit carCurrentStatus(carStatus, uint256(carStatus));
  }
  
  function StopCar() public{
    require(carStatus == CarStatus.Driving, "To drive a car. your car must be turned on")
    carStatus = CarStatus.Stop;
    emit carCurrentStatus(carStatus, uint256(carStatus));
  }
  
  function turnOffCar() public{
    require(carStatus == CarStatus.TurnOn || carStatus == CarStatus.Stop, "To turn off, your car must be turned on or driving");
    carStatus = CarStatus.TurnOff;
    emit carCurrentStatus(carStatus, uint256(carStatus)));
  }
  
  function CheckStatus() public view returns(CarStatus){
    return carStatus;
  }
}  
```  

</details>  
  
## interface
* interface : 스마트컨트랙 내에서 정의되어야할 필요한 것
1. 함수는 external로 표시
2. enum, structs 가능
3. 변수, 생성자 불가(constructor X)
* 컨트랙트 예제

<details>
  
```
interface ItemInfo{
  struct item{
    string name;
    uint256 price;
  }   
  function addItemInfo(string memory _name, uint256 _price) external;
  function getItemInfo(uint256 _index) external view returns(item memory);
}   
  
//interface의 함수와 리턴값을 선언해줘야하고 override를 전부 붙여줘야함
contract example is ItemInfo{
  item[] public itemList;
  function addItemInfo(string memory _name, uint256 _price) override public{
    itemList.push(item(_name, _price));
  }
  
  function getItemInfo(uint256 _index) override public view returns(item memory){
    return itemList[_index];
  }
}
```
  
</details>

## library 
* library: 기존에 만들던 스마트 컨트랙과 다른 종류의 스마트 컨트랙이라 할 수 있다.

* 라이브러리의 이점
1. 재사용 : 블록체인에 라이브러리가 배포되면, 다른 스마트 컨트랙들에 적용가능.
2. 가스 소비 줄임 : 라이브러리는 재사용가능한 코드, 즉 여러개의 스마트 컨트랙에서 공통으로 쓰이는 코드를 따로 라이브러리 통해서 배포 하기에, 다른 스마트 컨트랙에 명시를 해주는 것이 아니라, 라이브러리를 적용만 하면 되기에 가스 소비량을 줄일 수 있다. 왜냐하면 가스는 스마트 컨트랙의 사이즈/길이에 영향을 많이 받기 때문이다.
3. 데이터 타입 적용: 라이브러리의 기능들은 데이터 타입에 적용할 수 있기에, 좀 더 쉽게 사용할 수 있다.
  
* 제한사항
1. fallback 함수 불가: fallback 함수를 라이브러리 안에 저의를 못하기에, 이더를 갖고 있을 수 없다.
2. 상속 불가
3. payable 함수 정의 불가

<details>
  
```

//오버플로우를 방지하는 스마트 컨트랙트  
library SafeMath{
  function add(uint8 a, uint8 b) internal pure returns(uint8){
    //a:1 b:255 -> a+b=256 -> 오버플로우로 0이됨 < a
    require(a+b >= a, "SafeMath: addition overflow");
    return a+b;
  }  
}
  
contract example{
  using SafeMath for uint8;
  uint8 public a;
  
  function becomeOverflow(uint8 _num1, uint8 _num2) public{
    //a = _num1.add(_num2);
    a = _num1 + _num2;
  }
}
```
  
</details>

  
## import

---------------------------------
[solidity강좌](https://www.youtube.com/channel/UCuTGg-K1DY9cl8YtBKbQR9A)

# solidity정리

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
* public, private, internal, external

* public : 모든 곳에서 접근가능
* external : public처럼 모든곳에서 접근 가능하나, external이 정의된 자기자신 컨트랙 내에서 접근 불가
* private : 오직 private이 정의된 자기 컨트랙에서만 가능(private이 정의된 컨트랙을 상속 받은 자식도 불가능)
* internal : private처럼 오직 internal이 정의된 자기 컨트랙에서만 가능하고, internal이 정의된 컨트랙을 상속

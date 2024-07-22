# 기본 선언
```Solidity
pragma solidity 0.8.20;


contract Hello {
	uint public number;
	uint private secret;

	function setSecret(uint newSecret) public {
		secret = newSecret
	}
}
```
- contract는 다른 프로그래밍 언어의 class와 유사한 것 같다.
- uint는 unsigned int와 같다.
- 접근 제어자가 public이면 자동으로 getter가 생긴다고 한다.
- 함수는 function으로 선언 가능하며, 기본적으로 다른 언어와 비슷하지만 접근제어자가 파라미터 뒤에 온다.
- secret이라는 변수처럼 private으로 선언했어도 off chain(블로체인 밖을 의미 하는듯?), 이더리움 상에서 보았을 때 상태값을 확인할 수 있으므로, 실제로 secret값을 저장해서는 아니된다.

# 해야할 것
```Solidity
contract Hello {
	// 1. Data
	//   * Single
	//   * Multiple
	//   * Complex
	// 2. Actions
	//   * Conditional Statement, Loop
	//   * Function
	//   * Error
	//   * Event(Log)
	//   * Modifier, Library, Contract Inheritance
}
```
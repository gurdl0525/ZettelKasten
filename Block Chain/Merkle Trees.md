블록에 포함된 거래 내역을 트리 형태로 요약한 것을 말한다.

root 노드에 하위 노드 값을 전부 더해서 표기하는 것이 특징
![[머클트리.png|출처: https://jayground8.github.io/what_is_merkle_root/]]

### 장점
노드가 변경되더라도 머클 root값만 보면 판단할 수 있기 때문에 무결성이 보장된다.
![[머클트리-무결성.png|출처: https://jayground8.github.io/what_is_merkle_root/]]

오른쪽 노드에 4가 존재하는 알려면 짝노드와 상위 노드의 짝노드만 알면 검증할 수 있다.
![[머클트리-거래검증.png|출처: https://jayground8.github.io/what_is_merkle_root/]]
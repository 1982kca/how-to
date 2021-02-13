Git이 뭐죠?
===

> **Git (깃)**    
가장 많이 사용되는 분산 버전 관리 시스템

Git에 대해 이해하기 위해서는 **버전 관리 시스템**에 대해 먼저 알아볼 필요가 있다.

버전 관리 시스템 _(VCS; Version Control System)_
---

> 버전 관리 시스템은 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템이다.    
― git-scm.com

어떤 코드를 작성했다가 내용을 수정했는데, 이전에 작성한 코드가 더 좋은 것 같아 돌아가고자 한다면 어떻게 해야 할까?    
다행히 이전 코드를 따로 복사해두었다면 쉽게 복구할 수 있다.    
하지만 매번 수정할 때마다 이전 버전을 따로 남겨두었다가는 저장 공간이 몇 배씩 더 사용될 것이다.

이런 경우에 버전 관리 시스템을 사용했다면 쉽게 이전에 기록해놓은 버전으로 돌아갈 수 있다.    
파일을 따로 복사해둔 것만큼 공간을 차지하지도 않으면서 시간 순서대로 버전 관리가 가능한 것이다!

뿐만 아니라, 다른 사람과 협업을 할 경우에도 전체 파일을 주고 받거나 따로 구현하여 합칠 필요 없이 버전 관리 시스템을 통해 함께 관리할 수 있다.    
구체적인 방식은 중앙집중식 버전 관리 시스템이냐 분산 버전 관리 시스템이냐에 따라 다르지만 말이다.

> **중앙집중식 버전 관리 시스템**    
파일을 관리하는 서버가 별도로 있고 클라이언트가 중앙 서버에서 파일을 받아서 사용하는 방식

중앙 집중식 버전 관리 시스템은 중앙 서버가 모든 파일을 관리한다.    
사용자는 중앙 서버에서 최신 상태의 파일을 내려받아 작업을 하고 다시 중앙 서버에 올린다.    
파일의 특정 버전 상태를 **스냅샷**이라고 부르며 그것을 내려 받는 것을 **체크 아웃**한다고 한다.    
개발 사용자가 가지고 있는 파일은 각자가 수정을 가한 사본이며, 원본에 해당하는 전체 시스템은 중앙 서버에만 존재한다.

그런데 이와 같이 중앙집중식으로 관리할 경우 중앙 서버에 문제가 발생한다면 상황이 복잡해진다.    
중앙 서버에 문제가 발생한 동안 다른 사람과의 협업이 불가능하며 그 동안의 히스토리를 잃을 수도 있고, 복구하지 못할 경우 여러 사용자들의 사본 중 무엇을 새로운 원본으로 삼을지 애매해진다.

이런 문제를 개선하기 위해 나온 게 분산 버전 관리 시스템이다.

> **분산 버전 관리 시스템**    
단순히 파일의 마지막 스냅샷을 체크 아웃 하는 게 아니라 저장소를 히스토리째로 가져와 사용하는 방식

분산 버전 관리 시스템을 사용하면 서버에 문제가 있어도 클라이언트 저장소 중 아무거나 사용하여 복구할 수 있다.    
각각의 클라이언트 저장소에 원본 저장소를 그대로 내려 받으면 그만큼 공간적인 낭비가 발생할 것이라는 우려가 있을 수 있는데, Git의 경우 기존에 저장한 상태에 비해 달라진 게 없는 파일의 경우 해당 파일을 따로 저장하지 않아 작은 메타데이터로 저장소를 관리할 수 있다.

자, 그러면 Git은 어떻게 설치하고 어떻게 사용할 수 있는지 차근차근 알아보자.    
[>>> 01. Git 설치 및 초기 설정](chapter01.md)

---
slug: what-is-good-code
title: What is good code?
authors: derek
tags: [code]
---

## 좋은 코드는 무엇일까

개발자들은 모든 시작은 남의 코드를 읽는것에부터 출발합니다.  
대부분의 경우 이미 회사에 구축되어 있는 소프트웨어가 존재하기 때문이지요.  
회사에서 이미 개발되어 있는 소프트웨어가 규모가 크다면 비슷한 경험을 해보셨을 겁니다.

`남의 코드를 읽기란 쉽지 않다`

<!-- truncate -->

남의 코드는 곧 나의 코드가 되고, 결국 나의 코드 또한 남이 보았을 때 읽기 쉽지 않음을 의미합니다.  
좋은 코드란 사용자의 요구사항을 충족할 수 있으며, 유지보수 할 때에 쉽게 수정 할 수 있는 코드라 생각합니다.

## 좋은 코드를 작성하기 위한 나름의 가이드

### 변수의 최소화

슬랙과 같은 하나의 앱을 웹에서 제공해야 한다면 기능의 복잡도가 상당히 높을 것입니다.  
기능이 추가/수정이 이루어지면 자연스럽게 변수를 추가하게 되고, 추후 각 변수의 역활을 파악하기 힘들것 입니다.  
그렇기 때문에 꼭 필요한 변수인지, 상황에 따라서 줄이거나 추가 할 수 있어야 합니다.

제 경험상 함수 안에서 지역 변수의 개수는 비즈니스 로직을 파악하는데 도움이 될때가 많으나  
`this`로 참조 가능한 클래스 변수인 경우 유지보수 측면에서 부정적인 영향을 끼칠때가 많았습니다.

### 변수명의 길이

각 회사의 개발문화에 따라 다르나, 변수명을 길게 작성하여 최대한 의미를 부여한다고 해도  
변수명만을 가지고 타인이 변수의 목적을 추론하긴 쉽지 않습니다.  
오히려 코드의 길이만 길어져 빠르게 코드를 읽는데 방해가 될때도 있었습니다.  
그렇기에 변수를 의미를 담아 지으되, 14자를 넘어가는건 추천드리지 않습니다.

```ts
const projectJoinMember: string = "user";
// 변수가 프로젝트 컴포넌트 내에 존재한다면 project라는 단어 없이 추론 가능하다
const joinMember: string = "member";
```

### 코드의 흐름

타인이 보았을 때에 코드의 흐름을 파악 할 수 있어야 합니다.  
멋지게 보단 심플하게, 화려하기 보다는 명확하게 보일 때 가독성이 높은 코드입니다.  
아래의 코드를 보았을 때에 순서가 명확히 보이시나요?

물론 실제 회사의 코드는 이것보다 훨씬 플로우가 복잡할 것입니다.  
제 경험상 그럴수록 흐름을 명확하게 보이도록 작성하는 것이 협업 할때에도  
기능을 변경 할때에도 많은 도움이 되었습니다.

```ts
declare function initData(): any;
declare function reqApi(): any;
declare function viewInit(state: any): any;
declare function onEvent(): any;

const data = initData();
const state = reqApi();
viewInit(state);
onEvent();
```
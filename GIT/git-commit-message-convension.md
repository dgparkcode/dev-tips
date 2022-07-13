# Git 커밋 메시지 컨벤션   
개인적으로 사용중인 Git이라면 상관없겠지만, Github에 공개적으로 코드를 게시하거나 회사에서 협업을 하는 경우는 대부분 커밋 메시지 규칙이 존재한다. 나는 대부분의 경우 단독으로 사용해서 크게 생각해본 적이 없는데 많은 사람들이 이 주제를 다루고 있어 정리한다.

<br/>

## Git 커밋 메시지 형식
```
<type>(<option scope>): <subject>

<option body>

<option footer>
```

<br/>

## TYPE
일반적인 타입의 종류이며, 협업하는 그룹에 따라 다르다.   
더 세분화 할 수도 있다. remove, build, plus, minus ...   
대부분 웹 기준으로 작성된 것인지 안드로이드 입장으로 보면 애매하긴 하다.
```
- feat: 새로운 기능 추가
- fix: 버그 수정
- docs: 문서 생성, 수정, 삭제
- style: 코드 포멧팅, 줄바꿈 등 (비즈니스 로직 변화 없음)
- refactor: 리팩토링
- test: 테스트 코드 생성, 수정, 삭제
- chore: 빌드 작업 수정, 기타(.gitignore 같은)
```

<br/>

## SCOPE
주요 변경사항이 무엇인지 대략적으로 알리는 역할인듯 하다. 모듈이 주요 변경사항이면 module, domain, app 뭐 이런식으로 적고, gradle 파일을 주요 수정했으면 gradle 등으로 적으면 될 듯 하다.
```
- app, domain, data, gradle, view, viewmodel ...
```

<br/>

## SUBJECT
한글로 적어라, 영어로 적어라, 소문자로만 적어라, 대문자로만 적어라 등 많은 규칙들이 있다. 일반적으로 50자 내외 정도로 짧게 적으며, 과거시제를 사용하지 않고 명령문으로 적는다.
```
- add user interface (O)
- added user interface (X)
- user interface added (x)
```

<br/>

## BODY
부연설명이 필요한 경우 작성한다. 중요한 것은 '어떻게' 변경했다를 설명하는게 아니라 '왜' 변경했는가를 작성하는 것이다.
```
A를 잘 삭제했습니다. (X)   
A가 더이상 사용되지 않기 때문에 삭제했습니다. (O)
```

<br/>

## FOOTER)
이슈 번호나 close, closes 등을 적으면 자동으로 동작한다는데 아직 안써봐서 모르겠다.    
옵션이기 때문에 대부분 적지 않는다.
```
// TODO: 나중에 필요하면 작성...
```
<br/>

## 샘플
```
feat(project): implement domain layer module

클린 아키텍쳐를 함 해보려고 도메인 모듈을 구현했습니다.
usecase 기준으로 viewmodel에서 처리해야 합니다.
```

<br/>

# 참고
[Git - 커밋 메시지 컨벤션](https://doublesprogramming.tistory.com/256)   
[Conventional Commits 1.0.0-beta.2](https://www.conventionalcommits.org/en/v1.0.0-beta.2/)   
[좋은 git commit 메시지를 위한 영어 사전](https://blog.ull.im/engineering/2019/03/10/logs-on-git.html)
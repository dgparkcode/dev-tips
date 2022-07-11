# Github 여러 계정 사용하기   
한 컴퓨터에서 개인 계정, 회사 계정을 오가며 작업을 해보니 문제가 있다. 회사 프로젝트 저장소인데 개인 계정의 이름으로 커밋이 되거나 혹은 반대로 되는 경우다. 갑자기 push, pull 등이 안되서 확인해보니 잘못된 계정 정보로 해당 작업을 요청하더라.   
매번 계정정보를 설정하거나 초기화 하는 것은 너무너무너무 귀찮다. 그래서 찾아보니 이 문제를 SSH로 해결한 글이 많이 보이길래 정리한다.

<br/>

## SSH 키 생성하기
확장자가 없는 id_rsa 파일은 개인키이고, id_rsa.pub처럼 .pub 확장자가 있는 파일은 공개키이다.
```
$ cd ~/.ssh
$ ssh-keygen -t rsa -C "userA@email.com" -f "id_rsa"
$ ssh-keygen -t rsa -C "company@email.com" -f "id_rsa_company"
$ ls -al ~/.ssh
```

<br/>

## SSH 키 추가하기
개인키를 ssh-agent에 추가한다.
```
$ eval "$(ssh-agent -s)"
$ ssh-add id_rsa_userA
$ ssh-add id_rsa_company
$ ssh-add -l
```

<br/>

## SSH 키 Github에 등록하기
공개키 파일을 열어 내용을 복사해 Github에 등록한다.   
Github 로그인 > Settings > SSH and GPG keys
```
$ code ~/.ssh/id_rsa.pub
$ code ~/.ssh/id_rsa_company.pub
```

<br/>

## SSH Config 설정하기
.ssh 폴더에 config 파일 생성한다.
```
$ cd ~/.ssh
$ code config
```

```
# personal, default
Host github.com
    HostName github.com
    User userA
    IdentityFile ~/.ssh/id_rsa

# company
Host company.github.com
    HostName github.com
    User userB
    IdentityFile ~/.ssh/id_rsa_company
```

<br/>

## SSH 접속 확인하기
'Hi userA! You've successfully authenticated, but GitHub does not provide shell access.' 메시지를 확인한다.
```
$ ssh -T git@github.com
$ ssh -T git@company.github.com
```

<br/>

## SSH 키를 활용해 Git 클론하기   
SSH로 clone 할때 config 파일에 작성했던 host 정보를 이용해 클론한다.
```
$ git clone git@github.com:userA/repository.git
$ git clone git@company.github.com:userB/repository.git
```
<br/>

## 이미 클론한 소스에 적용하기
set-url을 이용해 적용한다.
```
git remote set-url origin git@company.github.com:userB/repository.git
```
<br/>

# 참고
[한 컴퓨터에서 여러 개의 깃허브 계정 사용하기](https://velog.io/@jay/multiplegithubaccounts)   
[A Practical Guide to Managing Multiple GitHub Accounts](https://medium.com/the-andela-way/a-practical-guide-to-managing-multiple-github-accounts-8e7970c8fd46)   
[한 컴퓨터에서 github 계정 여러개 사용하기](https://usingu.co.kr/frontend/git/%ED%95%9C-%EC%BB%B4%ED%93%A8%ED%84%B0%EC%97%90%EC%84%9C-github-%EA%B3%84%EC%A0%95-%EC%97%AC%EB%9F%AC%EA%B0%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0/)
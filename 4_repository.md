# Remote Repository

## 1. Github에서 repository 생성하기

## 2. git push
```cli
$ git remote add origin https://github.com/taehoonkong/git_study.git
$ git remote
$ git push -u origin master /* -u option은 최초에 한번만 사용하면 된다. */
```

## 3. Github과 local 저장소 동기화 하기
```cli
$ git clone https://github.com/taehoonkong/git_study.git git_home
$ git clone https://github.com/taehoonkong/git_study.git git_office
-----home 에서 commit push 후에 office에서-----
$ git pull /* home과 office */ 동기화
```
> remote repository로 push 하기 전 commit에 누락 된 내용이 있다면
> $ git commit --amend

## 4. git pull vs git fetch
보통은 git pull 특수한(정교함이 필요한) 상황에서는 git fetch를 사용

fetch는 remote 의 origin/master 보다 local의 commit이 한단계 뒤쳐지 있기 때문에(file만 다운로드 받음) local과 remote의 diff를 살펴 볼 수 있다.
```cli
$ git fetch
$ git merge origin/master
```

## 5. tag
branch는 commit이 계속 바뀌는 반면에 tag는 commit이 고정된다.
다양한 정보를 포함하기 위해서는 annotated tag를 사용해야 한다.
```cli
$ git tag -a 1.1.0 -m "bug fix"
$ git push --tags
$ git tag -d 1.1.0
```

# Version Control Systems

## GIT 버전 만들기

### 1. git init
VCS가 필요한 프로젝트 폴더에서 git init 명령어를 실행하여 .git 폴더를 생성(삭제에 주의를 요한다.)
```cli
$ mkdir git_study
$ cd git_study
$ git init
```
### 2. git status
> Untracked files : 추적되고 있지 않은 파일
```cli
$ git status
```
### 3. git add(commit 대기상태: stage area)
git에 파일 추적을 요청
```cli
$ git add somefile.txt
```
### 4. git config
git에 사용자 정보를 입력
```cli
$ git config --global user.name taehoonkong
$ git config --global user.email dahlia0111@gmail.com
```
### 5. git commit(commit 하면 repository로 저장)
version? : 의미있는 변화(일련의 작업이 완성되어있는 상태)


commit comment 입력시에 구버전 vim이 열리는 경우
```cli
$ git config --global core.editor "mvim -v"
```

```cli
$ git commit
```
vim editor 에서 comment 입력


버전관리 테스트를 위해서 somefile.txt를 수정 후
```cli
$ git status 
```
> modified: somefile.txt

### 6. git add (변경이력을 관리할떄도 git add를 해주어야 한다.)
```cli
$ git add somefile.txt
$ git commit -m "changed"
$ git status
```

## GIT 변경이력 확인하기

### 1. 차이점 확인
```cli
/* 로그 확인 */
$ git log 

/* 소스 사이의 차이 확인 */
$ git log -p

/* commit에 대한 고유 주소로 확인 */
$ git log #gitId

/* 변경 사항 비교(add와 commit을 하기 전에 마지막으로 확인할 수 있는 기회 제공) */
$ git diff

/* commit에 대한 두개의 고유 주소로 비교 */
$ git diff #gitId1..#gitId2
```

### 2. 과거로 돌아가기

#### 2.1 reset
```cli
$ git reset #gitId --hard(리셋을 원하는 시점의 ID - ID 기준으로 후의 log가 삭제된다.)
```

#### 2.2 revert
reset과 다른점은 단순 삭제가 아니라 commit을 취소하고 새로운 버전을 생성한다는 것이다.

## 명령 빈도와 Documents 참고하기
```cli
$ git commit --help

/* 수정된 파일을 자동으로 add하기 */
$ git commit -a

/* vim 에디터 열지 않고 comment 입력하기 */
$ git commit -m "comment"

/* 복합 사용 */
$ git commit -am "comment2"
```

# Branch

## 1. 분기되는 현상 : branch
한개의 기본 branch에 분기가 발생할때마다 branch를 새로 뻗어나간다.

원본파일을 건드리지 않으면서 새로운 customizing이 필요할 때 이용 될 수 있다.

```cli
$ git branch
* master /* 현재 master branch를 사용하고 있다. */

/* 새로운 branch 생성 */
$ git branch exp
$ git branch
exp
* master

/* branch 변경 */
$ git checkout exp
$ git branch
* exp
master

/* branch 생성과 checkout 동시에 하기 */
$ git checkout -b some_branch

this is shorthand for:
$ git branch some_branch
$ git checkout some_branch
```

## 2. master와 branch의 차이점 확인하기

```cli
/* 단순 log 조회 */
$ git log

/* 저장소에 있는 모든 branch의 log조회  */
$ git log --branches --decorate

/* 그래프 추가 */
$ git log --branches --decorate --graph

/* 그래프 online option(간결하게 표시) */
$ git log --branches --decorate --graph --oneline

/* branch와 branch간의 차이를 비교(순서가 중요) */
$ git log -p master..exp /* master에는 없고 exp에는 있는 것을 표시 */
$ git log -p exp..master /* exp에는 없고 master에는 있는 것을 표시 */
$ git diff master..exp
```

## 3. branch 병합 : merge

```cli
/* exp branch 의 commit을 master로 병합 */
/* 순서 : master로 checkout한 후에 merge한다. */
$ git checkout master
$ git merge exp

/* exp branch를 master branch와 동일하게 하기 */
$ git checkout exp
$ git merge master

/* 필요없어진 exp branch를 제거 */
$ git checkout master
$ git branch -d exp
```

## 4. branch merge 기타

fast-foward : master에서 새로운 branch를 딴 후에 master에서 별도의 commit이 발생하지 않았고, 새로운 branch에서 변경사항 commit후에 master에서 merge를 실행하면 fast-foward 
recursive : master에서 새로운 branch를 딴 후에 master에 변화가 생겼을 경우 새로운 branch에서 변경사항 commit후에 master에서 merge를 실행하면 git이 merge commit을 하게 된다.

## 5. branch 충동해결

```cli
$ git branch exp

/* 두 branch의 파일 이름이 다른 경우 - 문제 없음 */
$ vim master.txt
$ git add master.txt
$ git commit -m "master.txt"
$ git checkout exp
$ vim exp.txt
$ git add exp.txt
$ git commit -m "exp.txt"
$ git checkout master
$ git log --branches --decorate --graph --oneline
$ git merge exp

/* 두 branch에 같은 이름의 파일이 있는 경우 */
$ git checkout exp
$ vim common.txt
$ git add common.txt
$ git commit -m "common.txt"
$ git checkout master
$ git merge exp /* master와 exp branch에 모두 common.txt가 존재하는 상황 */
$ vim common.txt /* 내용 수정 by master */
$ git add common.txt
$ git commit -m "mod common.txt by master"
$ git checkout exp
$ vim common.txt /* 내용 수정 by exp */
$ git add common.txt
$ git commit -m "mod common.txt by exp" /* common.txt를 각각의 branch가 같은 부분을  서로 다르게 수정한 상황 */
$ git checkout master
/* 이 때 merge를 하게 된다면 어떻게 반영될 것인가? */
$ git merge exp
Auto-merging common.txt
CONFLICT (content): Merge conflict in common.txt
Automatic merge failed; fix conflicts and then commit the result
$ vim common.txt /* 충돌난 부분을 사용자가 직접 수정 head가 현재 checkout 되어있는 branch이다. */
$ git add common.txt
$ git commit /* Merge 완료 */
```

## 6. branch stash

branch로 작업을 하다가 해당 branch에서 작업이 완료되지 않은 상태에서 다른 branch에 checkout하여 작업을 하게 되는 경우가 발생했을때 이용한다.

```cli
$ vim f1.txt
$ git add f1.txt
$ git commit "f1.txt"
$ git checkout -b exp
$ vim f1.txt /* f1.txt를 수정중에 master로 checkout 해야 하는 상황이 발생 */ 
$ git stash
$ git status /* 꺠끗함 */
$ git checkout master
-----some process-----
$ git checkout exp
$ git stash apply /* 감춰 두었던 것을 복원시킴 */
$ git stash list /* stash list */
$ git reset --hard HEAD
$ git status
$ git stash list
$ git stash apply
$ git stash drop /* stash의 명시적인 삭제 */
$ git stash pop /* apply와 drop을 동시에 진행 */
```

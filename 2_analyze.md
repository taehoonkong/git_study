# Analyze git

## 1. git add의 원리
* 파일의 생성은 git에 영향을 주지 않는다.
* git add를 실행하면 파일의 주소를 담고있는 index와 내용을 담고 있는 object가 생성된다.
* cp 명령어를 이용하여 파일을 복제하거나 기존의 파일과 동일한 내용의 파일을 생성하면 index에 파일의 주소는 추가되지만 object는 변동이 없다.


## 2. objects 파일명의 원리
* git은 우리가 저장한 파일의 내용을 sha1 이라는 hash 알고리즘을 통과시켜 파일의 이름을 도출한 후에...


## 3. commit의 원리
* commit에 대한 정보도 object에 저장된다.
* commit을 반복하면 tree(이전)와 parent(이후)로 나누어지게 된다.
* 버전이 만들어진 시점에서 프로젝트 폴더의 내용에 대한 상태를 얻어낼 수 있다(snapshot).
* object는 blob(파일의 내용), tree(주소와 blob에 대한 내용), commit으로 구분 할 수 있다.

## 4. status의 원리
* index(stagin area)의 내용과 object의 내용, working directory를 비교하여 수정된 파일을 알려준다.

Git
============

git은 여러 문서 및 파일들의 버전을 관리하기 위한 도구이다.

시작하기
------

최초 설치 후 사용자이름과 이메일주소를 설정해 주어야 한다.  
```bash
git config --global user.name "사용자이름"
git config --global user.email 이메일주소
```
git을 이용할때 cli에서 텍스트 작업을 할 경우가 있다. 그 때 텍스트 편집기를 설정해주어야 한다.
```bash
git config --global core.editor vim
```

git이 버전관리를 시작할 작업공간을 지정해주어야한다.
```bash
git init
```
명령어를 입력한 경로에서 새로운 git의 repository가 시작된다.  

git repository를 생성한 곳에 .git이라는 디렉토리가 생성된 것을 발견할 수 있다.  
.git 디렉토링 안에 버전의 정보들이 기록된다.

git의 상태
-------
git은 3가지의 상태가 존재한다.
- Committed
    - 데이터가 git repository에 안전하게 저장됨
- Modified
    - 수정된 파일이 아직 commit되지 않음
- Staged
    - 수정된 파일을 commit하겠다고 표시함


이 3가지 상태는 3가지 단계와 연결돼 있다.
![area](areas.png)

- Working Directory
    - 현재 작업공간을 의미
- Staging Area
    - commit하겠다고 표시된 파일들의 집합
- Repository
    - commit되어 안전하게 저장된 파일들의 집합


![status](lifecycle.png)
- 최초 생성된 파일들은 git에서 추척하지 않는다
```bash
git add <파일이름>
```
위의 명령어를 사용해 해당 파일을 git이 추적하도록 한다  
다시 추적하지 않도록 하기 위해선
```bash
git rm 파일이름
```
> 단 작업중이던 내용이 사라지기 때문에 사라지게 하지 않기 위해선 `--cached`명령어를 함께 써준다. 
- 추적되고 있는 파일들 중 수정된 파일이 Modified 상태가 된다  
Modified상태가 된 파일들을 위의 `git add` 명령어를 이용해 
Staged상태가 되도록 한다
- Staged에 올라온 파일들을 `git commit` 명령어를 통해 새로운 버전을 만들어 commited상태가 되도록 한다
```
git commit
```
commit 명령어를 입력하면 text편집창이 나타난다. 편집창에서 commit할 새로운 버전의 내용을 작성해 주어야한다. 내용에는 어떤 것을 작업했는지에 대해 알아보기 쉽게 작성하면 된다.

버전의 내용을 commit message라고 하는데
```bash
git commit -m "새로운 버전 내용"
```
으로 text편집창으로 가지 않고 작성할 수 있다.

이렇게 만들어진 버전들은
```
git log
```
명령어를 통해 확인할 수 있다.

`-p` 각 commit들 간의 차이를 보여준다  
`--stat` 어떤 파일이 수정되었는지, 어떤 줄이 수정되었는지에 대한 통계를 보여준다  
`--pretty=oneline` 한줄에 보여준다  
`--graph` 브랜치를 시각적으로 보여준다

`git log`를 통해 얻은 commit id를 이용해 이전 commit들로 이동할 수 있다.

```bash
git checkout <commit id>
```
단순히 이동하는 것이 아닌 이전 커밋으로 되돌아가기 위해선
```bash
git reset --hard <commit id>
```
를 사용하면 현재 작업하는 것을 포기하고 commit id로 되돌아 갈 수 있다.
`--soft`를 사용하면 현재 작업하는 것을 갖고 이전 commit으로 돌아간다.

`git reset`명령어는 git이 갖고있던 commit을 제거하고 되돌아가기 때문에 version을 저장하는 git에게 치명적일 수 있다.
```bash
git revert <commit id>
```
를 사용하면 commit id에서 추가된 내용이 추가되기 이전 commit을 새롭게 commit한다.

이렇게 git을 이용해  
- repository 시작
- commit 생성
- commit 제거
- commit log 보기

등을 할 수 있게 되었다.

# Git

## 시작하기

### 버전 관리란?

- 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템
- 로컬 버전 관리(VCS) -> 중앙 집중식 버전 관리(CVCS) -> __분산 버전 관리 시스템 (DVCS)__

### 짧게 보는 Git의 역사

- 특징
	- 빠른 속도
	- 단순한 구조
	- 비선형적인 개발(수천 개의 동시 다발적인 브랜치)
	- 완벽한 분산
	- Linux 커널 같은 대형 프로젝트에도 유용할 것

### Git 기초

- 데이터를 파일 시스템 스냅샷으로 취급하고 크기가 아주 작다.
- 파일이 달라지지 않으면 파일에 대한 링크만 저장한다.
- 거의 모든 명령이 로컬 파일과 데이터만 사용한다.
- 데이터를 저장하기 전에 항상 체크섬을 구하고 그 체크섬으로 데이터를 관리한다.
- 파일을 Committed, Modified, Staged 과 같은 세 가지 상태로 관리한다.
	- Committed : 데이터가 로컬 데이터베이스에 안전하게 저장 됐다는 것
	- Modified : 수정한 파일을 아직 로컬 데이터베이스에 커밋하지 않을 것
	- Staged : 현재 수정한 파일을 곧 커밋할 것이라고 표시한 상태인 것

### 최소 설정

- 환경 설정을 해줘야 한다. 업그레이드해도 유지된다.
- `git config`으로 내용을 확인하고 변경할 수 있다.
- `--global`으로 공통적인 사용자 정보를 설정할 수 있다.
- `core.editor`으로 해당 설정에 대한 편집기를 변경 할 수 있다.
- `git config --list`으로 설정한 모든 값을 보여준다.

### CLI

### Git 설치하기

- Linux (Fedora)
	```text
	$ sudo yum install git-all
	```
- Linux (Ubuntu)
	```text
	$ sudo apt-get install git-all
	```
- Mac
	- http://git-scm.com/download/mac

- Windows
	1. http://git-scm.com/download/win
	2. http://windows.github.com

## Git 의 기초

### Git 저장소 만들기

- 기존 디렉토리를 Git 저장소로 만들기
	- `git init`
	- .git 이라는 하위 디렉토리 생성

- 기존 저장소를 Clone 하기
	- `git clone [url]`
	- 프로젝트의 히스토리를 전부 받아온다.
	- https, git, ssh 프로토콜 지원

### 수정하고 저장소에 저장하기

- 워킹 디렉토리(Check out 한 디렉토리)의 모든 파을은 크게 Tracked 와 Untracked 로 나뉜다.
	- Tracked : 이미 스냅샷에 포함돼 있던 파일
		- Unmodified : 수정하지 않음
		- Modified : 수정함
		- Staged : 커밋으로 저장소에 기록
	- Untracked : 워킹 디렉토리에 있는 파일 중 스냅샷에도 Staging Area 에도 포함되지 않은 파일

- 파일 상태 확인하기
	- `git status`

- 파일 새로 추적하기
	- `git add {file}`

- Modified 파일 Stage 하기
	- `git add`는 파일을 새로 추적할 떄도 사용하고 수정한 파일을 Staged 만들 때도 사용한다.

- 파일 상태 짧게 확인하기
	- `git status -s` 또는 `git status --short`
	- 새로운 파일은 ?? 표기
	- Staged 상태로 추가한 파일 중 새로 생성한 파일 앞에는 A 표기
	- 수정한 파일 앞에는 M 표

- 파일 무시하기
	- .gitignore 생성
	- 파일 패턴을 적음
		- 빈 라인이나 #으로 시작하는 라인 무시
		- 표준 Glob 패턴 사용

- Staged 와 Unstaged 상태의 변경 내용 보기
	- `git diff`
	- Staging Area 에 넣은 파일의 변경 부분을 보고 싶으면 `git diff --staged`
	- `git diff --staged` 와 `git diff --cached` 동일 옵션

- 변경사항 커밋하기
	- `git commit`
	- 메시지를 인라인 첨부 `git commit -m "{메시지}"`

- Staging Area 생략하기
	- Tracked 상태의 파일을 자동으로 Staging Area에 넣음. `git commit -a`

- 파일 삭제하기
	- Tracked 상태의 파일을 삭제. `git rm`
	- 삭제한 파일은 Staged 상태가 된다.

- 파일 이름 변경하기
	- `git mv {file_from} {file_to}`

### 커밋 히스토리 조회 하기

- `git log`
- SHA-1 체크섬, 저자 이름, 저자 이메일 커밋한 날짜 커밋 메시지 보여줌
- 각 커밋의 diff : `git log -p`
- 각 커밋의 통계 정보 : `git log --stat`
- 히스토리 형식 변경 : `git log --pretty={oneline|short|full|fuller|format}`
	- format 옵션(%H, %h, %T, %t, %P, %p, %an, %ae, %ad, %ar, %cn, %ce, %cd, %cr, %s)
- 브랜치와 머지 히스터리 정보를 아스키 그래프 : `git log --graph`
- 히스토리 갯수 : `git log -{n}`
- 히스토리 시간 : `git log --since | --after` | `git log --until | --before`
	```text
	n주 동안 : {n}.weeks
	절대 날짜 : "2017-08-23"
	상대 날짜 : "2 years 1 day 3 minutes ago"
	```
- 히스토리 저자 : `git log --author`
- 히스토리 키워드 : `git log --grep`

	> 저자와 키워드 모두 만족하는 커밋을 찾으려면 `--all-match` 옵션을 사용

- 히스토리 내용 : `git log --S{word}`

### 되돌리기

- 완료된 커밋 수정 : `git commit --amend`
- 아래 명령어는 하나의 커밋으로 기록
	```text
	$ git commit -m 'initial commit'
	$ git add forgotten_file
	$ git commit --amend
	```
- 파일 Unstage 상태로 변경 : `git reset HEAD {file}`

	> `git reset` 명령은 위험하기 때문에 되도록이면 사용하지 않는다.

- Modified 파일 되돌리기 : `git checkout -- {file}`

	> `git checkout` 명령은 위험하기 때문에 되도록이면 사용하지 않는다.

- Stash와 Branch를 사용하자.

### 리모트 저장소

- 리모트 저장소 확인 : `git remote`
- 단축이름과 URL 포함 : `git remote -v`
- 리모트 저장소 추가 : `git remote add {단축 이름} {url}`
- 리모트 저장소 가져오기(no merge) : `git fetch {단축 이름}`
- 리모트 저장소 가져오기(merge) : `git pull {단축 이름}`
- 리모트 저장소 공유하기 : `git push {단축 이름} {브랜치 이름}`
- 리모트 저장소 살펴보기 : `git remote show {단축 이름}`
- 리모트 저장소 이름 변경 : `git remote rename {단축 이름} {새 단축 이름}`
- 리모트 저장소 삭제 : `git remote remove {단축 이름}` | `git remote rm {단축 이름}`

### 태그

- 태그 조회 : `git tag`
- 태그 조회 (검색 패턴) : `git tag -l "{*word*}"`
- 태그 정보와 커밋 정보 확인 : `git show`
- 태그 붙이기
	1. Lightweight 태그
		- 특정 커밋에 대한 포인터
		- `git tag {tag}`
	2. Annotated 태그
		- 태그 만든 사람 이름, 이메일 등록 날짜 메시지 저장
		- `git tag -a {tag} -m "{message}"`
- 나중에 태그하기 : `git tag -a {tag} {체크섬}`
- 태그 공유하기 : `git push {단축 이름} {tag}`
- 태그 공유하기(복수) : `git push {단축 이름} --tags`

	> `git push` 명령은 자동으로 리모스 서버에 태그를 전송하지 않는다.

- 태그 checkout 하기 : `git checkout -b {new branch name} {tag}`

	> 태그는 브랜치와 달리 머킷을 바꿀 수 없기 때문에 새로운 브랜치를 만들어 작업해야 한다.

### Git Alias

- Git 명령어를 alias로 만들 수 있다.
- 예를 들면, `git commit` 을 `git ci` 로 대체 할 수 있다.
	```text
	$ git config --global alias.co checkout
	$ git config --global alias.br branch
	$ git config --global alias.ci commit
	$ git config --global alias.st status
	```

## Git 브랜치

### 브랜치란 무엇인가?

- 코드를 통째로 복사하고 나서 원래 코드와 상관없이 독립적으로 개발을 진행 하는 것
- Git의 브랜치는 매우 가볍다.
- Git 데이터는 스냅샷을 이용하여 기록한다.
- Git 저장소에 파일을 blob이라고 부른다.
- 브랜치를 만들어 작업하고 Merge 하는 방법을 권장
- Git의 브랜치는 커밋 사이를 가볍게 이동할 수 있는 포인터 같은 것 이다.
- 새 브랜치 생성 : `git branch {name}`
	- 새로 만든 브랜치는 지금 작업하고 있던 마지막 커밋을 가리킨다.
- 현재 작업 중인 브랜치를 가리키는 특수한 포인터인 HEAD가 있다.
	- 브랜치 커밋 내용 확인 : `git log --decorate`
- 브랜치 이동하기 : `git checkout {name}`

### 브랜치와 Merge의 기초

- 브랜치 생성 및 checkout : `git checkout -b {name}`
- 브랜치 삭제 : `git branch -d {name}`
- 브랜치 합침 : `git merge {name}`
- Fast forward 방식 Merge : Merge를 하였으나, Merge 과정 없이 그저 최신 커밋으로 이동
- 3-way Merge : 결과를 별도의 커밋으로 만들어서 가리키도록 이동 (Merge 커밋)
- merge 충돌 시, `git status`명령으로 확인하면 unmerged 상태로 표기
	- `======` 위쪽은 HEAD 내용, 아래쪽은 해당 브랜치 내용
	- `git mergetool`명령으로 충돌 해결
	- 충돌 해결 후, `git commit`에는 해당 내용을 자세헤게 기록된다.

### 브랜치 관리

- 브랜치 목록 : `git branch` (현재 checkout 브랜치는 앞에 * 표기)
- 마지막 커밋 표기 : `git branch -v`
- merge 필터링 : `git branch --(merged|no-merged)`
- 브랜치 강제 삭제 : `git branch -D {name}` (merge 하지 않은 브랜치는 `-d`로 삭제 되지 않는다.)

### 브랜치 워크플로

- 브랜치를 만들고 Merge 하는 Flow 방식(?)
- LongRunning 브랜치
	- 안정적인 `master` 브랜치를 두고 개발 브랜치를 만들어 Merge 하는 방식
	- 규모가 크고 복잡한 프로젝트에 유용
- 토픽 브랜치
	- 프로젝트 크기에 상관없음
	- 한 가지 주제나 작업을 위한 짧은 호흡의 브랜치

### 리모트 브랜치

- 리모트 Refs는 리모트 저장소에 있는 포인터인 레퍼런스이다. (브랜치, 태그 등등)
- 모든 리모트 Refs 조회 : `git ls-remote {branch name}`
- 모든 리모트 브랜치와 그 정보 조회 : `git remote show {branch name}`
- 보통 리모트 Refs보다는 리모트 트래킹 브랜치(리모트 브랜치를 추적하는 브랜치, 일종의 북마크)를 사용한다.
- 리모트 트래킹 브랜치를 로컬 브랜치로 Checkout 하면 자동으로 `트래킹 브랜치`가 만들어진다.
	- 서버 저장소에서 `master` 브랜치를 clone 하면, git에서 `orgin/master`의 트래킹 브랜치인 `master` 브랜치를 만든다.
- 리모트의 특정 브랜치를 추적 : `git branch -(u|set-upstream-to)`
- 추적 브랜치 확인 : `git branch -vv`
- `git pull` = `git fetch` + `git merge`
- 리모트 브랜치 삭제 : `git push {리모트 저장소} --delete {branch name}`

### Rebase 하기

- 브랜치 합치는 방법
	1. Merge
	2. Rebase
- rebase : 한 브랜치에서 변경된 사항을 다른 브랜치로 적용하는 방식
	1. 합칠 브랜치를 어딘가에 임시로 저장해놓는다.
	2. rebase 브랜치가 합칠 브랜치가 가리키는 커밋을 가리키게 한다.
	3. 합칠 브랜치를 Fast forward 시킨다.
- 보다 깔끔한 히스토리
- rebase : `git rebase {베이스 브랜치} {브랜치}`
- 브랜치의 브랜치를 다른 브랜치에 적용시키는 방법 : `git rebase --onto {다른 브랜치} {브랜치} {브랜치의 브랜치}`
- 이미 저장소에 push한 커밋을 rebase하면 안된다.
- rebase한 것을 rebase 하기 : `git pull --rebase`

## Git 서버

### 프로토콜

- 리모트 저장소는 일반적으로 워킹 디렉토리가 없는 Bare 저장소 이다.
	- Bare 저장소 : 일반 프로젝트에서 `.git` 디렉토리만 있는 저장소
- 프로토콜
	- Local, HTTP, SSH, Git 등의 프로토콜 지원
	- 로컬 프로토콜
		- 리모트 저장소가 단순히 디스크의 다른 디렉토리에 존재
		- 파일경로
			1. 직접 쓸 때 : 복사나 하드링크 사용
			2. `file://` : 별도의 프로세스를 생성하여 처리
		- 장점
			1. 간단하다.
			2. 타저장소 가져오기 용이
		- 단점
			1. 디렉토리 공유 불편
			2. 마운트 중에는 빠르지 않다.
			3. 우발적 사고에 보호되지 않는다.
	- HTTP 프로토콜
		- 스마트 HTTP : SSH나 Git 프로토콜처럼 통신
		- 멍청한 HTTP : 원격 저장소를 파일 건네주는 웹 서버로 취급
	- SSH 프로토콜
		- Git의 대표 프로토콜
		- 아무런 외부 도구 없이 Git 서버 구축 가능
		- 장점
			1. 상대적으로 설정이 쉽다.
			2. 보안에 안전하다.
			3. 전송 시, 데이터를 가능한한 압축하기 때문에 효율적이다.
		- 단점
			1. 익명 접근 불가능
	- Git 프로토콜
		- Git에 포함된 데몬을 사용하는 것
		- 9418 포트 사용
		- SSH 프로토콜과 비슷한 서비스 제공(인증 메커니즘 X)
		- 장점
			1. 전송 속도가 가장 빠르다.
		- 단점
			1. 인증 메커니즘이 없다.

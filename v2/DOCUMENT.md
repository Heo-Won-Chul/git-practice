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
	- ```text
		$ sudo yum install git-all
	  ```
- Linux (Ubuntu)
	- ```text
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
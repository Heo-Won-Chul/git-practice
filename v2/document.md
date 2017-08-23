# Git

## 시작하기


### 최소 설정

- 환경 설정을 해줘야 한다. 업그레이드해도 유지된다.
- `git config`으로 내용을 확인하고 변경할 수 있다.
- `--global`으로 공통적인 사용자 정보를 설정할 수 있다.
- `core.editor`으로 해당 설정에 대한 편집기를 변경 할 수 있다.
- `git config --list`으로 설정한 모든 값을 보여준다.

## Git의 기초

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
		
# Ch.11: The Environment (환경)

## 핵심 개념

### 셸 변수 vs 환경변수
- **셸 변수**: `VAR="값"` — 현재 셸에서만 존재
- **환경변수**: `export VAR="값"` — 자식 프로세스에도 전달됨
- **삭제**: `unset VAR`
- **주의**: `=` 앞뒤에 공백 없이! `VAR="값"` ✅ / `VAR = "값"` ❌

### 환경 확인 명령어
- `printenv` — 환경변수 전체 목록
- `printenv HOME` — 특정 환경변수 확인
- `echo $HOME` — 같은 결과
- `set` — 셸 변수 + 환경변수 + 함수 전부 표시
- `export` — export된 변수 목록

### 주요 환경변수
- `HOME` — 홈 디렉토리
- `USER` — 현재 사용자
- `PATH` — 명령어 검색 경로
- `SHELL` — 현재 셸
- `LANG` — 언어/로케일
- `PWD` — 현재 디렉토리
- `EDITOR` — 기본 에디터

### PATH
- 명령어를 찾는 디렉토리 목록 (`:` 구분)
- **왼쪽부터 순서대로** 탐색 → 찾으면 실행, 못 찾으면 `command not found`
- PATH에 추가: `export PATH="$PATH:/새경로"` (뒤에 추가)
- 우선순위 높게: `export PATH="/새경로:$PATH"` (앞에 추가)

### 스타트업 파일
- **로그인 셸**: `/etc/profile` → `~/.bash_profile` (또는 `~/.profile`)
- **비로그인 셸**: `~/.bashrc`
- `.bash_profile`이 보통 `.bashrc`를 호출함 → 결국 둘 다 실행
- 설정 변경 후 적용: `source ~/.bashrc` (= `. ~/.bashrc`)

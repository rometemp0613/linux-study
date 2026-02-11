# 리눅스 명령어 학습 기록

**기반**: "The Linux Command Line" 책 + Udemy 강의 커리큘럼 합집합
**학습 방식**: Claude와 함께 실습 중심 학습
**학습 시작일**: 2026-01-28

---

## 진도 체크리스트

### Part 1: Learning the Shell

- [x] **Ch.1: What Is the Shell? + 유닉스/리눅스 역사**
  - 핵심: 셸 개념, 터미널, bash, 기본 명령어 (date, cal, df, free)
- [x] **Ch.2: Navigation**
  - 핵심: pwd, cd, ls, 절대경로/상대경로
- [x] **Ch.3: Exploring the System**
  - 핵심: ls 옵션들, file, less, 디렉토리 구조
- [x] **Ch.4: Manipulating Files and Directories**
  - 핵심: mkdir, cp, mv, rm, ln, 와일드카드
- [x] **Ch.4.5: 파일명 작명법** *(강의 추가)*
  - 핵심: 좋은 파일명 vs 나쁜 파일명, 공백/특수문자 처리
- [x] **Ch.5: Working with Commands**
  - 핵심: type, which, help, man, apropos, alias
- [x] **Ch.6: Redirection**
  - 핵심: >, >>, <, 2>, 2>&1, |, 표준 입출력/에러
- [x] **Ch.7: Seeing the World as the Shell Sees It**
  - 핵심: 확장 (경로명, 틸드, 중괄호, 산술, 명령어 치환), 따옴표
- [ ] **Ch.8: Advanced Keyboard Tricks**
  - 핵심: 커서 이동, 히스토리, 자동완성, 킬링/yanking
- [ ] **Ch.9: Permissions**
  - 핵심: 읽기/쓰기/실행 권한, chmod, chown, sudo, su
- [ ] **Ch.10: Processes**
  - 핵심: ps, top, jobs, bg, fg, kill, &

### Part 2: Configuration and the Environment

- [ ] **Ch.11: The Environment**
  - 핵심: 환경변수, PATH, export, 스타트업 파일
- [ ] **Ch.12: Nano 에디터** *(강의 추가)*
  - 핵심: nano 기본 사용법, 단축키, 찾기/바꾸기
- [ ] **Ch.13: A Gentle Introduction to vi**
  - 핵심: vi/vim 모드, 기본 편집, 저장/종료
- [ ] **Ch.14: Customizing the Prompt**
  - 핵심: PS1, 이스케이프 코드, 프롬프트 커스터마이징

### Part 3: Common Tasks and Essential Tools

- [ ] **Ch.15: Reading Files** *(강의 추가)*
  - 핵심: cat, less, head, tail, tac, rev, wc, sort
- [ ] **Ch.16: Piping과 tr 명령어** *(강의 추가)*
  - 핵심: 파이프 활용, tr, tee, 여러 파이프 조합
- [ ] **Ch.17: Package Management**
  - 핵심: apt, yum/dnf, 패키지 설치/삭제/업데이트
- [ ] **Ch.18: Storage Media**
  - 핵심: mount, umount, fdisk, 파일시스템
- [ ] **Ch.19: Networking**
  - 핵심: ping, traceroute, netstat, ssh, scp, wget, curl
- [ ] **Ch.20: Searching for Files**
  - 핵심: find, locate, xargs, 타임스탬프 기반 검색
- [ ] **Ch.21: Archiving and Backup**
  - 핵심: tar, gzip, bzip2, zip, rsync
- [ ] **Ch.22: Regular Expressions**
  - 핵심: 기본 정규식, 메타문자, 문자 클래스
- [ ] **Ch.23: grep 완전 정복** *(강의 추가)*
  - 핵심: grep 옵션들, 정규식과 함께 사용, 재귀 검색
- [ ] **Ch.24: Text Processing**
  - 핵심: cut, paste, join, comm, diff, sed, awk
- [ ] **Ch.25: Formatting Output**
  - 핵심: nl, fold, fmt, pr, printf
- [ ] **Ch.26: Printing**
  - 핵심: lpr, lp, a2ps, lpstat, lpq
- [ ] **Ch.27: Compiling Programs**
  - 핵심: gcc, make, Makefile 기초

### Part 4: Writing Shell Scripts

- [ ] **Ch.28: Writing Your First Script**
  - 핵심: shebang, chmod +x, PATH에 추가, 실행
- [ ] **Ch.29: Starting a Project**
  - 핵심: 스크립트 구조, 주석, 변수
- [ ] **Ch.30: Top-Down Design**
  - 핵심: 함수, 지역변수, 모듈화
- [ ] **Ch.31: Flow Control: Branching with if**
  - 핵심: if/elif/else, test, [[ ]], 조건식
- [ ] **Ch.32: Reading Keyboard Input**
  - 핵심: read, 사용자 입력 처리, 유효성 검사
- [ ] **Ch.33: Flow Control: Looping with while/until**
  - 핵심: while, until, break, continue
- [ ] **Ch.34: Troubleshooting**
  - 핵심: 디버깅, set -x, 오류 처리
- [ ] **Ch.35: Flow Control: Branching with case**
  - 핵심: case문, 패턴 매칭
- [ ] **Ch.36: Positional Parameters**
  - 핵심: $0, $1, $#, $@, $*, shift
- [ ] **Ch.37: Flow Control: Looping with for**
  - 핵심: for문, 범위, 배열 순회
- [ ] **Ch.38: Strings and Numbers**
  - 핵심: 문자열 조작, 산술 연산, bc
- [ ] **Ch.39: Arrays**
  - 핵심: 배열 선언, 접근, 순회
- [ ] **Ch.40: Exotica**
  - 핵심: 그룹 명령, 서브쉘, 프로세스 치환
- [ ] **Ch.41: Cron과 자동화** *(강의 추가)*
  - 핵심: crontab, cron 문법, 자동 백업 스크립트

---

## 학습 일지

| 날짜 | 챕터 | 주요 내용 | 비고 |
|------|------|----------|------|
| 2026-01-28 | Ch.1 | 셸 개념, 기본 명령어 (date, cal, df), 단축키 | 완료 |
| 2026-01-30 | Ch.2 | 파일 시스템 트리, pwd, ls, cd, 경로 개념 | 완료 |
| 2026-01-30 | Ch.3 | ls 옵션, file, less, 심볼릭 링크, 디렉토리 구조 | 완료 |
| 2026-01-31 | Ch.4 | mkdir, cp, mv, rm, ln, 와일드카드, 하드/심볼릭 링크 | 완료 |
| 2026-01-31 | Ch.5 | type, which, help, man, apropos, alias | 완료 |
| 2026-01-31 | - | 커리큘럼 보충 (강의 내용 합집합) | 완료 |
| 2026-02-07 | Ch.6 | 리다이렉션(>, >>, 2>, &>), 파이프(\|), tee, /dev/null | 완료 |
| 2026-02-12 | Ch.4.5 | 파일명 규칙, 공백/특수문자 처리, YYYY-MM-DD 날짜 형식 | 완료 |
| 2026-02-12 | Ch.7 | 확장 7종류, $()와 $(()) 차이, 따옴표(큰/작은/이스케이프) | 완료 |

---

## 진행 현황

- **총 챕터**: 41개
- **완료**: 8개
- **진행률**: 20%

---

## 디렉토리 구조

```
study/linux/
├── README.md              # 진도 체크리스트 (현재 파일)
├── CLAUDE.md              # Claude 학습 지침서
├── notes/                 # 챕터별 학습 노트
│   ├── part1-learning-the-shell/
│   ├── part2-configuration-and-environment/
│   ├── part3-common-tasks/
│   └── part4-writing-shell-scripts/
└── logs/                  # 날짜별 학습 일지
```

---

## GitHub 저장소

**URL**: https://github.com/rometemp0613/linux-study

### 학습 후 반드시 실행할 것

```bash
cd "/Volumes/Extreme SSD/study/linux"
git add -A
git commit -m "docs: 학습 내용 추가"
git push
```

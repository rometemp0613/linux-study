# Chapter 5: Working with Commands

## 핵심 명령어

| 명령어 | 기능 |
|--------|------|
| `type` | 명령어 종류 확인 |
| `which` | 실행 파일 경로 |
| `help` | 쉘 내장 명령어 도움말 |
| `man` | 매뉴얼 페이지 |
| `whatis` | 한 줄 설명 |
| `apropos` | 키워드로 명령어 검색 |
| `alias` | 별칭 만들기 |
| `unalias` | 별칭 삭제 |

---

## 명령어의 4가지 종류

| 종류 | 설명 | 예시 |
|------|------|------|
| 실행 파일 | 컴파일된 프로그램 | `/usr/bin/ls` |
| 쉘 내장 | 쉘에 내장됨 | `cd`, `exit` |
| 쉘 함수 | 스크립트로 정의 | 사용자 정의 |
| 별칭 (alias) | 다른 명령어의 별명 | `ll` → `ls -l` |

### 실행 파일 vs 내장 명령어

| | 실행 파일 | 내장 명령어 |
|---|----------|-------------|
| 위치 | `/bin`, `/usr/bin` 등 디스크에 파일로 존재 | 쉘 프로그램 안에 포함 |
| 확인 방법 | `which`, `man` | `help` |
| 속도 | 상대적으로 느림 (파일 읽어야 함) | 빠름 |
| 예시 | `cp`, `ls`, `grep` | `cd`, `exit`, `alias` |

### 왜 내장 명령어가 필요할까?

`cd`가 대표적인 예:

```bash
cd /home/user
```

`cd`는 **현재 쉘의 디렉토리를 바꿔야 함**. 만약 `cd`가 외부 실행 파일이면, 새로운 프로세스가 생기고 그 프로세스의 디렉토리만 바뀌고 끝나버림. 원래 쉘은 그대로.

그래서 `cd`는 쉘 안에 내장되어 있어야만 함.

---

## type - 명령어 종류 확인

```bash
type cd        # cd is a shell builtin
type cp        # cp is /bin/cp
type ll        # ll is an alias for ls -l
```

| 옵션 | 의미 |
|------|------|
| `-a` | 같은 이름의 모든 명령어 표시 |
| `-t` | 종류만 출력 (alias, builtin, file 등) |

---

## which - 실행 파일 경로

```bash
which cp       # /bin/cp
which cd       # (출력 없음 - 내장 명령어라서)
```

| 옵션 | 의미 |
|------|------|
| `-a` | 같은 이름의 모든 실행 파일 표시 |

**참고**: 쉘 내장 명령어는 파일이 아니므로 which로 찾을 수 없음

---

## 도움말 보기

### help - 쉘 내장 명령어용

```bash
help cd
help exit
```

쉘 내장 명령어 전용. 실행 파일에는 사용 불가.

### man - 매뉴얼 페이지

```bash
man cp         # cp 매뉴얼 (q로 나가기)
man 5 passwd   # 섹션 5의 passwd 문서
```

| 옵션 | 의미 |
|------|------|
| `-k` | 키워드 검색 (apropos와 동일) |
| 섹션 번호 | 특정 섹션 보기 |

### man 섹션 번호

| 번호 | 내용 |
|------|------|
| 1 | 사용자 명령어 |
| 2 | 시스템 콜 |
| 3 | 라이브러리 함수 |
| 4 | 특수 파일 |
| 5 | 파일 형식 |
| 6 | 게임 |
| 7 | 기타 |
| 8 | 시스템 관리 명령어 |

### whatis - 한 줄 설명

```bash
whatis ls      # ls (1) - list directory contents
whatis cp      # cp (1) - copy files and directories
```

### apropos - 키워드로 검색

명령어 이름이 기억나지 않을 때, 키워드로 관련 명령어를 찾을 수 있음.

```bash
apropos copy
# 결과 예시:
# cp (1)       - copy files and directories
# dd (1)       - convert and copy a file
# install (1)  - copy files and set attributes
```

```bash
apropos delete   # 삭제 관련 명령어 검색
apropos network  # 네트워크 관련 명령어 검색
```

### man -k

`apropos`와 완전히 동일한 기능.

```bash
man -k copy      # apropos copy와 같음
```

`-k`는 keyword의 약자.

---

## alias - 별칭 만들기

```bash
alias                        # 현재 별칭 전체 보기
alias ll='ls -l'             # 별칭 생성
alias la='ls -la'
unalias ll                   # 별칭 삭제
```

### 예시

```bash
alias study='cd ~/ssd/linux\ 공부'
alias ..='cd ..'
alias ...='cd ../..'
```

**주의**: 터미널 종료 시 사라짐. 영구 저장은 Chapter 11에서 학습.

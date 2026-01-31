# The Linux Command Line 학습 기록

**책**: The Linux Command Line: A Complete Introduction (2019, 2nd Edition)
**저자**: William E. Shotts Jr.
**학습 시작일**: 2026-01-28

---

## 진도 체크리스트

### Part 1: Learning the Shell
- [x] Chapter 1: What Is the Shell?
- [x] Chapter 2: Navigation
- [x] Chapter 3: Exploring the System
- [x] Chapter 4: Manipulating Files and Directories
- [x] Chapter 5: Working with Commands
- [ ] Chapter 6: Redirection
- [ ] Chapter 7: Seeing the World as the Shell Sees It
- [ ] Chapter 8: Advanced Keyboard Tricks
- [ ] Chapter 9: Permissions
- [ ] Chapter 10: Processes

### Part 2: Configuration and the Environment
- [ ] Chapter 11: The Environment
- [ ] Chapter 12: A Gentle Introduction to vi
- [ ] Chapter 13: Customizing the Prompt

### Part 3: Common Tasks and Essential Tools
- [ ] Chapter 14: Package Management
- [ ] Chapter 15: Storage Media
- [ ] Chapter 16: Networking
- [ ] Chapter 17: Searching for Files
- [ ] Chapter 18: Archiving and Backup
- [ ] Chapter 19: Regular Expressions
- [ ] Chapter 20: Text Processing
- [ ] Chapter 21: Formatting Output
- [ ] Chapter 22: Printing
- [ ] Chapter 23: Compiling Programs

### Part 4: Writing Shell Scripts
- [ ] Chapter 24: Writing Your First Script
- [ ] Chapter 25: Starting a Project
- [ ] Chapter 26: Top-Down Design
- [ ] Chapter 27: Flow Control: Branching with if
- [ ] Chapter 28: Reading Keyboard Input
- [ ] Chapter 29: Flow Control: Looping with while / until
- [ ] Chapter 30: Troubleshooting
- [ ] Chapter 31: Flow Control: Branching with case
- [ ] Chapter 32: Positional Parameters
- [ ] Chapter 33: Flow Control: Looping with for
- [ ] Chapter 34: Strings and Numbers
- [ ] Chapter 35: Arrays
- [ ] Chapter 36: Exotica

---

## 학습 일지

| 날짜 | 챕터 | 주요 내용 | 비고 |
|------|------|----------|------|
| 2026-01-28 | Ch.1 | 셸 개념, 기본 명령어 (date, cal, df), 단축키 | 완료 |
| 2026-01-30 | Ch.2 | 파일 시스템 트리, pwd, ls, cd, 경로 개념 | 완료 |
| 2026-01-30 | Ch.3 | ls 옵션, file, less, 심볼릭 링크, 디렉토리 구조 | 완료 |
| 2026-01-31 | Ch.4 | mkdir, cp, mv, rm, ln, 와일드카드, 하드/심볼릭 링크 | 완료 |
| 2026-01-31 | Ch.5 | type, which, help, man, apropos, alias | 완료 |

---

## 디렉토리 구조

```
linux 공부/
├── README.md              # 진도 체크리스트 (현재 파일)
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

학습 내용을 추가하거나 수정한 후에는 아래 명령어를 실행해서 GitHub에 업로드해야 합니다.

```bash
cd "/Volumes/Extreme SSD/linux 공부"
git add -A
git commit -m "docs: 학습 내용 추가"
git push
```

### 다른 컴퓨터에서 받아오기

```bash
git clone https://github.com/rometemp0613/linux-study.git
```

### 최신 내용 동기화

```bash
git pull
```

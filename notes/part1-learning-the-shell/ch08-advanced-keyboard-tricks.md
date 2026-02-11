# Ch.8: Advanced Keyboard Tricks (키보드 고급 트릭)

## 커서 이동

| 단축키 | 동작 |
|--------|------|
| `Ctrl-A` | 줄 맨 앞으로 |
| `Ctrl-E` | 줄 맨 끝으로 |
| `Ctrl-B` / `Ctrl-F` | 한 글자 뒤로 / 앞으로 |
| `Alt-B` / `Alt-F` | 한 단어 뒤로 / 앞으로 |

> A = 알파벳 처음, E = End

## 텍스트 편집

| 단축키 | 동작 |
|--------|------|
| `Ctrl-D` | 커서 위치 글자 삭제 |
| `Ctrl-T` | 커서 앞 두 글자 교환 |
| `Alt-T` | 커서 앞 두 단어 교환 |
| `Alt-L` / `Alt-U` | 소문자 / 대문자로 변환 |

## Kill & Yank (잘라내기 & 붙여넣기)

| 단축키 | 동작 |
|--------|------|
| `Ctrl-K` | 커서 → 줄 끝까지 kill |
| `Ctrl-U` | 커서 → 줄 처음까지 kill |
| `Alt-D` | 커서 → 단어 끝까지 kill |
| `Alt-Backspace` | 커서 → 단어 처음까지 kill |
| `Ctrl-Y` | 마지막 kill한 텍스트 yank (붙여넣기) |

## 자동완성 (Tab)

```bash
ls /etc/ho[Tab]       # → ls /etc/hostname (파일명 완성)
sys[Tab][Tab]         # → sys로 시작하는 명령어 목록
echo $HO[Tab]         # → echo $HOME (변수 완성)
```

- Tab 1번: 자동완성
- Tab 2번: 후보 목록 표시

## 히스토리

| 단축키/명령어 | 동작 |
|--------------|------|
| `↑` / `Ctrl-P` | 이전 명령어 |
| `↓` / `Ctrl-N` | 다음 명령어 |
| `Ctrl-R` | 역방향 검색 (가장 유용!) |
| `Ctrl-G` / `Ctrl-C` | 검색 취소 |
| `history` | 전체 히스토리 보기 |
| `history \| grep ssh` | 특정 명령어 검색 |

### 히스토리 확장

```bash
!!        # 직전 명령어 재실행
!123      # 히스토리 123번 재실행
!ssh      # ssh로 시작하는 마지막 명령어 재실행
sudo !!   # 직전 명령어를 sudo로 재실행 (실전에서 자주 씀)
```

## 기타

| 단축키 | 동작 |
|--------|------|
| `Ctrl-L` | 화면 지우기 (= clear) |
| `Ctrl-C` | 현재 명령 취소 |
| `Ctrl-D` | EOF 전송 (빈 줄에서 셸 종료) |

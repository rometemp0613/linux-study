# Ch.12: Nano 에디터

## 기본 사용법

- `nano filename` — 파일 열기 (없으면 새로 만들기)
- `nano +10 filename` — 10번째 줄에서 열기
- `nano -l filename` — 줄 번호 표시하며 열기
- `sudo nano /etc/hosts` — 관리자 권한으로 수정

## 핵심 단축키

`^` = Ctrl 키

### 저장 & 종료
- `Ctrl+O` → Enter — 저장 (Write Out)
- `Ctrl+X` — 나가기 (Exit)
- `Ctrl+X` → `Y` → Enter — 저장하고 나가기

### 편집
- `Ctrl+K` — 현재 줄 잘라내기 (Kill)
- `Ctrl+U` — 붙여넣기 (Uncut)
- `Ctrl+6` — 선택 시작 → 커서 이동 → Ctrl+K로 잘라내기
- `Alt+6` — 선택 영역 복사

### 이동
- `Ctrl+A` / `Ctrl+E` — 줄 맨 앞 / 맨 끝
- `Ctrl+Y` / `Ctrl+V` — 페이지 위 / 아래
- `Ctrl+_` — 특정 줄 번호로 이동

### 찾기 & 바꾸기
- `Ctrl+W` — 찾기 (Where is)
- `Alt+W` — 다음 검색 결과
- `Ctrl+\` — 찾아 바꾸기 (Y=하나씩, A=전부)

### 기타
- `Ctrl+G` — 도움말
- `Ctrl+C` — 현재 커서 위치 확인

## bash Kill/Yank과 비교

| nano | bash | 동작 |
|------|------|------|
| Ctrl+K | Ctrl+K | 잘라내기 |
| Ctrl+U | Ctrl+Y | 붙여넣기 (키가 다름 주의!) |

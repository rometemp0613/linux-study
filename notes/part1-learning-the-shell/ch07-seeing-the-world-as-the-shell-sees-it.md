# Ch.7: Seeing the World as the Shell Sees It (셸의 눈으로 세상 보기)

## 확장(Expansion)이란?

셸은 명령어를 바로 실행하지 않고, 특수 문자를 먼저 해석/변환한 뒤 실행한다.

```
너의 입력 → [셸의 확장 처리] → 실제 실행되는 명령어
```

## 확장의 종류

### 1. 경로명 확장 (Pathname Expansion)
```bash
echo *.txt        # .txt로 끝나는 파일들
echo .[!.]*       # 숨김 파일들 (.과 ..은 제외)
```

### 2. 틸드 확장 (Tilde Expansion)
```bash
echo ~            # /home/사용자명
echo ~root        # /root
```

### 3. 산술 확장 (Arithmetic Expansion)
```bash
echo $((2 + 2))       # 4
echo $((100 / 3))     # 33 (정수만)
echo $((5**2))        # 25 (거듭제곱)
echo $((11 % 3))      # 2 (나머지)
```

### 4. 중괄호 확장 (Brace Expansion)
```bash
echo {A,B,C}-file     # A-file B-file C-file
echo file-{1..5}      # file-1 file-2 file-3 file-4 file-5
echo {01..10}         # 01 02 03 ... 10 (제로패딩)

# 실전 활용
mkdir -p project/{src,docs,tests}
cp config.yml{,.bak}  # → cp config.yml config.yml.bak
```

**주의: 쉼표 뒤에 공백 넣으면 안 됨!**
```bash
echo {a, b}    # ❌ 확장 안 됨
echo {a,b}     # ✅ 확장됨
```

### 5. 매개변수 확장 (Parameter Expansion)
```bash
echo $USER    # 현재 사용자명
echo $HOME    # 홈 디렉토리
echo $PATH    # 실행 경로
```

### 6. 명령어 치환 (Command Substitution)
```bash
echo "오늘: $(date +%Y-%m-%d)"
file_list=$(ls /usr)
```

### 7. 단어 분리 (Word Splitting)
```bash
name="hello world"
touch $name       # "hello"와 "world" 두 파일 생성!
touch "$name"     # "hello world" 한 파일 생성
```

## $()와 $(())의 차이

| 문법 | 이름 | 용도 | 예시 |
|------|------|------|------|
| `$()` | 명령어 치환 | 명령어를 실행하고 그 **출력 결과**로 대체 | `$(date)` → `2026-02-12` |
| `$(())` | 산술 확장 | 수학 **계산 결과**로 대체 | `$((2+3))` → `5` |

```bash
# $() - 명령어를 실행해서 출력을 가져옴
echo "사용자: $(whoami)"        # → 사용자: ihyejun
echo "파일 수: $(ls | wc -l)"   # → 파일 수: 10

# $(()) - 수학 계산만 함
echo "합계: $((100 + 200))"     # → 합계: 300
echo "나눗셈: $((10 / 3))"     # → 나눗셈: 3

# 헷갈리지 말 것!
echo $(date)     # ✅ date 명령어 실행
echo $((date))   # ❌ date를 숫자로 계산하려고 함 → 에러
```

## 따옴표 (Quoting)

### 큰따옴표 `" "` - $ 계열 확장만 허용
```bash
echo "사용자: $USER"          # 변수 확장 O
echo "날짜: $(date)"          # 명령어 치환 O
echo "합계: $((1+2))"         # 산술 확장 O
echo "*.txt"                   # 경로명 확장 X → 그대로 출력
echo "{a,b}"                   # 중괄호 확장 X → 그대로 출력
```

### 작은따옴표 `' '` - 모든 확장 차단
```bash
echo '$USER'       # → $USER
echo '$(date)'     # → $(date)
```

### 이스케이프 `\` - 한 글자만 보호
```bash
echo "가격: \$100"    # → 가격: $100
```

## 따옴표별 확장 동작 정리

| 확장 종류 | 따옴표 없음 | `" "` | `' '` |
|-----------|:-----------:|:-----:|:-----:|
| 경로명 `*` `?` | O | X | X |
| 틸드 `~` | O | X | X |
| 중괄호 `{a,b}` | O | X | X |
| 산술 `$(())` | O | O | X |
| 매개변수 `$변수` | O | O | X |
| 명령어 치환 `$()` | O | O | X |
| 단어 분리 | O | X | X |

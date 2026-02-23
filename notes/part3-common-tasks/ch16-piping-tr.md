# Ch.16: Piping과 tr

## tr - 문자 변환/삭제

표준 입력을 받아 문자를 **문자 단위로** 변환하거나 삭제. 파일을 직접 읽지 못함 — 반드시 파이프(`|`) 또는 리다이렉션(`<`)으로 입력.

### 기본 사용법 (변환)

```bash
echo "hello" | tr 'a-z' 'A-Z'       # → HELLO (소문자→대문자)
echo "hello world" | tr ' ' '_'      # → hello_world (공백→밑줄)
echo "abc" | tr 'abc' 'xyz'          # → xyz (문자 1:1 매핑)
```

### tr -d (삭제)

지정한 문자를 **삭제**. `-d` 없이 쓰면 변환이지 삭제가 아님!

```bash
echo "hello123world456" | tr -d '0-9'   # → helloworld (숫자 삭제)
echo "h e l l o" | tr -d ' '            # → hello (공백 삭제)
```

### tr -s (squeeze, 압축)

연속된 중복 문자를 **하나로** 압축.

```bash
echo "hello     world" | tr -s ' '    # → hello world (연속 공백 → 하나)
echo "aaabbbccc" | tr -s 'abc'         # → abc
```

### 문자 클래스 (Character Classes)

범위 대신 표준화된 클래스 사용 가능:

| 클래스 | 의미 |
|--------|------|
| `[:lower:]` | 소문자 (a-z) |
| `[:upper:]` | 대문자 (A-Z) |
| `[:digit:]` | 숫자 (0-9) |
| `[:space:]` | 공백 문자 (스페이스, 탭, 개행 등) |
| `[:punct:]` | 구두점 |

```bash
echo "Hello World 123" | tr '[:lower:]' '[:upper:]'   # → HELLO WORLD 123
echo "Hello World 123" | tr -d '[:digit:]'             # → Hello World
```

## tee - T자 파이프 (이중 출력)

파이프 흐름을 유지하면서 **동시에 파일에도 저장**. 배관의 T자 연결부처럼 흐름을 두 갈래로 나눔.

```
         ┌──→ 파일 (file)
입력 → tee
         └──→ stdout (다음 파이프 또는 화면)
```

### 기본 사용법

```bash
ls -l | tee output.txt                      # 화면에 출력 + 파일에 저장
cat data.txt | sort | tee sorted.txt | head -5   # 파이프 중간에서 저장
```

### tee -a (append 모드)

기본적으로 tee는 파일을 **덮어쓰기**(`>`처럼). `-a`를 쓰면 **추가**(`>>`처럼).

```bash
echo "새 로그" | tee -a log.txt    # 기존 내용 유지하면서 추가
```

### tee vs `>` 리다이렉션 차이

- `>`: 출력이 파일로만 감 (화면에 안 나옴)
- `tee`: 파일에도 가고, 화면(stdout)에도 감 → 파이프 체인 중간에 사용 가능

## uniq - 중복 제거

**반드시 sort 후에 사용** — **인접한** 중복만 제거하기 때문.

```bash
sort list.txt | uniq        # 중복 제거
sort list.txt | uniq -c     # 중복 횟수 표시
sort list.txt | uniq -d     # 중복된 항목만 출력
sort list.txt | uniq -u     # 유일한 항목만 출력 (1번만 나온 것)
```

### uniq 옵션 정리

| 옵션 | 의미 | 출력 대상 |
|------|------|----------|
| (없음) | 중복 제거 | 모든 항목 (중복은 1개로) |
| `-c` | count | 모든 항목 + 횟수 |
| `-d` | duplicated | 2번 이상 나온 것만 |
| `-u` | unique | 정확히 1번만 나온 것만 |

### sort -u vs sort | uniq

- `sort -u`: 중복 제거 + 정렬을 한 번에 (단순 중복 제거만 필요할 때)
- `sort | uniq -c`: 빈도 분석이 필요하면 반드시 이 조합 사용 (`sort -u`로는 횟수를 셀 수 없음)

## 파이프 조합 실전

### 기본 패턴

```bash
# 에러 줄 수 세기
grep "ERROR" app.log | wc -l

# 파일명 대문자로 출력
ls | tr 'a-z' 'A-Z'

# CSV 특정 열 빈도 분석
cut -d',' -f2 data.csv | sort | uniq -c | sort -rn
```

### 단어 빈도 분석 파이프라인 (단계별 해설)

```bash
cat book.txt | tr 'A-Z' 'a-z' | tr -s ' ' '\n' | sort | uniq -c | sort -rn | head -10
```

| 단계 | 명령어 | 역할 |
|------|--------|------|
| 1 | `cat book.txt` | 파일 읽기 |
| 2 | `tr 'A-Z' 'a-z'` | 대문자→소문자 통일 |
| 3 | `tr -s ' ' '\n'` | 공백→줄바꿈 (단어별 한 줄) |
| 4 | `sort` | 알파벳 정렬 (uniq 전 필수!) |
| 5 | `uniq -c` | 각 단어 등장 횟수 |
| 6 | `sort -rn` | 횟수 기준 내림차순 정렬 |
| 7 | `head -10` | 상위 10개만 |

### 가장 많이 쓴 명령어 top 5

```bash
history | tr -s ' ' | cut -d' ' -f3 | sort | uniq -c | sort -rn | head -5
```

## 유닉스 철학

> "한 가지 일을 잘하는 작은 프로그램들을, 파이프로 조합한다."

각 명령어(tr, sort, uniq, head 등)는 단순하지만, 파이프로 연결하면 복잡한 작업도 가능.

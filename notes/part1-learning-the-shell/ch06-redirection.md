# Chapter 6: Redirection

## 표준 스트림 (Standard Streams)

| 이름 | fd | 기본 연결 | 설명 |
|------|-----|----------|------|
| stdin | 0 | 키보드 | 프로그램에 들어오는 데이터 |
| stdout | 1 | 화면 | 정상 결과 출력 |
| stderr | 2 | 화면 | 에러 메시지 출력 |

stdout과 stderr는 둘 다 화면에 나오지만 **서로 다른 통로**임.

---

## 리다이렉션 기호 총정리

| 기호 | 의미 | 예시 |
|------|------|------|
| `>` | stdout → 파일 (덮어쓰기) | `ls > file.txt` |
| `>>` | stdout → 파일 (이어쓰기) | `echo "hi" >> file.txt` |
| `<` | 파일 → stdin | `cat < file.txt` |
| `2>` | stderr → 파일 | `cmd 2> error.txt` |
| `> file 2>&1` | stdout + stderr → 파일 | 순서 중요! |
| `&>` | stdout + stderr → 파일 (축약) | `cmd &> all.txt` |
| `\|` | stdout → 다음 명령어의 stdin | `ls \| grep zip` |

---

## 출력 리다이렉션: `>` vs `>>`

```bash
echo "AAA" > file.txt    # file.txt = "AAA" (덮어쓰기)
echo "BBB" > file.txt    # file.txt = "BBB" (AAA 사라짐!)
echo "CCC" >> file.txt   # file.txt = "BBB\nCCC" (이어쓰기)
```

- `>` 는 **무조건 덮어쓰기** — 기존 내용 삭제
- `>>` 는 **이어쓰기** — 기존 내용 뒤에 추가
- `> file.txt` 만 쓰면 파일 내용을 비울 수 있음

---

## 에러 리다이렉션: `2>`

```bash
ls /없는폴더 2> error.txt       # stderr만 파일로
ls /usr/bin /없는폴더 > ok.txt 2> err.txt  # 따로따로
```

---

## `2>&1` — 순서가 핵심!

`2>&1`의 의미: "stderr를 stdout이 **지금 현재** 가리키는 곳으로 보내라"

### `> file 2>&1` (올바른 순서)

```
① > file      → stdout을 파일로 변경
② 2>&1        → stderr를 stdout이 가는 곳(파일)으로 → 둘 다 파일!
```

### `2>&1 > file` (의도와 다른 결과)

```
① 2>&1        → stderr를 stdout이 가는 곳(화면)으로 → 변화 없음
② > file      → stdout만 파일로 변경 → stderr는 여전히 화면!
```

**결론**: 항상 `> file 2>&1` 순서로 쓰거나, 간단하게 `&>` 사용

---

## `/dev/null` — 블랙홀

```bash
ls /없는폴더 2> /dev/null    # 에러 메시지 숨기기
```

여기로 보내면 그냥 사라짐. 에러를 무시하고 싶을 때 사용.

---

## 파이프: `|`

명령어의 stdout을 다음 명령어의 stdin으로 연결.

```bash
ls /usr/bin | wc -l              # 파일 개수 세기
ls /usr/bin | sort | head -10    # 정렬 후 앞 10개
ls /usr/bin | grep zip           # "zip" 포함된 것 찾기
ls /usr/bin | sort | uniq | wc -l  # 중복 제거 후 개수
```

---

## 유용한 명령어

| 명령어 | 역할 | 예시 |
|--------|------|------|
| `cat` | 파일 내용 출력 / 합치기 | `cat a.txt b.txt > merged.txt` |
| `sort` | 정렬 | `sort file.txt` |
| `uniq` | 연속된 중복 제거 | `sort data.txt \| uniq` |
| `wc` | 줄/단어/바이트 수 | `wc -l file.txt` |
| `grep` | 패턴 검색 | `grep "error" log.txt` |
| `head` | 앞부분 보기 | `head -5 file.txt` |
| `tail` | 뒷부분 보기 | `tail -5 file.txt` |
| `tee` | 화면 + 파일 동시 출력 | `ls \| tee output.txt` |

### tee 사용법

```bash
ls /usr/bin | tee allfiles.txt | grep zip
```

- `tee`는 파일명을 **인자로** 받음 (`>` 아님!)
- 화면 출력 + 파일 저장 동시에 처리

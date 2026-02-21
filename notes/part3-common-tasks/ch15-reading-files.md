# Ch.15 Reading Files

## 파일 전체 출력

### cat (concatenate)
```bash
cat filename          # 파일 내용 출력
cat -n filename       # 줄 번호 붙여서 출력
cat -A filename       # 숨겨진 문자(탭, 줄끝) 표시
cat file1 file2       # 여러 파일 이어서 출력
```

### tac (cat 거꾸로)
```bash
tac filename          # 마지막 줄부터 첫 줄 순서로 출력
```

### rev (줄 안의 글자 반전)
```bash
rev filename          # 각 줄의 문자 순서를 뒤집음
echo "hello" | rev    # olleh
```

> tac = 줄 순서 뒤집기, rev = 글자 순서 뒤집기

## 부분 출력

### head
```bash
head filename         # 처음 10줄 (기본값)
head -n 5 filename    # 처음 5줄
head -n -3 filename   # 마지막 3줄 제외한 전부
```

### tail
```bash
tail filename         # 마지막 10줄 (기본값)
tail -n 5 filename    # 마지막 5줄
tail -n +3 filename   # 3번째 줄부터 끝까지
tail -f logfile       # 실시간 모니터링 (follow)
```

> `tail -f`는 서버 로그 모니터링의 필수 명령어!

## 페이지 단위 읽기

### less
```bash
less filename
```

| 키 | 동작 |
|----|------|
| Space / f | 다음 페이지 |
| b | 이전 페이지 |
| /검색어 | 앞으로 검색 |
| ?검색어 | 뒤로 검색 |
| n / N | 다음/이전 검색 결과 |
| g / G | 파일 처음/끝 |
| q | 종료 |

## 파일 통계

### wc (Word Count)
```bash
wc filename           # 줄 수  단어 수  바이트 수  파일명
wc -l filename        # 줄 수만
wc -w filename        # 단어 수만
wc -c filename        # 바이트 수만
wc -m filename        # 문자 수 (멀티바이트 지원)
```

## 정렬

### sort
```bash
sort filename         # 알파벳 순 정렬
sort -r filename      # 역순 정렬
sort -n filename      # 숫자 기준 정렬 (문자열이면 1, 10, 2 순서가 됨!)
sort -k 2 filename    # 2번째 필드 기준 정렬
sort -t ',' -k 3 f.csv  # 콤마 구분, 3번째 필드 기준
sort -u filename      # 정렬 + 중복 제거
```

## 팁: Useless Use of Cat

```bash
# 나쁜 예 (불필요한 프로세스)
cat file | head -3

# 좋은 예 (직접 파일명 전달)
head -3 file
```

# Ch.16: Piping과 tr

## tr - 문자 변환/삭제

표준 입력을 받아 문자를 변환하거나 삭제.

```bash
echo "hello" | tr 'a-z' 'A-Z'   # → HELLO
tr -d '\n'                        # 개행 문자 삭제
tr -s ' '                         # 연속된 공백을 하나로 압축
tr -d '0-9'                       # 숫자 삭제
```

## tee - 파이프 중간 저장

파이프 흐름을 유지하면서 동시에 파일에도 저장.

```bash
ls | tee output.txt | grep ".md"
# ls 결과 → output.txt에 저장 & grep으로 전달
```

## uniq - 중복 제거

**반드시 sort 후에 사용** — 인접한 중복만 제거하기 때문.

```bash
sort list.txt | uniq        # 중복 제거
sort list.txt | uniq -c     # 중복 횟수 표시
sort list.txt | uniq -d     # 중복된 항목만 출력
```

## 파이프 조합 실전

```bash
# 가장 많이 쓴 명령어 top 5
history | tr -s ' ' | cut -d' ' -f3 | sort | uniq -c | sort -rn | head -5

# 로그에서 ERROR 줄 수 세기
cat app.log | grep "ERROR" | wc -l

# 중복 제거 후 정렬
cat list.txt | sort | uniq
```

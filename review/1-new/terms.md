# 새로 배운 용어/개념

## Ch.9 Permissions

- **권한 숫자 계산**: r=4, w=2, x=1을 더한다. rwx=7, rw-=6, r-x=5, r--=4, ---=0
- **chmod 숫자 방식**: `chmod 755 file` = owner/group/others 순서로 3자리
- **chmod 기호 방식**: `chmod u+x file`. 누구(u/g/o/a) + 동작(+/-/=) + 권한(r/w/x)
- **권한 체크 순서**: owner → group → others 순서로, 첫 매칭에서 끝. owner이면서 group이어도 owner 권한만 적용
- **sudo**: Super User Do. 명령어 하나만 관리자 권한으로 실행. 실무에서 주로 사용
- **su**: Switch User. 사용자 통째로 전환. 거의 안 씀
- **chown**: change owner. 소유자/그룹 변경. sudo 필요 (남의 파일 가로채기 방지)

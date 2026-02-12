# 새로 배운 용어/개념

## Ch.9 Permissions

- **권한 숫자 계산**: r=4, w=2, x=1을 더한다. rwx=7, rw-=6, r-x=5, r--=4, ---=0
- **chmod 숫자 방식**: `chmod 755 file` = owner/group/others 순서로 3자리
- **chmod 기호 방식**: `chmod u+x file`. 누구(u/g/o/a) + 동작(+/-/=) + 권한(r/w/x)
- **권한 체크 순서**: owner → group → others 순서로, 첫 매칭에서 끝. owner이면서 group이어도 owner 권한만 적용
- **sudo**: Super User Do. 명령어 하나만 관리자 권한으로 실행. 실무에서 주로 사용
- **su**: Switch User. 사용자 통째로 전환. 거의 안 씀
- **chown**: change owner. 소유자/그룹 변경. sudo 필요 (남의 파일 가로채기 방지)

## Ch.10 Processes

- **프로세스 vs 프로그램**: 프로그램 = 디스크의 파일, 프로세스 = 실행 중인 프로그램 (메모리에 올라간 상태)
- **ps aux**: 시스템 전체 프로세스 목록. USER, PID, %CPU, %MEM, COMMAND 등 표시
- **top**: 실시간 프로세스 모니터링. q로 나가기
- **& (백그라운드 실행)**: `명령어 &`로 처음부터 백그라운드에서 실행
- **Ctrl+Z / bg / fg**: Ctrl+Z = 일시 정지, bg %번호 = 백그라운드 재개, fg %번호 = 포그라운드로
- **fg/bg는 jobs 번호(%), kill은 PID**: `fg %1` vs `kill 12345`
- **kill vs kill -9**: kill = 종료 요청(정리 시간), kill -9 = 강제 즉시 종료(최후의 수단)
- **killall**: 프로세스 이름으로 종료. `killall firefox`

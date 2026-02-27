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

## Ch.11 The Environment

- **셸 변수 vs 환경변수**: 셸 변수 = 현재 셸에서만. 환경변수 = `export`하면 자식 프로세스에도 전달
- **printenv**: 환경변수 목록 확인. `printenv PATH`로 특정 변수 확인 가능
- **PATH**: 명령어 검색 경로. `:`으로 구분, 왼쪽부터 탐색. 추가: `export PATH="$PATH:/새경로"`
- **변수 할당 규칙**: `=` 앞뒤 공백 금지! `VAR="값"` ✅ / `VAR = "값"` ❌
- **.bashrc vs .bash_profile**: `.bashrc` = 비로그인 셸(매번), `.bash_profile` = 로그인 셸(SSH 등)
- **source**: 설정 파일 다시 불러오기. `source ~/.bashrc` = `. ~/.bashrc`
- **unset**: 변수 삭제. `unset VAR`

## Ch.12 Nano 에디터

- **nano 기본**: `nano filename`으로 열기. `^` = Ctrl 키
- **저장하고 나가기**: `Ctrl+X` → `Y` → `Enter`
- **Ctrl+K / Ctrl+U**: 줄 잘라내기(Kill) / 붙여넣기(Uncut). bash의 Kill/Yank과 비슷하지만 붙여넣기 키 다름!
- **Ctrl+W**: 찾기 (Where is)
- **Ctrl+\\**: 찾아 바꾸기 (Y=하나씩, A=전부)
- **Ctrl+_**: 특정 줄 번호로 이동

## Ch.13 vi/vim

- **vi의 3가지 모드**: Normal(기본, 이동/삭제/복사), Insert(텍스트 입력), Command(저장/종료/찾기바꾸기)
- **모드 전환**: Insert 진입 = `i`/`a`/`o`, Normal 복귀 = `Esc`, Command 진입 = `:`(Normal에서)
- **저장/종료**: `:w` 저장, `:q` 종료, `:wq` 저장+종료, `:q!` 강제종료, `ZZ` 저장+종료(Normal)
- **커서 이동 hjkl**: h=왼, j=아래, k=위, l=오른. `0`=줄 처음, `$`=줄 끝, `w`=다음 단어, `b`=이전 단어
- **파일 이동**: `gg`=맨 처음, `G`=맨 끝, `숫자G`=해당 줄로
- **Insert 진입 6가지**: `i`(앞), `a`(뒤), `o`(아래 새줄), `I`(줄 맨앞), `A`(줄 맨뒤), `O`(위 새줄)
- **삭제**: `x`=글자 1개, `dd`=줄 삭제, `dw`=단어 삭제, `d$`=줄 끝까지, `3dd`=3줄 삭제
- **복사/붙여넣기**: `yy`=줄 복사(yank), `yw`=단어 복사, `p`=뒤에 붙여넣기, `P`=앞에 붙여넣기. `dd`+`p`=줄 이동(잘라내기)
- **실행 취소**: `u`=undo, `Ctrl-r`=redo
- **찾기**: `/단어`=아래로 검색, `?단어`=위로 검색, `n`=다음, `N`=이전
- **찾기/바꾸기**: `:%s/찾을것/바꿀것/g` = 전체 바꾸기, `gc` = 하나씩 확인하며 바꾸기(confirm)

## Ch.14 Customizing the Prompt

- **PS1**: 프롬프트를 저장하는 환경변수. `echo $PS1`로 확인, `.bashrc`에 추가하면 영구 적용
- **이스케이프 코드**: `\u`(유저명), `\h`(호스트명), `\w`(전체 경로), `\W`(폴더명만), `\t`(24시간), `\@`(12시간 AM/PM), `\n`(줄바꿈), `\$`($또는#)
- **색상 코드**: `\[\033[코드m\]내용\[\033[00m\]`. 01;31=빨강, 01;32=초록, 01;33=노랑, 01;34=파랑, 00=리셋
- **`\[...\]` 규칙**: 색상 코드를 반드시 감싸야 함. bash에게 "화면에 안 보이는 문자"라고 알려줘서 프롬프트 길이 계산 오류 방지
- **PS2**: 줄이 이어질 때 나오는 보조 프롬프트. 기본값 `>`

## Ch.15 Reading Files

- **cat**: concatenate. 파일 전체 출력. `-n` 줄 번호, `-A` 숨겨진 문자 표시
- **tac**: cat 거꾸로. 마지막 줄부터 출력. 로그에서 최신 내용 먼저 볼 때
- **rev**: 각 줄의 글자 순서를 좌우 반전. tac(줄 순서)과 구분!
- **head -n N**: 파일 앞에서 N줄 출력 (기본 10줄). `-n -3` = 마지막 3줄 제외
- **tail -n N**: 파일 뒤에서 N줄 출력 (기본 10줄). `-n +3` = 3번째 줄부터 끝까지
- **tail -f**: follow. 파일에 추가되는 내용을 실시간 출력. 로그 모니터링 필수 명령어
- **wc**: Word Count. `-l` 줄 수, `-w` 단어 수, `-c` 바이트 수, `-m` 문자 수
- **sort**: 정렬. `-n` 숫자 기준(없으면 문자열 정렬로 1,10,2 됨!), `-r` 역순, `-k N` N번째 필드, `-u` 중복 제거
- **Useless Use of Cat**: `cat file | cmd` 대신 `cmd file`로 직접 전달이 효율적 (불필요한 프로세스 방지)

## Ch.16 Piping과 tr

- **tr**: Translate. 문자 단위 변환. 파일 직접 읽기 불가 — 반드시 파이프(`|`) 또는 리다이렉션(`<`)으로 입력
- **tr -d**: 지정한 문자 삭제. `tr -d '0-9'`로 숫자 전부 삭제. `-d` 없으면 변환이지 삭제가 아님!
- **tr -s**: squeeze. 연속된 중복 문자를 하나로 압축. `tr -s ' '`으로 다중 공백 정리
- **tr 문자 클래스**: `[:lower:]`, `[:upper:]`, `[:digit:]`, `[:space:]`, `[:punct:]` — 범위 대신 표준 클래스 사용 가능
- **tee**: T자 파이프. stdout과 파일에 동시 출력. 배관의 T자 연결부 비유
- **tee -a**: append 모드. 기존 파일 내용 유지하면서 추가 (`>>` 같은 효과)
- **uniq**: 중복 줄 제거. **인접한** 중복만 제거하므로 반드시 `sort` 선행 필수
- **uniq -c**: count. 각 줄의 등장 횟수 표시
- **uniq -d**: duplicated. 2번 이상 나온 줄만 출력
- **uniq -u**: unique. 정확히 1번만 나온 줄만 출력
- **sort | uniq -c | sort -rn**: 빈도 분석 필수 패턴. sort -u로는 횟수를 셀 수 없음

## Ch.17 Package Management

- **패키지(Package)**: 프로그램을 설치 가능하게 묶은 파일. 실행파일 + 설정파일 + 의존성 정보 포함
- **의존성(Dependency)**: 프로그램 A가 동작하려면 라이브러리 B가 필요한 관계. 패키지 매니저가 자동 해결
- **저장소(Repository)**: 패키지들이 모여있는 온라인 서버. 앱스토어 같은 것
- **데비안 계열 vs 레드햇 계열**: 데비안(.deb, apt) = Ubuntu/Debian, 레드햇(.rpm, yum/dnf) = CentOS/RHEL/Fedora
- **apt update vs apt upgrade**: update = 저장소 목록 갱신(설치X), upgrade = 실제 패키지 업그레이드. 세트로 씀
- **apt remove vs apt purge**: remove = 설정파일 남김(재설치 시 복원), purge = 설정파일까지 완전 삭제
- **sudo 필요 여부**: 시스템 변경(install/remove/update/upgrade) = sudo 필요, 조회(search/show/list) = 불필요
- **dnf**: yum의 후속 버전. RHEL 8+, Fedora에서 사용. 명령어 사용법 동일

## Ch.18 Storage Media

- **마운트(mount)**: 저장장치를 파일 트리의 특정 디렉토리에 연결하는 것. `sudo mount /dev/sdb1 /mnt/usb`
- **umount**: 마운트 해제. `unmount`가 아니라 **`umount`** (n 없음!). `sudo umount /mnt/usb`
- **장치 이름 규칙**: `sda`=첫 번째 디스크, `sda1`=첫 번째 파티션, `sdb1`=두 번째 디스크의 첫 번째 파티션
- **lsblk**: 블록 장치 트리 구조로 보기. macOS 동등 명령어: `diskutil list`
- **fdisk -l**: 모든 디스크/파티션 목록 확인. `sudo fdisk -l /dev/sda`로 특정 디스크만
- **mkfs**: make filesystem (포맷). `mkfs.ext4`, `mkfs.vfat`, `mkfs.ntfs` — 포맷하면 데이터 삭제!
- **/etc/fstab**: 부팅 시 자동 마운트 설정 파일. 장치/마운트위치/파일시스템/옵션/dump/pass 6개 필드
- **UUID 사용 이유**: 장치명(`sda`, `sdb`)은 꽂는 순서에 따라 바뀔 수 있음. UUID는 고유 ID라 안전. `blkid`로 확인
- **Microsoft Basic Data**: diskutil에서 보이는 타입. exFAT 또는 NTFS로 포맷된 윈도우 호환 파티션
- **nodev/nosuid/noowners/noatime**: nodev=디바이스파일 차단, nosuid=setuid 무시, noowners=소유자 무시(ExFAT 등), noatime=접근시간 기록 안 함(SSD 수명+성능)
- **setuid 비트**: `chmod 4755`의 4. 실행 시 파일 소유자 권한으로 실행됨. `ls -l`에서 `s`로 표시. 예: passwd 명령어
- **sealed (macOS)**: OS 볼륨 봉인. 시스템 파일 변조 방지, read-only로 마운트됨

## Ch.19 Networking

- **ping**: 서버 연결 확인. `-c N` 횟수, `-i N` 간격, `-s N` 패킷 크기 지정. ping 안 됨 ≠ 서버 죽음 (방화벽 차단 가능)
- **traceroute**: 목적지까지 경로 추적. 각 hop = 거쳐가는 라우터. `-m N` 최대 hop, `-q N` hop당 패킷 수 (기본 3, 빠르게는 1)
- **ifconfig vs ip**: macOS는 `ifconfig`, 리눅스는 `ip a`. `ifconfig | grep "inet "`으로 IP 추출
- **netstat vs ss**: macOS는 `netstat`, 리눅스는 `ss`. macOS: `netstat -an | grep LISTEN`
- **ssh**: 원격 접속. `-p`(소문자) 포트, `-i` 키파일, `-v` 디버그, `-L` 포트포워딩
- **ssh -L (포트포워딩)**: `ssh -L 로컬포트:localhost:서버포트 user@server`. 외부 차단된 서비스를 SSH 터널로 우회 접속. 터널 열고 해당 서비스 클라이언트로 접속
- **포트**: 건물의 문 번호. IP = 주소, 포트 = 문. 서비스마다 고유 포트 사용 (22=SSH, 80=HTTP, 443=HTTPS, 3306=MySQL)
- **scp**: SSH 기반 파일 복사. `scp 출발지 목적지` — 목적지 생략 불가! `-r` 디렉토리, `-P`(**대문자**) 포트. ssh는 -p(소문자)
- **wget**: 파일 다운로드 전문. `-O` 파일명, `-c` 이어받기(끊겨도 재개), 기본 파일로 저장
- **curl**: 만능 네트워크 도구. `-I` 헤더만, `-s` 조용히, `-L` 리다이렉트 따라가기, `-X` 메서드, `-d` 데이터, `-H` 커스텀 헤더. 기본 화면 출력
- **wget vs curl**: 다운로드만 → wget(-c 이어받기 편함), API 테스트/디버깅 → curl(POST, 헤더 등)

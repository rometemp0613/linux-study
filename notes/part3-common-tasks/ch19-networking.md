# Ch.19: Networking

## 네트워크 진단

### ping — 연결 확인
- 상대 서버가 살아있는지 확인. ICMP 패킷을 보내고 응답을 받음
- 리눅스/macOS는 `Ctrl+C`로 멈춰야 함 (Windows는 기본 4번)
- **ping 안 됨 ≠ 서버 죽음** — 방화벽이 ICMP 차단하는 경우 많음 (네이버 등)
- 주요 옵션:
  - `-c N`: 횟수 제한 (Count)
  - `-i N`: 간격 (Interval, 초)
  - `-W N`: 타임아웃 (Wait, 초)
  - `-s N`: 보내는 패킷 크기 지정 (Size, 바이트). 큰 데이터 전송 문제 진단용

### traceroute — 경로 추적
- 목적지까지 거쳐가는 라우터(hop)를 하나씩 보여줌
- `* * *`은 해당 라우터가 응답을 안 하는 것 (차단과 다름)
- 주요 옵션:
  - `-m N`: 최대 hop 수 (Max)
  - `-q N`: hop당 보내는 패킷 수 (기본 3). `-q 1`로 빠르게 확인
  - `-w N`: 응답 대기 시간 (초)

### ifconfig / ip — 내 네트워크 정보
- macOS: `ifconfig` (ip 명령어 없음)
- 리눅스: `ip addr show` 또는 `ip a` (ifconfig은 구식)
- `inet` 뒤의 숫자가 내 IP 주소
- `ifconfig | grep "inet "`으로 IP만 추출 가능

### netstat / ss — 네트워크 연결 상태
- macOS: `netstat` (ss 없음), 리눅스: `ss` (netstat 구식)
- macOS에서 LISTEN 확인: `netstat -an | grep LISTEN`
- ESTABLISHED: 현재 연결된 외부 서버들

## 원격 접속 & 파일 전송

### ssh — 원격 서버 접속 ⭐
- Secure Shell. 암호화된 원격 접속
- `ssh user@server` — 접속 후 모든 명령어는 원격 서버에서 실행
- 나가기: `exit` 또는 `Ctrl+D`
- 주요 옵션:
  - `-p N`: 포트 지정 (기본 22)
  - `-i 파일`: 인증키 파일 지정 (AWS 등 클라우드 필수)
  - `-v`: 디버그 모드 (접속 안 될 때 원인 파악)
  - `-L 로컬포트:localhost:서버포트`: 포트 포워딩 (터널링)

### 포트 포워딩 (ssh -L)
- 외부에서 직접 접속 안 되는 서비스를 SSH 터널로 우회 접속
- `ssh -L 3307:localhost:3306 user@server`
  → 내 컴퓨터 localhost:3307 → 터널 → 서버 localhost:3306
- 포트 = 건물의 문 번호. IP가 주소, 포트가 문 번호
- 터널 열고 나서 해당 서비스에 맞는 클라이언트로 접속 (DB면 mysql, 웹이면 브라우저)

### scp — 파일 전송 (SSH 기반)
- cp의 네트워크 버전. `scp [출발지] [목적지]`
- **목적지 생략 불가!** — 반드시 `./` 등 명시
- 주요 옵션:
  - `-r`: 디렉토리 전체 복사 (cp -r과 같은 이유)
  - `-P N`: 포트 지정 (**대문자 P!** ssh는 소문자 -p)
  - `-i 파일`: 인증키 파일
  - `-C`: 압축 전송

## 다운로드 & API

### wget — 파일 다운로드 전문
- URL에서 파일 받기. 기본적으로 파일로 저장
- 주요 옵션:
  - `-O 파일`: 파일명 지정 (Output)
  - `-c`: 이어받기 (Continue) — 끊겨도 재개
  - `-q`: 조용히 (Quiet)
  - `-b`: 백그라운드 다운로드

### curl — 만능 네트워크 도구 ⭐
- URL과 데이터를 주고받는 도구. 기본적으로 화면에 출력
- 주요 옵션:
  - `-I`: 헤더만 보기 (Head)
  - `-o 파일`: 파일명 지정, `-O`: 원래 이름으로 저장
  - `-s`: 진행 표시 숨기기 (Silent) — stderr의 progress 출력 제거
  - `-L`: 리다이렉트 따라가기 (Location) — 301 → 200 자동 추적
  - `-X METHOD`: HTTP 메서드 지정 (POST, PUT 등)
  - `-d 데이터`: 데이터 전송 (Data)
  - `-H "헤더"`: 커스텀 헤더 (Header)
  - `-v`: 상세 출력 (Verbose)

### wget vs curl
- 파일 다운로드만 → wget (이어받기 -c가 편함)
- API 테스트/디버깅 → curl (POST, 헤더 등 다양한 기능)

# Ch.17: Package Management

## 핵심 개념

### 패키지(Package)
- 프로그램을 설치 가능한 형태로 묶어놓은 파일
- 실행 파일 + 설정 파일 + 문서 + 의존성 정보 포함

### 의존성(Dependency)
- 프로그램 A가 동작하려면 라이브러리 B가 필요한 관계
- 패키지 매니저가 자동으로 파악해서 함께 설치

### 저장소(Repository)
- 패키지들이 모여있는 온라인 서버 (앱스토어 같은 것)
- 공식 저장소, 커뮤니티 저장소, 서드파티 저장소 등

### 저수준 vs 고수준 도구
- **저수준** (`dpkg`, `rpm`): 패키지 파일 하나를 직접 설치/삭제. 의존성 자동 해결 ❌
- **고수준** (`apt`, `yum`/`dnf`): 저장소에서 검색, 의존성 자동 해결 ✅ — 보통 이걸 씀

## 두 가지 계열

| | 데비안(Debian) 계열 | 레드햇(Red Hat) 계열 |
|--|--|--|
| **배포판** | Ubuntu, Debian, Mint | RHEL, CentOS, Fedora, Rocky |
| **패키지 형식** | `.deb` | `.rpm` |
| **저수준 도구** | `dpkg` | `rpm` |
| **고수준 도구** | `apt` | `yum` / `dnf` |

## apt 주요 명령어 (데비안/우분투)

| 명령어 | 용도 | sudo 필요 |
|--------|------|-----------|
| `sudo apt update` | 저장소 목록 최신화 (설치 X, 카탈로그 갱신) | ✅ |
| `sudo apt install 패키지` | 패키지 설치 | ✅ |
| `sudo apt remove 패키지` | 패키지 삭제 (설정파일 남김) | ✅ |
| `sudo apt purge 패키지` | 패키지 + 설정파일 완전 삭제 | ✅ |
| `sudo apt upgrade` | 설치된 패키지 전부 업그레이드 | ✅ |
| `apt search 키워드` | 패키지 검색 | ❌ |
| `apt show 패키지` | 패키지 정보 보기 | ❌ |
| `apt list --installed` | 설치된 패키지 목록 | ❌ |

## yum/dnf 주요 명령어 (레드햇/CentOS)

| 명령어 | 용도 |
|--------|------|
| `sudo yum install 패키지` | 설치 |
| `sudo yum remove 패키지` | 삭제 |
| `sudo yum update` | 전체 업데이트 (= apt의 upgrade) |
| `yum search 키워드` | 검색 |
| `yum info 패키지` | 정보 보기 |

> `dnf`는 `yum`의 후속 버전. Fedora, RHEL 8+에서 사용. 명령어 사용법 동일.

## 헷갈리기 쉬운 차이

### update vs upgrade (apt)
- `apt update` = 저장소 목록 갱신 (뭐가 새 버전인지 확인만)
- `apt upgrade` = 실제로 패키지들을 새 버전으로 업그레이드
- 보통 세트로 씀: `sudo apt update && sudo apt upgrade`

### remove vs purge
- `remove` = 프로그램 삭제, 설정 파일 남김 (재설치 시 설정 복원 가능)
- `purge` = 프로그램 + 설정 파일 모두 삭제

### sudo 필요 vs 불필요
- 시스템 변경 (install, remove, update, upgrade) → sudo 필요
- 정보 조회 (search, show, list) → sudo 불필요

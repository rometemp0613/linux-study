# Ch.9: Permissions (권한)

## 핵심 개념: 리눅스는 멀티유저 시스템

모든 파일/디렉토리에 대해 3가지를 제어:
- **누가**: owner(소유자) / group(그룹) / others(그 외)
- **뭘**: read(읽기) / write(쓰기) / execute(실행)
- **허용 여부**: 허용 / 거부

## 권한 읽는 법

```
-rwxr-xr-x
│ │   │   │
│ │   │   └── others: r-x
│ │   └────── group:  r-x
│ └────────── owner:  rwx
└──────────── 파일 타입 (- = 일반파일, d = 디렉토리, l = 심볼릭 링크)
```

- `r` = read(4), `w` = write(2), `x` = execute(1), `-` = 없음(0)

## 권한 체크 순서

```
1. owner인가?  → YES → owner 권한 적용 (여기서 끝!)
2. group에 속해있나?  → YES → group 권한 적용
3. 둘 다 아니면 → others 권한 적용
```

- owner이면서 group이어도 **owner 권한만** 적용 (첫 매칭에서 끝)

## group이란?

- 사용자들을 묶어놓은 **팀**
- 파일에는 그룹이 **딱 1개만** 지정됨
- 내가 여러 그룹에 속해있어도, 파일의 그룹에 속해있느냐만 중요
- `id` 또는 `groups` 명령어로 내 그룹 확인 가능

## chmod — 권한 변경

### 숫자(8진수) 방식

```
r=4, w=2, x=1 → 더해서 표현

chmod 755 file   # rwxr-xr-x
chmod 644 file   # rw-r--r--
chmod 600 file   # rw-------
chmod 700 dir/   # rwx------
```

### 기호 방식

```
누구: u(owner) g(group) o(others) a(all)
동작: +(추가) -(제거) =(설정)
권한: r w x

chmod u+x file       # 소유자에게 실행 추가
chmod g-w file       # 그룹에서 쓰기 제거
chmod o-rwx file     # 그 외 전부 제거
chmod a+r file       # 모두에게 읽기 추가
```

### 사용 기준

- 숫자: 권한을 **통째로** 설정할 때 (chmod 755)
- 기호: 특정 권한만 **하나 추가/제거**할 때 (chmod u+x)

## 자주 쓰는 패턴

```
chmod 755 script.sh   # 스크립트 실행 가능하게 (가장 흔함)
chmod 644 file.txt    # 일반 파일 기본 권한
chmod 600 id_rsa      # 비밀 파일 (나만 접근)
```

## sudo — 관리자 권한으로 명령어 실행

```bash
sudo cat /etc/sudoers   # 이 명령어 하나만 root 권한으로 실행
```

- **S**uper **U**ser **Do**
- 비밀번호 입력 후 약 5분간 유지
- 실무에서 주로 사용

## su — 사용자 전환

```bash
su            # root로 전환
su - 영희     # 영희로 전환
exit          # 원래 사용자로 돌아오기
```

- 거의 안 씀 (sudo가 더 안전)

## sudo vs su

| | sudo | su |
|---|------|-----|
| 범위 | 명령어 하나만 | 사용자 통째로 전환 |
| 안전성 | 더 안전 | 덜 안전 |
| 실무 | 주로 사용 | 거의 안 씀 |

## chown — 소유자/그룹 변경

```bash
sudo chown 영희 file.txt          # 소유자 변경
sudo chown 영희:개발팀 file.txt    # 소유자 + 그룹 변경
sudo chown :개발팀 file.txt        # 그룹만 변경
```

- **ch**ange **own**er
- sudo 필요 — 아무나 소유권 바꾸면 남의 파일을 가로챌 수 있으므로

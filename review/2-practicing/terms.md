# 복습 중인 용어/개념

## Ch.16 Piping과 tr (2026-02-23) — 연습문제에서 틀린 것

- **sort -rn으로 내림차순**: "큰 순서대로" 정렬할 때 `-r`(reverse) 필수. `sort -n`만 쓰면 오름차순(작은→큰). top N 구할 때: `sort -rn | head -N`

## Ch.18 Storage Media (2026-02-26) — 퀴즈에서 틀린 것

- **파티션 이름**: `sdb`는 디스크 전체, `sdb1`이 파티션. 장치 경로는 `/dev/sdb1`
- **마운트 전 디렉토리 생성 필수**: 마운트 포인트가 없으면 `sudo mkdir /mnt/backup` 먼저! 없는 디렉토리에 mount하면 에러
- **/etc/fstab 6개 필드**: 장치(UUID) / 마운트위치 / 파일시스템 / 옵션(defaults) / dump(0=안함) / pass(0=검사안함, 1=루트, 2=나머지)

## Ch.19 Networking (2026-02-27) — 퀴즈에서 틀린 것

- ~~**scp 목적지 필수**~~ ✅ 2026-02-28 mastered로 승급
- **scp -r 디렉토리**: 디렉토리 전체 복사 시 `-r` 필수. cp -r과 같은 이유

## Ch.16 Piping과 tr (2026-03-02) — 복습 퀴즈 승급

- **uniq**: 중복 줄 제거. **인접한** 중복만 제거하므로 반드시 `sort` 선행 필수

## Ch.19 Networking (2026-03-02) — 복습 퀴즈 승급

- **wget vs curl**: 다운로드만 → wget(-c 이어받기 편함), API 테스트/디버깅 → curl(POST, 헤더 등)

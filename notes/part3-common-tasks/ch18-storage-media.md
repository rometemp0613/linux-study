# Ch.18 Storage Media

## 핵심 개념

### 마운트(Mount)란?
리눅스는 모든 게 하나의 파일 트리. 저장장치를 쓰려면 트리의 어딘가에 "붙여야(mount)" 함.

```
/
├── home/
└── mnt/
    └── usb/   ← USB를 마운트하면 여기서 접근 가능
```

### 장치 이름 규칙
```
/dev/sda       ← 첫 번째 디스크 전체
/dev/sda1      ← 첫 번째 디스크의 1번 파티션
/dev/sdb       ← 두 번째 디스크 (USB 등)
/dev/sdb1      ← 두 번째 디스크의 1번 파티션
/dev/nvme0n1   ← NVMe SSD (최신 방식)
```

---

## 주요 명령어

### 상태 확인
```bash
lsblk          # 블록 장치 트리 구조로 보기 (제일 보기 편함)
df -h          # 마운트된 장치 + 용량 (human-readable)
mount          # 현재 마운트 목록 전체
```

### 마운트 / 언마운트
```bash
sudo mount /dev/sdb1 /mnt/usb     # 마운트
sudo umount /mnt/usb              # 언마운트 (unmount 아님! n 없음)
sudo umount /dev/sdb1             # 장치명으로도 가능
```

### 파티션 확인
```bash
sudo fdisk -l             # 모든 디스크/파티션 목록
sudo fdisk -l /dev/sda    # 특정 디스크만
```

### 포맷 (mkfs = make filesystem)
```bash
sudo mkfs.ext4 /dev/sdb1    # ext4 (리눅스 표준)
sudo mkfs.vfat /dev/sdb1    # FAT32 (USB, 호환성용)
sudo mkfs.ntfs /dev/sdb1    # NTFS (윈도우 호환)
```
⚠️ 포맷하면 데이터 전부 날아감!

### UUID 확인
```bash
sudo blkid    # 각 파티션의 UUID 출력
```

---

## /etc/fstab — 자동 마운트 설정

```
# 장치              마운트위치    파일시스템  옵션       dump  pass
/dev/sda1           /            ext4       defaults   0     1
UUID=xxxx-xxxx      /mnt/data    ext4       defaults   0     2
```

### UUID 사용 이유
장치명(`sda`, `sdb`)은 꽂는 순서에 따라 바뀔 수 있음.
UUID는 파티션 고유 ID라 안전하게 지정 가능.

---

## macOS 비교

| 개념 | 리눅스 | macOS |
|------|--------|-------|
| 물리 디스크 | `/dev/sda` | `/dev/disk0` |
| 파티션 | `/dev/sda1` | `/dev/disk0s1` |
| 디스크 목록 | `lsblk` | `diskutil list` |
| 마운트 상태 | `df -h` | `df -h` |
| 파티션 관리 | `fdisk` | `diskutil` |
| 포맷 | `mkfs.ext4` | `diskutil eraseVolume` |

### APFS 특이점 (macOS)
하나의 물리 파티션(`disk0s2`) 안에서 여러 볼륨을 생성 (disk3s1, disk3s5 등).
`synthesized`로 표시되는 disk3가 논리적 컨테이너.

---

## 파일시스템 종류

| 이름 | 용도 |
|------|------|
| ext4 | 리눅스 표준 |
| FAT32/vfat | USB, 크로스플랫폼 (4GB 파일 제한) |
| exFAT | FAT32 대용량 개선판 |
| NTFS | 윈도우 표준 |
| APFS | macOS 표준 |
| XFS | 대용량 서버용 |

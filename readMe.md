# Git 라이프사이클 (Lifecycle)

Git에서 파일은 **작업 디렉터리(Working Directory)** → **스테이징 영역(Staging Area / Index)** → **로컬 저장소(Local Repository)** → **원격 저장소(Remote Repository)** 흐름으로 이동
---

## Git Flow 이미지

![Git Flow](img/git-flow.png)
![Git Flow 2](img/git-flow2.png)

## 1) 4개의 주요 영역

### 1. Working Directory (작업 디렉터리)
- 내가 실제로 파일을 **수정/추가/삭제**하는 공간
- 아직 Git에 “기록(스냅샷)”으로 확정되지 않은 상태

### 2. Staging Area (스테이징 영역 / Index)
- 다음 커밋에 포함될 변경사항을 **선별해서 올려두는 공간**
- “커밋 대기열” 같은 개념

### 3. Local Repository (로컬 저장소, `.git`)
- 커밋이 저장되는 공간
- `commit`이 누적되며 히스토리(버전)가 만들어짐

### 4. Remote Repository (원격 저장소)
- GitHub/GitLab/Bitbucket 같은 서버 저장소
- 협업/백업/배포 트리거 등에 활용

---

## 2) 파일 상태(State)

Git은 파일을 크게 아래 상태로 관리합니다.

- **Untracked**: Git이 아직 추적하지 않는 새 파일
- **Tracked**: Git이 추적하는 파일  
  - **Unmodified**: 마지막 커밋과 동일 (변경 없음)
  - **Modified**: 작업 디렉터리에서 변경됨
  - **Staged**: 스테이징 영역에 올라감(다음 커밋 대상)

---

## 3) 상태 전이(Flow)

### A. 새 파일 생성
1. `Untracked` (새 파일)
2. `git add <file>` → `Staged`
3. `git commit -m "msg"` → `Tracked(Unmodified)` (커밋에 기록됨)

### B. 기존 파일 수정
1. `Tracked(Unmodified)` → 수정 → `Modified`
2. `git add <file>` → `Staged`
3. `git commit -m "msg"` → `Tracked(Unmodified)`

### C. 스테이징 되돌리기 (add 취소)
- `git restore --staged <file>`
  - `Staged` → `Modified` (스테이징에서만 내림)

### D. 작업 디렉터리 변경 되돌리기 (수정 취소)
- `git restore <file>`
  - `Modified` → `Unmodified` (주의: 변경 내용 사라짐)

### E. 파일 삭제
- `git rm <file>` → `Staged(삭제 예약)`
- `git commit` → 커밋 히스토리에 “삭제”로 기록됨

---

## 4) 로컬 ↔ 원격 이동

### 원격에 반영하기 (Push)
- 로컬 커밋을 원격으로 올림
- `git push origin <branch>`

### 원격 변경 가져오기 (Fetch / Pull)
- `git fetch`: 원격 변경을 “가져오기만” 하고 병합은 안 함
- `git pull`: `fetch + merge(or rebase)` 한 번에 수행

---

## 5) 전체 흐름 요약 (한 줄 버전)

- 수정/생성: **Working Directory**
- 커밋 대상 선택: **Staging Area (`git add`)**
- 버전 확정: **Local Repo (`git commit`)**
- 공유/배포: **Remote Repo (`git push`)**

---

## 6) 자주 쓰는 명령어 맵

- 상태 확인: `git status`
- 변경 확인: `git diff` / `git diff --staged`
- 스테이징: `git add .` / `git add <file>`
- 커밋: `git commit -m "msg"`
- 스테이징 취소: `git restore --staged <file>`
- 변경 취소: `git restore <file> or git reset <file>`
- 원격 반영: `git push`
- 원격 가져오기: `git fetch` / `git pull`

---

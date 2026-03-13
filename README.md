# 🚀 Git Cheat-Sheet & Guide

효율적인 버전 관리를 위한 Git의 핵심 명령어와 워크플로우를 정리한 가이드 ( feature by 코딩애플 )

---

## 1. 기본 개념 (Fundamentals)

### 왜 `add`와 `commit`을 나누나요?
모든 변경 사항을 기록할 필요는 없기 때문입니다. (예: 빌드 이미지, 임시 파일 등)
1. **Step 1 (add):** 기록을 남길 파일만 골라 담습니다. (**Staging**)
2. **Step 2 (commit):** 골라둔 파일들을 사진 찍듯 기록합니다. (**Repository**)

[Image of git workflow staging area repository]

| 명령어 | 설명 |
| :--- | :--- |
| `git status` | 현재 파일들의 상태(수정, 스테이징 등) 확인 |
| `git add <파일명>` | 파일을 Staging Area에 올리기 |
| `git commit -m "메시지"` | 스테이징된 파일을 로컬 저장소에 기록 |
| `git log` | 커밋 히스토리 보기 (`--oneline`, `--graph` 옵션 활용) |

---

## 2. 브랜치 관리 (Branching)

독립적인 작업 공간을 생성하여 안전하게 기능을 개발합니다.

- **브랜치 생성 및 이동**: `git checkout -b <브랜치명>` (생성+이동 한 번에)
- **이름 변경**: `git branch -M master main`
- **합치기(Merge)**: 기준이 되는 브랜치(main)로 이동 후 `git merge <대상브랜치>` 수행

### 🔄 병합(Merge) 전략 상세
* **3-way Merge**: 각 브랜치에서 커밋 후 합치는 기본 방식.
* **Fast-forward**: 신규 브랜치에만 커밋이 있을 때, 포인터만 이동하는 방식. (`--no-ff`로 강제 3-way 가능)
* **Rebase & Merge**: 시작점을 최신 커밋으로 옮겨 선형 히스토리를 만듦.
* **Squash & Merge**: 여러 개의 커밋을 하나로 뭉쳐서 깔끔하게 병합.

---

## 3. 원격 저장소와 협업 (Remote & Collaboration)

### 기본 명령어
- **원격 연결**: `git remote add origin <저장소주소>`
- **코드 올리기**: `git push -u origin <브랜치명>` ( `-u`는 주소를 기억하게 함)
- **코드 가져오기**:
    - `git clone <주소>`: 저장소 통째로 복제
    - `git pull`: 원격의 최신 내역을 로컬로 가져와서 합침
- **Pull Request (PR)**: 내가

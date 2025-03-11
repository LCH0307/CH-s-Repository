# **Git & GitHub 사용법**

## **📌 Git 기본 개념**
Git은 분산 버전 관리 시스템(DVCS)으로, 코드를 안전하게 관리하고 협업할 수 있도록 도와줍니다.

### **✅ 주요 개념**
- **원격 저장소(Remote Repository)**: GitHub와 같은 원격 서버에 저장된 저장소
- **로컬 저장소(Local Repository)**: 내 컴퓨터에 저장된 저장소
- **스테이지(Stage)**: 커밋을 준비하는 영역
- **커밋(Commit)**: 변경된 내용을 저장하는 단위 (=세이브)
- **푸시(Push)**: 로컬에서 작업한 내용을 원격 저장소에 업로드
- **풀(Pull)**: 원격 저장소에서 최신 변경 사항을 가져옴
- **패치(Fetch)**: 원격 저장소의 변경 사항을 가져오지만, 로컬 브랜치에는 반영하지 않음
- **브랜치(Branch)**: 독립적인 작업을 위해 분리된 코드 공간
- **병합(Merge)**: 여러 브랜치를 하나로 합치는 작업
- **리베이스(Rebase)**: 변경 내역을 깔끔하게 정리하는 병합 방법

---

## **📌 Git 설치 및 설정**

### **1️⃣ Git 설치**
1. [Git 공식 웹사이트](https://git-scm.com/)에서 운영체제에 맞는 Git을 다운로드합니다.
2. 설치 후, 터미널(cmd, bash, PowerShell)에서 아래 명령어로 정상 설치 여부를 확인합니다.
```bash
git --version
```
3. Git 사용자 정보를 설정합니다.
```bash
git config --global user.name "사용자이름"
git config --global user.email "이메일주소"
```

---

## **📌 Git 기본 사용법**

### **1️⃣ 저장소 초기화 및 원격 연결**
```bash
git init  # 현재 폴더를 Git 저장소로 초기화
git remote add origin <원격 저장소 URL>  # 원격 저장소 연결
git clone <원격 저장소 URL>  # 원격 저장소를 로컬로 복사
```

### **2️⃣ 파일 변경 및 커밋**
```bash
git status  # 현재 Git 상태 확인
git add .  # 모든 변경된 파일을 스테이징
git commit -m "작업 내용 설명"  # 커밋 생성
```

### **3️⃣ 원격 저장소와 동기화**
```bash
git push origin <브랜치명>  # 원격 저장소로 업로드
git pull origin <브랜치명>  # 원격 저장소에서 변경 사항 가져오기
git fetch origin  # 원격 저장소의 변경 사항을 가져오기만 함
git merge origin/<브랜치명>  # fetch 후 로컬에 반영
```

---

## **📌 브랜치 관리**
브랜치는 독립적인 작업을 가능하게 하며, 코드 변경 사항을 분리하여 개발할 수 있도록 돕습니다.

### **1️⃣ 브랜치 생성 및 이동**
```bash
git branch  # 현재 존재하는 브랜치 목록 확인
git branch <브랜치명>  # 새로운 브랜치 생성
git checkout <브랜치명>  # 특정 브랜치로 이동
git checkout -b <브랜치명>  # 새로운 브랜치를 생성하고 동시에 이동
```

### **2️⃣ 브랜치 삭제**
```bash
git branch -d <브랜치명>  # 병합된 브랜치 삭제 (로컬)
git branch -D <브랜치명>  # 강제 삭제 (병합되지 않은 브랜치 포함)
git push origin --delete <브랜치명> # 원격 브랜치 삭제 (Github 에서 삭제)
git fetch -p  # 삭제된 랜치 정보를 로컬에 반영(-p (--prune)옵션 : 삭제된 원격 브랜치를 로컬에서도 정리)
```

### **3️⃣ 브랜치 병합**
```bash
git checkout main  # 병합을 수행할 브랜치로 이동
git merge <브랜치명>  # 현재 브랜치에 지정된 브랜치를 병합
```

### **4️⃣ 원격 브랜치 관련 명령어**
```bash
git push origin <브랜치명>  # 원격 저장소에 브랜치 업로드
git branch -r  # 원격 저장소의 브랜치 목록 확인
git checkout -b <브랜치명> origin/<브랜치명>  # 원격 브랜치를 로컬로 가져오기
git push --delete origin <브랜치명>  # 원격 저장소에서 브랜치 삭제
```

---

## **📌 Merge 충돌 해결 방법**
### **1️⃣ Merge 충돌 발생 시 상태 확인**
```bash
git status
```
🔍 **출력 예시**:
```
Unmerged paths:
  both modified:   example.txt
```
- 충돌이 발생한 파일 목록이 표시됩니다.

### **2️⃣ 충돌 파일 직접 수정**
```txt
<<<<<< HEAD
현재(main) 브랜치의 내용
======
feature-branch의 내용
>>>>>> feature-branch
```
- **`HEAD` 위쪽** → `main` 브랜치의 코드
- **`======` 아래쪽** → `feature-branch`의 코드
- 불필요한 충돌 표시를 삭제하고, 원하는 내용으로 수정합니다.

### **3️⃣ 수정 후 Git에 반영**
```bash
git add example.txt
git commit -m "Merge conflict resolved"
git push origin main
```
✔ 충돌 해결 후, `add`로 해결 완료 표시 → `commit` → `push` 하면 병합이 완료됩니다.

### **4️⃣ Merge 충돌을 피하는 방법**
1. **항상 최신 코드로 동기화**
```bash
git pull origin main
```
2. **작업 브랜치를 자주 병합하여 최신 상태 유지**
```bash
git merge main
```
3. **작업 단위를 작게 나누어 커밋하고 변경 사항을 자주 반영하기**

---

## **📌 Commit vs Push의 차이점**
| 명령어 | 설명 |
|------|------|
| **Commit** | 변경 사항을 **로컬 저장소**에 저장하는 작업 (원격에는 반영되지 않음) |
| **Push** | 로컬에서 저장한 커밋을 **원격 저장소**로 업로드하는 작업 |

📌 **즉, `commit`은 로컬에서 저장하는 것이고, `push`를 해야 GitHub 등에 반영됨!**

---

## **📌 Fetch vs Pull의 차이점**
| 명령어 | 설명 |
|------|------|
| **Fetch** | 원격 저장소의 최신 변경 사항을 가져오지만, **로컬 브랜치에는 적용되지 않음** |
| **Pull** | `fetch` 후 `merge`를 자동으로 실행하여 **로컬 브랜치에도 반영** |

📌 **즉, `fetch`는 가져오기만 하고, `pull`은 병합까지 수행하는 차이가 있음!**

---

## **📌 Sync Changes (동기화 변경)**
GitHub Desktop이나 VS Code에서는 **"Sync Changes"** 기능을 제공하며, 이는 내부적으로 아래 명령어를 실행하는 것과 동일합니다:
```bash
git pull origin <현재 브랜치명>
git push origin <현재 브랜치명>
```
✔ **로컬과 원격 저장소를 자동으로 동기화하여 최신 상태 유지**

---

🚀 **이제 Git의 기본 개념부터 브랜치 관리, Merge 충돌 해결까지 완벽하게 정리되었습니다!** 😊  



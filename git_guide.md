# **CH-s-Repository: Git & GitHub 사용법**

## **📌 Git 기본 개념**
Git은 분산 버전 관리 시스템(DVCS)으로, 코드를 안전하게 관리하고 협업할 수 있도록 도와줍니다.

### **✅ 주요 개념**
- **원격 저장소(Remote Repository)**: GitHub와 같은 원격 서버에 저장된 저장소
- **로컬 저장소(Local Repository)**: 내 컴퓨터에 저장된 저장소
- **스테이지(Stage)**: 커밋을 준비하는 영역
- **커밋(Commit)**: 변경된 내용을 저장하는 단위 (=세이브)
- **푸시(Push)**: 로컬에서 작업한 내용을 원격 저장소에 업로드
- **풀(Pull)**: 원격 저장소에서 최신 변경 사항을 가져옴
- **브랜치(Branch)**: 독립적인 작업을 위해 분리된 코드 공간
- **병합(Merge)**: 여러 브랜치를 하나로 합치는 작업
- **리베이스(Rebase)**: 변경 내역을 깔끔하게 정리하는 병합 방법

---

## **📌 Git 사용법 (기본 명령어)**

### **1️⃣ Git 초기화 및 원격 저장소 연결**
```bash
git init
```
- 현재 폴더를 Git 저장소로 초기화

```bash
git remote add origin <원격 저장소 URL>
```
- 원격 저장소를 연결

```bash
git clone <원격 저장소 URL>
```
- 원격 저장소를 내 로컬 컴퓨터로 복사 (다운로드)

---

### **2️⃣ 작업한 파일을 Git에 올리기**
```bash
git status
```
- 현재 Git 상태 확인 (추적되지 않은 파일, 변경된 파일 확인 가능)

```bash
git add .
```
- 모든 변경된 파일을 스테이징 영역에 추가

```bash
git commit -m "작업 내용 설명"
```
- 스테이징된 파일을 커밋 (로컬 저장소에 저장)

```bash
git push origin <브랜치명>
```
- 로컬의 변경 사항을 원격 저장소로 업로드

---

### **3️⃣ 원격 저장소에서 변경 사항 가져오기**
```bash
git pull origin <브랜치명>
```
- 원격 저장소에서 최신 변경 사항을 가져옴

```bash
git fetch
git branch -r
```
- 원격 저장소의 최신 정보를 가져오고, 원격 브랜치 목록 확인

---

### **4️⃣ 브랜치(Branch) 관리**
```bash
git branch  # 현재 브랜치 목록 확인
git branch <브랜치명>  # 새 브랜치 생성
git checkout <브랜치명>  # 특정 브랜치로 이동
git checkout -b <브랜치명>  # 브랜치 생성 + 이동
git push origin <브랜치명>  # 원격 저장소에 브랜치 업로드
```

---

### **5️⃣ 브랜치 병합 (Merge & Rebase)**
```bash
git checkout main  # 메인 브랜치로 이동
git merge <브랜치명>  # 병합 수행
```

```bash
git checkout <브랜치명>
git rebase main  # 깔끔한 병합 수행
```

---

### **6️⃣ 작업 취소 및 되돌리기**
```bash
git reset --hard HEAD~1  # 마지막 커밋 삭제 후 이전 상태로 되돌리기
git checkout -- <파일명>  # 특정 파일 변경 사항 되돌리기
git revert <커밋ID>  # 특정 커밋 취소 후 새로운 커밋 생성
```

---

## **📌 Git 사용 흐름 요약**
1. **Git 초기화 및 원격 저장소 연결**
   ```bash
   git init
   git remote add origin <원격 저장소 URL>
   ```
2. **새로운 브랜치 생성 및 이동**
   ```bash
   git checkout -b feature-branch
   ```
3. **파일 추가 및 커밋**
   ```bash
   git add .
   git commit -m "새로운 기능 추가"
   ```
4. **원격 저장소로 푸시**
   ```bash
   git push origin feature-branch
   ```
5. **브랜치 병합 (Merge)**
   ```bash
   git checkout main
   git merge feature-branch
   git push origin main
   ```
6. **작업 되돌리기**
   ```bash
   git reset --hard HEAD~1
   ```

---

## **📌 Git 사용 시 주의할 점**
- **작업을 시작할 때 `git pull`을 실행하여 최신 상태를 유지하세요.**
- **작업이 끝나면 반드시 `commit` 후 `push`하세요.**
- **팀 프로젝트에서는 브랜치를 활용하여 협업하세요.**
- **Merge 전에 반드시 충돌(conflict)이 없는지 확인하세요.**
- **Rebase를 사용할 경우 원본 커밋이 변경되므로 주의하세요.**

---

## **✅ Git & GitHub 용어 정리**
| 용어 | 설명 |
|------|------|
| **Staging Area (스테이징 영역)** | `git add`를 하면 변경된 파일이 대기하는 공간 |
| **Commit (커밋)** | 변경 사항을 로컬 저장소에 저장 |
| **Push (푸시)** | 로컬 저장소의 변경 사항을 원격 저장소로 업로드 |
| **Pull (풀)** | 원격 저장소의 변경 사항을 가져와 병합 |
| **Merge (머지)** | 다른 브랜치의 내용을 현재 브랜치에 합치는 작업 |
| **Rebase (리베이스)** | 변경 이력을 정리하며 브랜치를 병합 |
| **Checkout (체크아웃)** | 특정 브랜치나 커밋으로 이동 |
| **HEAD** | 현재 작업 중인 브랜치를 가리키는 포인터 |

---

## **✅ 마무리**
🎯 **Git을 사용하면 코드 관리가 더 쉬워지고 협업이 편리해진다!** 🎯


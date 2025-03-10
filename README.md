# CH-s-Repository

## git 명령어 요약
- clone: 원격 저장소 (github)를 내 컴퓨터에 복사.
- add: 내 컴퓨터에서 작업한 파일들을 스테이지에 추가.
- commit: 스테이지에 올라온 파일들을 가지고 커밋. (=세이브)
- push: 원격 저장소에 커밋을 업로드.

## 파일 내용 되돌리기
- 특정 파일의 내용을 마지막 커밋으로 돌리고 싶다면 해당 파일 선택 후 '코드 뭉치 버리기(Discard Changes)' 선택
- VsCode > Source Control > Discard Changes

## commit 과 push의 차이
(참고 링크 : https://thenicesj.tistory.com/506)

git 의 repository 에서 받아오는 것을 pull 로 당겨온다 라고 하고, 로컬에 있는 코드를 원격으로 올리는 작업을 push라고 함.

여기서 push를 하기 위해서는 add와 commit 작업이 필요한데, 이 작업들의 차이점은.

local(local repository 내 피시의 저장소)에서 올리기 위해 올릴 파일들을 리스트업 하는 작업을 git add 라고 함.
add된 파일들을 local에 변경 작업 하는것을 commit 이라고 하고 메세지를 추가할 수 있음.
그리고 local 에서 원격으로 보내는 것을 push 작업이라고 함.

## commit 했는데 git에 적용이 되지 않을때
- commit -> 내 컴퓨터(로컬 저장소) 에만 변경 사항을 저장
- push -> 변경 사항을 GitHub(원격 저장소) 에 업로드
#### vscode에서 source control에서 커밋을 하면?
- 커밋만 실행됨 -> github에는 적영되지 않음
- github에 반영하려면 push를 직접 실행해야 함



## git에 올리기 위한 기본적인 명령어 (프로그램이 아닌 터미널에서 코드로 올리는 법)
``````
git init
```
- 프로젝트를 생성했다면 해당 폴더에서 터미널로 git init을 하여 저장소 초기화 작업을 해줘야함.

```
git status
```
- 깃의 현재 상태를 보는 명령어. 순서가 중요한건 아니고 로딩하면서 종종 사용하며 현 상태가 괜찮은 상태인지 체크.

```
git add .
```
- 해당 폴더에 있는 (. 이 현재 위치를 말함) 모든 파일을 add로 로컬 저장소에 올리는 바구니 리스트에 넣음.

```
git commit -m "test commit"
```
- add 작업 이후 local repository에 해당 파일들을 로딩. -m은 필수 옵션이며 "test commit" 이라는 메세지로 올림.

```
git push
```
- 마지막으로 연결되어있는 원격 repository에 local repository 에 있는 것들을 push 해주면 됨.

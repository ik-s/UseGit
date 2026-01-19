<h1>깃 사용법</h1>

<h3>add, commit</h3>
왜 굳이 2개 입력?
=> 이미지같은건 굳이 기록할 필요가 없기에 기록을 남길 파일부터 고르고 (add)
골라둔걸 기록해두자 (commit)

<img width="567" height="181" alt="image" src="https://github.com/user-attachments/assets/9877a408-7707-458f-a4dc-51b2830f6346" />

staging 한다 : git add  
repository : 저장소  
git status : 상태창 열기 = 어떤 파일들을 staging 했는지, 어떤 파일들이 수정이 됐는지 확인  

<b>git log :</b>   
commit 기록을 한 눈에 파악하고 싶을 때  
--graph 옵션을 넣으면 그래프로 그려줌. 지금은 보잘것 없음  
다만 입력 후엔 Vim 에디터가 켜져서 j, k 키로 위아래 스크롤이 가능하고 q 키로 종료할 수 있음  
git log --all : 한번에 전부 보여줌  
git log --oneline : 한 줄에 보여줌  

=============================================================================

<b>git branch : </b>  
새 곳에서 작업하고 싶을 때 (복사해서 새로운 곳에서) git switch (ex : coupon, main)  
main에 branch를 합치고 싶다 => 기준 브랜치로 이동   
git merge coupon : 같은 곳을 수정하면 conflict가 일어날 수 있음  
해결법 : 원하는 코드만 남기고 add, commit  
git branch -M main : git branch 이름을 main으로 함  


<h3>다양한 git merge 방법</h3>
<img width="567" height="375" alt="image" src="https://github.com/user-attachments/assets/2913750b-27c0-4e6e-a894-ca9afe7d5634" />  

<b>3-way-merge</b>  
각각의 branch에서 commit 후 merge 하는 것  
가끔 main 브랜치에서 커밋이 없고 신규 브랜치에만 커밋이 있다면 신규 브랜치가 main branch가 됨. 이를 fast-forward merge 라고 함.  
이게 싫으면 git merge --no-ff 브랜치명 하면 됨.

<b>브랜치를 지우려면 ?</b>  
merge가 된 애를 삭제하려면 git branch -d 브랜치명 안된 애를 삭제하려면 git branch -D 브랜치명  

<b>rebase & merge</b>  
rebase로 신규 브랜치의 시작점을 main 브랜치의 최근 커밋으로 옮긴 후 ff merge 하는 것  
단, 새 branch에서 git rebase main 해야 함.  
-> commit 내역을 한 줄로 하기 위해서 사용함

<b>squash & merge</b>  
대충 모든 branch를 3-way-merge 해버리면 나중에 참사가 날 수도 있음  
새 branch에서 커밋한 것들을 하나로 모아서 main branch로 순간이동해서 붙여줌.  
git merge --squasgh 브랜치명 (main 브랜치에서 진행)  

<b>파일 복구하는 법</b>  
git restore 파일명 : 최근 커밋 상태로 복구


<b>커밋 자체를 취소하는 법</b>
git revert 커밋아이디 : editor가 뜨는데 I키 누르면 입력, esc 후 :wq 저장 후 닫기  
커밋 아이디는 여러개 취소 가능, 가장 최근꺼 취소는 HEAD

<b>과거로 모든 걸 되롤리기</b>
git reset --hard 커밋아이디 : 커밋아이디 시점으로 완전히 돌아옴  
--soft를 주면 변동사항 지우지말고 스테이징 해놓기  
--mixed : unstage 해놓기

=============================================================================

<b>git push</b>  
: 원격 저장소로 로컬 저장소의 내용을 업로드  
git push -u 원격저장소주소 main  
돌발 상황에 대비하기 위해 원격 저장소에 따로 복구해둘 필요가 있음

<b>git remote</b>  
git에서 변수 문법을 사용 (함수마냥 긴 걸 짧게 쓰기 위해 사용)  
git remote add 변수명 주소  
(git remote add origin www)  
git push -u origin main : -u는 주소를 기억하라는 뜻임. 그래서 다음엔 push만으로 가능  

<b>타인과 협업하기</b>  
git clone 저장소주소 : 원격저장소 파일 그대로 가져오기  
git push를 하려면 원격 저장소가 변해서는 안됨 그래서 pull로 가져와야함. 즉, 원격 저장소의 최신 내역이 로컬 저장소에 반영이 돼있어야만 push 가능함  
git pull 저장소주소 브랜치명 : 원격저장소 내용을 로컬로 합쳐주는 것  

<b>브랜치로 협업하기</b>  
pull request : merge 요청  

===============================================================================

<h3>git flow로 협업하기</h3>

1. main / 2. develop / 3. feature / 4. release / 5. hotfix

main에서 따로 개발할 브랜치를 develop 브랜치를 생성해서 코드 작성  
develop 브랜치에 넣을 기능을 feature 브랜치에서 다룸 ( 길드 기능 : feature/guild ) 이를 develop 브랜치에 merge함  
develop 브랜치를 테스트 하기 위해 release 브랜치 생성, 여기서 여러번의 테스트 진행, 완성되면 main에 합치고 유저들에게 배포, 완성된 것을 develop에도 merge 해서 개발은 계속 진행할 수 있게 해둬야함.   
만약 main에서 발견하지 못한 버그가 나타나는 경우 hotfix 브랜치를 생성해서 빠르게 수정한 후 main과 develop에 merge함.  

<b>Trunk-based : 브랜치 하나만 잘 관리하자</b>  
main에서 쭉 개발하고 중간 중간 추가할 것만 feature 브랜치로 관리하여 merge함


<b>git stash로 코드 잠깐 보관하기</b>  
commit까지 한 파일에 뭔가를 추가했는데 뭔가 애매해서 잠깐 치워버리고 싶네..  
git stash로 임시 저장소에 저장 (staging을 안해놓은 새로운 파일은 stash 안됨)  
git stash save "메모" 로 저장할 때 메모도 입력 가능  
git stash list로 stash 돼있는 코드 목록 출력해서 확인할 수 있음  
저장한 코드들을 꺼내오기 위해서 git stash pop으로 꺼내면 됨 (pop이라 최근꺼부터 꺼냄)  

git stash drop 삭제할id / git stash clear   
   특정 stash 삭제, 	      모든 stash 삭제

삭제할 id는 git stash list 하면 보이는 0, 1, 2 이런 숫자 넣으면 됨  

전체 말고 일부 코드만 git stash 하고싶으면 git stash -p  
그럼 파일을 훑어주면서 stash 할 지 의견을 물어보는데 y/n 으로 잘 대답하면 됨. 

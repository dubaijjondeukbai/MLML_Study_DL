git add .
git commit -m "Update study notes"
git push





colab저장 후 GitHub 쪽에 내 로컬에 없는 새 commit이 생겼기 때문에 push가 막힘
(colab에서 GitHub로 노트북을 저장했을 때 발생함)
GitHub 변경사항을 먼저 받아온 뒤 내 로컬 commit을 그 위에 얹고 다시 push하기

git pull --rebase origin main
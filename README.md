github練習  
既にgitがインストールされていて、  
macはターミナル、  
windowsはgit bashを用いる前提  
  
招待をする側を「オーナー」、  
招待を受ける側を「コラボレーター」とする  
  
linuxコマンドの細かい説明は省きます  
  
——————————ここからオーナーの作業——————————  
下準備  
  
ターミナルを起動し、git-practiceフォルダを作成  
mkdir git-practice  
cd git-practice  
↓  
git init  
↓  
echo "# git-practice" >> README.md  
git add .  
git commit -m "first commit"  
↓  
githubでリモートリポジトリを作成  
Repository nameはgit-practice  
publicを選択  
↓  
git remote add origin https://github.com/jyef/git-practice.git  
git push -u origin master  
↓  
今回はpull requestでのレビュー承認を必須にする  
githubリポジトリのメニューの Settings > Branches から  
Add ruleをクリックしてルールを追加する  
Branch name patternに「master」と入力、  
Require pull request reviews before mergingにチェックを入れる  
Required approving reviewsは1とする  
↓  
Settings > Manage access から  
invite a collaboratorで相手のgithub IDを入力する  
——————————オーナーの作業ここまで——————————  
  
  
——————————ここからコラボレーターの作業——————————  
githubに登録したメールアドレスに招待メールが届いている  
メール内の”accept or decline”をクリック、  
githubのページに飛んだらAccept invitationを押す  
↓  
ローカルリポジトリにコラボレータになった人は、  
まずgithubから最新のコードを取得する必要がある  
リポジトリページのClone or downloadからURLをコピーしてくる  
↓  
ターミナルで  
git clone https://github.com/jyef/git-practice.git  
↓  
cdでgit-practiceフォルダに移動  
↓  
(以下の作業はオーナーとコラボレーター両名ともやるのも良いと思います)  
ブランチを切ってファイルを追加する  
git checkout -b 自分のgithubID  
↓  
touch 自分のgithubID  
↓  
git add .  
↓  
git commit -m ‘ファイルを新規作成’  
↓  
git push origin 自分のgithubID  
↓  
github上でpull requestを作成する  
pull requestタブ等からNew Pull Requestを選択  
base: master ← compare: 自分のgithubID を選択  
Create pull requestを選ぶ  
右枠のReviewersからオーナーを選択  
Create pull requestする  
——————————コラボレーターの作業ここまで——————————  
  
  
——————————ここからオーナーの作業——————————  
オーナーのメールアドレスにpull requestがあった旨のメールが届く  
プルリクエストのページに飛んでFiles changedタブから内容を確認する  
↓  
Review changesで  
相手に「ファイルに内容を追加してください」と依頼をしてみる  
テキストエリアに依頼する旨を書き、  
Request changesを選んでSubmit reviewを押す  
↓  
相手の元に先ほど入力した内容のメールが届く  
——————————オーナーの作業ここまで——————————  
  
  
——————————ここからコラボレーターの作業——————————  
自分のgithubIDファイルに何か内容を記載する  
ターミナルを起動し、git-practiceフォルダに移動する  
↓  
git branch  
でbranch名が自分のgithubIDになっていることを確認する  
もしmasterブランチになっている場合は  
git checkout 自分のgithubID  
でbranchを切り替える  
↓  
vim 自分のgithubID  
で何か内容を記載し、上書き保存する  
  
vim（テキストエディタ）の使い方：  
vimには複数のモードが存在する  
立ち上げた時はノーマルモードになっていて、直接文字の入力はできない  
iキーを押して入力モードに切り替える  
文字を入力したら、escキーを押してノーマルモードに切り替える  
ノーマルモードで :wq と入力し、enter　保存して終了する  
↓  
git add .  
git commit -m ‘ファイルに内容を追加’  
↓  
git push origin 自分のgithubID  
↓  
相手の元にメールが届く  
——————————コラボレーターの作業ここまで——————————  
  
  
——————————ここからオーナーの作業——————————  
プルリクエストを承認する  
Review changesで  
Approveを選択  
テキストエリアに何か書いても良い  
Submit reviewを押す  
↓  
Merge pull requestを押す  
Confirm merge  
——————————オーナーの作業ここまで——————————  
  
  
——————————両方の作業——————————  
リモートリポジトリから最新の情報を取ってきてローカルのワークツリーに反映させる  
git pullでもいいが今回はgit fetchを使う  
  
git fetch origin  
↓  
git branch -a  
ここで表示される  
remotes/origin/masterブランチにリモートから取ってきた情報があるので  
これをmasterブランチに統合する  
↓  
git checkout master  
↓  
git merge origin/master  
remotes/origin/masterの情報をmasterブランチに統合した  
remotesは省略可能なので、origin/master  
↓  
git log —onelineで  
githubのcommitsと内容を一致していることを確認  
——————————両方の作業——————————  # 

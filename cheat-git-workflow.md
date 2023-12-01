
## ローカルにワークスペースを作成(本線)

	# 本線をクローン
	git clone <url>

## ローカルにワークスペースを作成(ブランチ)

	# 本線をクローン
	git clone <url>
	
	# ブランチに切り替え
	git checkout <branch_name>


## コミット

	--------------------------------------- 通常の手順
	# 対象ファイルを指定してステージングする
	git add <files or folders>

	# コミット対象ファイルを確認
	git status
	
	# ローカルリポジトリにコミットする
	git commit

	# リモートリポジトリにプッシュする
	git push

	--------------------------------------- 関連操作
	# ステージング対象から外す
	git reset <files or folders>

	# 差分表示
	git diff <files or folders>		# ローカルファイルとの差分を表示します
	git diff --staged				# ステージングとの差分を表示します

Gitコマンド早見表​
https://qiita.com/kohga/items/dccf135b0af395f69144 ​
​

よく使うGitコマンド19選！使い方を初心者向けにわかりやすく解説​
https://www.sejuku.net/blog/5816 ​
​

サル先生のGit入門　(基本操作、ブランチ、コミットの書き換えまで)​
https://backlog.com/ja/git-tutorial/ ​
​

GitとSVNの違いとは？​
https://aslead.nri.co.jp/products/gitlab/column/differences-between-git-and-svn.html ​
​

Git コンフリクト解消手順​
https://qiita.com/crarrry/items/c5964512e21e383b73da　

[この参考資料](https://qiita.com/gold-kou/items/7f6a3b46e2781b0dd4a0)を基にgit運用をします。
# 各ブランチの役割
|ブランチ名|役割|
|---|---|
|master|本番環境適用するためのブランチ（基本触らない）|
|develop|maseteにマージする前に、作業用ブランチを集約するためのブランチ|
|release|リリース作業用。developから派生させる。mergeされたら削除する|
|feature|担当機能を作成したり修正したりするブランチ|

# 作業用ブランチのライフサイクル
1. 作業用ブランチの作成（developブランチからfeatureブランチを派生させる）
1. 担当している作業をする（例：スケジュール管理機能修正）
1. コミットする
1. プルリク&レビュー依頼([プルリク手順](#プルリクとレビュー))
1. （レビュー指摘がある場合は2〜4を繰り返す）

```bash
# 作業用ブランチ作成
$ git checkout -b feature_xxxxx_name origin/develop
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
                      修正作業
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# 修正状況の確認
$ git status #修正したファイルが赤色になっているはず

# 修正をステージング環境に追加（コミットされる予備軍を溜めておく場所）
$ git add hogehoge.html #修正したファイルが1つだった場合
$ git add hogehoge.html HogehogeController.java #半角スペース区切りで複数ファイル同時登録可能

# ちゃんとaddされているか確認する
$ git status #git add したファイルが緑色になっていればOK

# git add したファイルをコミットする 
# 例）勤怠管理機能作成作業でコントローラを作成した場合
$ git commit -m "勤怠管理機能のコントローラを作成"

# リモートブランチに登録する（これしないと他の人が見たりできない）
$ git push origin feature_#xxxxx_name
```

# ブランチの命名規約
* feature_xxxxx_nameの形式で作成する
* xxxxx: Issuesのタスク番号を5桁で0埋めする
* name: 自分の苗字
* 例）Issuesのタスク番号1と123のブランチ名
`feature_00001_asami`
`feature_00123_asami`

# プルリクとレビュー
## プルリク方法
[公式ドキュメント](https://help.github.com/ja/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request)
### 1.github上でプロジェクトのトップページ
![](https://github.com/GrahamSolution/documents/blob/master/intranet-development/images/pull-request1.png)
### 2.必須項目を埋めてプルリクを投げる
![](https://github.com/GrahamSolution/documents/blob/master/intranet-development/images/pull-request2.png)

## レビュー
管理者はプルリクが来たら、内容とソースコードを確認する。   
問題なければdevelopブランチにマージする。   
問題がある場合は、プルリクを却下して再修正依頼する。

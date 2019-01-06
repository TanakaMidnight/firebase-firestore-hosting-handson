# Step4 サイトと DB を繋いでみよう

ここからは実際の Web アプリを作っていきます。

### 完成イメージ

![](images/04_1.png)

## 01 匿名ログインの有効化

「開発」内の「Authentication」をクリックします。
「ログイン方法」をクリックします。
「匿名」のステータスを「有効」にして「保存」をクリックします。

匿名ログインの詳細はこちら参照。
https://firebase.google.com/docs/auth/web/anonymous-auth

## 02 コードの入手

一から作っていくと時間がかかるため、ある程度出来ているコードを取得します。

`git clone https://github.com/tanakamidnight/`

`cd firebase-handson-code`

## 03 Firebase プロジェクトとコードの関連付け

ターミナルから以下を入力します。  
`firebase use --add`  
すると、  
`? Which project do you want to add?`  
と表示されるので先ほど作成したプロジェクトを選択します。

次に、  
`? What alias do you want to use for this project? (e.g. staging)`
と表示されるので  
`default`  
と入力し、関連付けを行います。

## 04 ローカル環境で確認

ローカルで実行して確認してみましょう。
`firebase serve --only hosting`

## データの挿入の作成

## データの表示の作成

## データを検索して表示の作成

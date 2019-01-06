# Step4 サイトと DB を繋いでみよう

ここからは実際の Web アプリを作っていきます。

### 完成イメージ

![](images/04_01.png)

## 1.匿名ログインの有効化

「開発」内の「Authentication」をクリックします。
「ログイン方法」をクリックします。
「匿名」のステータスを「有効」にして「保存」をクリックします。
![](images/04_02.png)

匿名ログインの詳細はこちら参照。
https://firebase.google.com/docs/auth/web/anonymous-auth

## 2.コードの入手

一から作っていくと時間がかかるため、ある程度出来ているコードを取得します。

`git clone https://github.com/TanakaMidnight/firebase-firestore-hosting-handson-source`

`cd firebase-firestore-hosting-handson-source`

## 3.プロジェクトとコードの関連付け

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

## 4.ローカル環境で確認

ローカルで実行して確認してみましょう。
`firebase serve --only hosting`

## 5.FireStore にデータを書き込む

FireStore にデータを書き込みます。

### データ・モデル

FireStore データは、

- コレクション
  - ドキュメント
    - フィールド
    - サブコレクション

に分割されています。

Restaurants データは以下の通りです。
![](images/04_03.png)

Ratings データは各 Restaurant のサブコレクションとして格納します。
![](images/04_04.png)

TBW データ更新  コード

 ブラウザに戻り、ページをリロードします。
「モックデータを追加」ボタンを押下します。

## 6.FireStore からリアルタイムにデータを表示

Firestore からデータを取得してアプリに表示します。

TBW コード

ブラウザに戻り、ページをリロードします。

## 7.FireStore から 1 度きりのデータを表示

6.ではリアルタイムで変更があった場合、データが更新されます。  
 しかし、常にリアルタイムである必要が無い処理、つまり 1 度だけ取得  したい時もあるはずです。  
その場合の書き方について以下で解説します。

TBW コード

## 8.データの並び替えとフィルタリング

 データの取得が出来るようになり、リストが表示されるようになりました。

実際のアプリでは、並び替え(ソート)や絞り込み（フィルタ）などが必要になってくると思います。
 その場合の書き方について、以下で解説します。

TBW コード

## 9.インデックスの設定

クエリの  パフォーマンスを向上されるために、FireStore にインデックスを設定します。

TBW コード

## 10. トランザクションの設定

データの不整合を防ぐためにデータの作成、更新、削除時にトランザクションを  貼りたいことがあるはずです。
その場合の書き方について以下で解説します。

TBW 　コード

## 11. セキュリティの設定

Step3 で  データベースの作成を行いましたが、その際のセキュリティルールで「テストモード」を選択していました。  
この「テストモード」はすべてのユーザーがデータベースの読み書きが行えてしまい、セキュリティに問題が発生しています。  
セキュリティルールを以下で正しく設定します。

firestore/firestore.rules

```
service cloud.firestore {
  match /databases/{database}/documents {

    // Restaurants:
    //  - 読み取り・作成：認証済ユーザーは可能
    //  - 更新：認証済ユーザーは可能、バリデーションを行う
    //  - 削除：禁止
    match /restaurants/{restaurantId} {
      allow read, create: if request.auth != null;
      allow update: if request.auth != null
                    && request.resource.data.name == resource.data.name
      allow delete: if false;

      // Ratings:
      //  - 読み取り：認証済ユーザーは可能
      //  - 作成：認証済ユーザーでuserIdが一致している場合は可能
      //  - 更新・削除：禁止
      match /ratings/{ratingId} {
        allow read: if request.auth != null;
        allow create: if request.auth != null
                      && request.resource.data.userId == request.auth.uid;
        allow update, delete: if false;
      }
    }
  }
}

```

 ターミナルから以下を入力します。

```
firebase deploy --only firestore:rules
```

以上で完成です。  
お疲れ様でした。

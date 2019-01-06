# Step1 Firebase を使うための準備をしよう

## 01 Firebase にログイン

https://firebase.google.com/

## 02 Firebase CLI のインストール

https://firebase.google.com/docs/cli/?hl=ja

Firebase CLI のインストール

```
npm install -g firebase-tools
```

Firebase にログイン

```
firebase login
```

## 03 Firebase プロジェクトを作る

![](01_1.png)

Firebase サイト、 「コンソールへ移動」、「プロジェクトの追加」をクリックします。  
「プロジェクトの追加」画面が表示されたらプロジェクト名に「handson」と入力、「Firebase 向け Google アナリティクスのデータ共有にデフォルトの設定を使用する」のチェックを外し、「次へ」をクリックします。  
「データ共有のカスタマイズ」画面が表示されたら、値を変更せず、「プロジェクトの作成」をクリックします。

しばらく待つと、プロジェクトが作成されます。

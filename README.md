# 動く数学教材工房（外部JSON版）

## いちばん簡単な使い方

1. ZIPを展開します。
2. `index.html`をダブルクリックします。
3. 画面の「プロジェクトフォルダを選択」を押します。
4. このREADME・index.html・materials.jsonが入っているフォルダを選びます。

Chrome / Edge / Safariの新しい版を想定しています。

## Webサイトへ公開する場合

フォルダ構成を変えずに、そのまま静的サイトへアップロードしてください。
Web上では `materials.json` と各教材HTMLが自動で読み込まれ、フォルダ選択は不要です。

## 教材を追加する方法

1. 新しい1ファイルHTMLを `materials/` に置きます。
2. `materials.json` に教材情報を1件追加します。

例:

```json
{
  "id": "recurrence-cobweb",
  "title": "漸化式と蜘蛛の巣図法",
  "course": "数学B",
  "unit": "数列",
  "level": "高校発展",
  "description": "漸化式の反復と固定点への収束を可視化します。",
  "file": "materials/recurrence-cobweb.html"
}
```

`index.html`本体を編集する必要はありません。

## 注意

- 生徒版は教材ライブラリをlocalStorageへ書き込みません。
- エディタで変更したコードはページを閉じると消えます。必要なら「HTML保存」を使ってください。
- 教材はsandbox付きiframeと外部通信禁止CSPの中で実行します。

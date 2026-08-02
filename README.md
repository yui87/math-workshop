# 動く数学教材工房

数学の動的教材を閲覧し、HTMLコードを編集・実行するための静的Webアプリです。

## 使い方（生徒向け）

公開URLをブラウザで開くだけで使えます。ダウンロードや準備は不要です。

1. 公開URLを開きます。
2. 左の一覧から教材を選びます。
3. 「実行結果」タブでそのまま試すか、「コード」タブでLLM（ChatGPT・Claude・Geminiなど）に改変してもらったHTMLを貼り付けて実行します。

編集した内容はページを閉じると消えます。手元に残したい場合は「HTML保存」を使ってください。

---

以下は、教材の追加・管理を行う先生向けの説明です。

教材一覧は `materials.json`、各教材本体は `materials/` フォルダ内のHTMLファイルとして管理します。教材を追加する際に、`index.html`を編集する必要はありません。

## フォルダ構成

```text
dynamic_math_workshop_external/
├─ index.html
├─ materials.json
├─ README.md
├─ material-entry-template.json
└─ materials/
   ├─ quad.html
   ├─ trig-ratio.html
   ├─ unit-circle.html
   └─ ...
```

## ローカルで試す方法（先生向け）

1. ZIPファイルを展開します。
2. `index.html`をブラウザで開きます。
3. 「プロジェクトフォルダを選択」を押します。
4. `index.html`と`materials.json`が入っているフォルダを選択します。

ブラウザの制限により、HTMLをダブルクリックして開いた場合は、外部JSONや教材HTMLを自動取得できないことがあります。そのため、初回にフォルダ選択が必要です。

Webサーバー上で公開した場合は、`materials.json`と教材HTMLが自動で読み込まれ、フォルダ選択は不要です。

## 教材を追加する方法

### 1. 教材HTMLを配置する

新しい1ファイルHTMLを、`materials/`フォルダへ入れます。

例：

```text
materials/recurrence-cobweb.html
```

教材HTMLは、HTML・CSS・JavaScriptをすべて含む1ファイル形式にしてください。

外部ライブラリ、CDN、API、外部通信には依存しない構成を推奨します。

### 2. materials.jsonへ登録する

`materials.json`へ、教材情報を1件追加します。

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

各項目の意味：

* `id`：教材を識別する重複しないID
* `title`：教材一覧に表示する名前
* `course`：数学I、数学II、数学B、数学Cなど
* `unit`：教材の単元
* `level`：高校基礎、高校標準、高校発展など
* `description`：教材の目的や内容
* `file`：教材HTMLへの相対パス

JSONでは、項目と項目の間にカンマが必要です。ただし、最後の項目の後にはカンマを付けません。

追加後、GitHubにコミット・pushすれば、公開URLにも自動的に反映されます。

## 教材を変更する方法

既存教材の内容を変更する場合は、`materials/`内の対応するHTMLファイルを差し替えます。

教材名、科目、単元、説明などを変更する場合は、`materials.json`を編集します。

## 教材を削除する方法

1. `materials.json`から対象教材の項目を削除します。
2. 不要になった教材HTMLを`materials/`フォルダから削除します。

HTMLファイルだけを削除し、JSONの登録を残すと、教材の読み込みエラーになります。

## 生徒の操作

生徒は次の操作ができます。

* 教材の閲覧
* 教材HTMLコードの確認・コピー
* コードの一時的な編集
* 編集したHTMLの実行
* HTMLファイルとしての保存
* LLMへ渡す改変プロンプトの作成

生徒がエディタ上で変更した内容は、教材ライブラリや`materials.json`には保存されません。

## 安全機構

教材HTMLは、次の制限を付けたiframe内で実行されます。

```html
sandbox="allow-scripts"
```

`allow-same-origin`は付けていません。

また、教材実行時には外部通信などを禁止するContent Security Policyを挿入します。

ただし、無限ループや非常に重い計算によって、ブラウザのタブが一時的に動かなくなる可能性はあります。内容を確認できないHTMLは実行しないでください。

## 教材作成時の推奨条件

LLMへ教材の作成を依頼する場合は、次の条件を指定してください。

1. HTML・CSS・JavaScriptを含む1ファイルHTMLにする
2. 外部ライブラリ、CDN、API、外部通信を使わない
3. 表示と説明を日本語にする
4. PC・タブレット・スマートフォンで見やすくする
5. スライダーなどの操作部分とグラフを近くに配置する
6. 数式的な正確さを優先する
7. 回答は完成したHTMLコードだけにする

## 公開時の注意

`index.html`、`materials.json`、`materials/`フォルダの位置関係を変更せず、フォルダ一式を公開してください。

ファイル名を変更した場合は、`materials.json`の`file`も同じ名前に変更してください。

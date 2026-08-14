# Typing Lab

ブラウザ上でタイピング速度・誤入力・キーボード差を記録・比較するための実験ツール集です。

公開ページ:

https://pozihamebaystar.github.io/typing-error-logger/

## Features

Typing Lab には現在、3つのツールがあります。

### Typing Error Logger

通常のタイピング練習と誤入力記録を行います。

- 日本語文章のローマ字入力
- 複数のローマ字表記に対応
  - `shi / si / ci`
  - `sha / sya`
  - `chi / ti`
  - `tsu / tu`
  - `fu / hu`
  - `ja / jya / zya`
  - など
- 正打鍵・誤打鍵の記録
- タイムスタンプ記録
- JSON / CSV 出力
- 誤入力傾向の解析用ログ生成

ページ:

https://pozihamebaystar.github.io/typing-error-logger/typing.html

---

### Keyboard A/B Test

2台のキーボードを同一条件で比較するためのA/Bテストです。

同じ問題順、同じ制限時間で入力し、以下の指標を比較します。

- 生WPM
- 実効WPM
- 正確率
- 誤打鍵数
- 隣接キー誤打率
- 隣接キー誤打数
- 重複打鍵数
- 完了問題数

問題順はSeedを使って固定されるため、A/B間で同一条件を再現できます。

実施順は以下から選択できます。

- A → B
- B → A
- ランダム

ページ:

https://pozihamebaystar.github.io/typing-error-logger/keyboard-ab-test.html

#### 指標の定義

**生WPM**

全printable keydown数を基準に計算します。  
誤打鍵も含むため、実際にどれだけ高速に指を動かしていたかに近い指標です。

```text
Gross WPM = 全打鍵数 / 5 / 経過時間[分]
```

**実効WPM**

正しく受理された打鍵数を基準に計算します。

```text
Effective WPM = 正打鍵数 / 5 / 経過時間[分]
```

誤打鍵後の復帰時間もそのまま経過時間に含まれるため、
「速く打てるがミスが多いキーボード」と
「少し遅いが正確なキーボード」を比較しやすくしています。

**正確率**

```text
Accuracy = 正打鍵数 / 全打鍵数
```

**隣接キー誤打率**

QWERTY配列上で、期待していたキーに隣接するキーを誤って押した割合です。

---

### HID Key Depth Probe

WebHIDを利用して、キーボードがPC側へ送信しているHIDレポートを調査するための実験ページです。

- `keydown`
- `keyup`
- 高精度タイムスタンプ
- WebHID input report
- HIDレポート内の変動byte解析
- JSON / CSV 出力

ページ:

https://pozihamebaystar.github.io/typing-error-logger/hid-test.html

> [!NOTE]
> 磁気式キーボード内部ではストローク量を計測していても、その生データがPCへ公開されているとは限りません。
> また、ブラウザは通常のKeyboard HID Collectionへの直接アクセスを制限する場合があります。
>
> このページは「キー深度を必ず取得できるツール」ではなく、
> 利用可能なHIDインターフェースや生レポートを調査するための実験用ツールです。

## Recommended Browser

Google Chrome / Microsoft Edge などのChromium系ブラウザを推奨します。

特に `HID Key Depth Probe` は WebHID を使用するため、対応ブラウザが必要です。

GitHub PagesはHTTPSで配信されるため、WebHIDを試す環境として利用できます。

## How to Use

1. 公開ページを開く
2. 使用したいツールを選択する
3. 日本語IMEをOFFにする
4. タイピングまたは実験を開始する
5. 必要に応じてJSON / CSVを保存する

A/Bテストを行う場合は、可能な限り以下の条件を揃えることを推奨します。

- 同じ姿勢
- 同じ机・椅子
- 同じパームレスト条件
- 同じ制限時間
- キーボード以外の設定を変更しない
- 複数セット実施する
- A→BだけでなくB→Aも試す

1回だけの測定では、ウォームアップや疲労の影響を受けるため、
複数回の測定結果を比較する方が有効です。

## Data

入力データは基本的にブラウザ内で処理されます。

ログは、ユーザーがJSON / CSVの書き出し操作を行った場合にローカルへ保存されます。

現在のページには、タイピングログを外部サーバーへ自動送信する処理はありません。

## File Structure

```text
typing-error-logger/
├── index.html
├── typing.html
├── keyboard-ab-test.html
├── hid-test.html
└── README.md
```

- `index.html`  
  Typing Lab のトップページ

- `typing.html`  
  通常タイピング・誤入力記録

- `keyboard-ab-test.html`  
  キーボードA/B比較

- `hid-test.html`  
  WebHID調査

## Local Use

静的HTMLだけで構成されているため、通常のページはローカルでも利用できます。

ただしWebHIDにはSecure Contextが必要なので、`hid-test.html` はGitHub Pagesやlocalhost経由での利用を推奨します。

簡易HTTPサーバーの例:

```bash
python -m http.server 8000
```

その後、

```text
http://localhost:8000/
```

をブラウザで開きます。

## Purpose

このプロジェクトは、単純な最高WPMだけではなく、

- 高速化するとどのような誤入力が増えるか
- キーボードによってミス傾向が変わるか
- 隣接キー誤打が増えるか
- 高速だが低精度なのか
- 少し遅いが実効速度では優れているのか

といった点を、実際の打鍵ログから比較することを目的としています。

## License

現時点ではライセンスを明示していません。

第三者による再利用・改変・再配布を許可したい場合は、MIT Licenseなどを追加してください。

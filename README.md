# Typing Lab

Typing Lab は、ブラウザ上でタイピング速度・誤入力・キーボード差を記録・分析するための実験ツール集です。

公開ページ:

https://pozihamebaystar.github.io/typing-error-logger/

## Tools

### Typing Error Logger

日本語文章をローマ字入力しながら、タイピング速度と誤入力を記録します。

主な機能:

- 日本語ローマ字タイピング
- 複数のローマ字表記に対応
- 生WPM / 実効WPM / 正確率の計測
- keydown / keyup の時系列記録
- 誤打鍵の集計
- タイプミス事象の自動分類
- JSON / CSV 出力

タイプミス分析では、連続した誤打鍵をひとつの「ミス事象」としてまとめ、以下のようなパターンを推定します。

- 隣接キー誤打
- 同一指領域での誤打
- 意図しない同時押し
- 次キーの先行入力
- 文字順序の入れ替わり
- 文字飛ばし候補
- 次チャンクへの先走り
- 前キーの重複
- オートリピート
- 高速再入力候補

ページ:

https://pozihamebaystar.github.io/typing-error-logger/typing.html

---

### Keyboard A/B Typing Experiment

2台のキーボードを、同一問題順・同一制限時間で比較するA/Bテストです。

比較できる主な指標:

- 生WPM
- 実効WPM
- 正確率
- 誤打鍵数
- 隣接キー誤打率
- 隣接キー誤打数
- 重複打鍵数
- 完了問題数

問題順はSeedによって固定されるため、A/B間で同一条件を再現できます。

実施順は以下から選択できます。

- A → B
- B → A
- ランダム

ページ:

https://pozihamebaystar.github.io/typing-error-logger/keyboard-ab-test.html

#### 指標

**生WPM**

```text
Gross WPM = 全printable keydown数 / 5 / 経過時間[分]
```

誤打鍵も含めた、実際の打鍵量に近い速度指標です。

**実効WPM**

```text
Effective WPM = 正しく受理された打鍵数 / 5 / 経過時間[分]
```

誤打鍵からの復帰時間も経過時間に含まれるため、速度と正確さの両方を反映します。

**正確率**

```text
Accuracy = 正打鍵数 / 全printable打鍵数
```

**隣接キー誤打率**

QWERTY配列上で、期待キーの近傍にあるキーを誤って押した割合です。

---

### 運転免許学科 Typing Trainer

普通四輪自動車の運転免許学科に関連する内容をタイピングしながら学習するページです。

主な機能:

- 普通免許学科に関連する例文
- 分野別出題
- タイピング速度・正確率の計測
- タイプミス自動分析
- 各問題の学習ポイント表示
- JSON / CSV 出力

学習対象には、以下のような内容を含みます。

- 基本的な安全運転
- 信号・標識
- 歩行者・自転車
- 速度・車間距離
- 合図・進路変更
- 追越し
- 交差点
- 駐車・停車
- 踏切
- 夜間・悪天候
- 高速道路
- 事故・故障時の対応
- 法改正に関する項目

ページ:

https://pozihamebaystar.github.io/typing-error-logger/driver-license-typing.html

> [!IMPORTANT]
> このツールは学習補助を目的としたものであり、公安委員会・警察・指定自動車教習所などが提供する公式試験問題集ではありません。
> 実際の試験対策では、最新の公式資料・教本・教習所教材も確認してください。

---

### HID Key Depth Probe

WebHIDを利用して、キーボードがPC側へ送信しているHIDレポートを調査するための実験ページです。

主な記録対象:

- keydown
- keyup
- 高精度タイムスタンプ
- WebHID input report
- HIDレポート内の変動byte
- JSON / CSV

ページ:

https://pozihamebaystar.github.io/typing-error-logger/hid-test.html

> [!NOTE]
> 磁気式キーボード内部でストローク量を計測していても、その生データがPC側へ公開されているとは限りません。
> また、ブラウザは標準的なKeyboard HID Collectionへの直接アクセスを制限する場合があります。
>
> このページは、キー深度を必ず取得できるツールではなく、利用可能なHIDインターフェースや生レポートを調査するためのものです。

## Supported Romaji Variants

代表的な複数表記に対応しています。

例:

```text
し      shi / si / ci
しゃ    sha / sya
しゅ    shu / syu
しょ    sho / syo
ち      chi / ti
つ      tsu / tu
ふ      fu / hu
じゃ    ja / jya / zya
```

入力判定は、単一の固定ローマ字文字列との完全一致ではなく、許容される入力経路を追跡して行います。

## Recommended Browser

Google Chrome / Microsoft Edge などのChromium系ブラウザを推奨します。

特に `HID Key Depth Probe` は WebHID を使用するため、WebHID対応ブラウザが必要です。

## Data Handling

タイピングデータはブラウザ内で処理されます。

JSON / CSV の書き出し操作を行った場合、ログはユーザー端末へ保存されます。

サイト上の各ツールは、タイピングログを外部サーバーへ自動送信することを前提としていません。

## File Structure

```text
typing-error-logger/
├── index.html
├── typing.html
├── keyboard-ab-test.html
├── driver-license-typing.html
├── hid-test.html
└── README.md
```

## Local Use

静的HTMLで構成されているため、通常のタイピングページはローカルでも利用できます。

簡易HTTPサーバーを利用する場合:

```bash
python -m http.server 8000
```

その後、ブラウザで以下を開きます。

```text
http://localhost:8000/
```

WebHIDを利用する場合はSecure Contextが必要なため、HTTPS環境またはlocalhostでの利用を推奨します。

## Purpose

このプロジェクトでは、単純な最高WPMだけでなく、以下のような観点からタイピングを分析することを目的としています。

- 高速化したときにどのようなミスが増えるか
- キーボードによってミス傾向が変化するか
- 隣接キー誤打が多いか
- 次キーを先に押す傾向があるか
- 複数キーをほぼ同時に押す傾向があるか
- 速度と正確率のバランスがどう変化するか
- 誤打鍵が単発なのか、連続したミス事象なのか

## Disclaimer

タイプミス分類は、ブラウザで取得できるキーイベントとタイミング情報から推定したものです。

たとえば、物理的にはキーを押していてもアクチュエーションポイントに達せずOSへ入力されなかった場合、その事実を通常の `keydown` ログだけから判別することはできません。

そのため、分析結果は入力挙動を理解するための補助情報として利用してください。

## License

ライセンスは現在明示していません。

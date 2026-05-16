# hsp-script

HSP3/OpenHSP のスクリプトを書く・直す・レビューする・説明するための Codex skill です。

## 対応範囲

- 通常の HSP3 ウィンドウ付きスクリプト
- HSPCL 向けのコンソールスクリプト
- HSP3Dish 向けスクリプト
- HGIMG4 向けスクリプト
- `.as` モジュールファイル
- OpenHSP リポジトリ内の sample、help、test 用コード

このskillは、CodexがHSPらしい書き方を保てるように、ラベル、`repeat`/`loop`、`gosub`、コマンド形式の文、HSPプリプロセッサ、OpenHSPリポジトリ内の慣例を参照するための指示をまとめています。

## インストール

このリポジトリを Codex の skills ディレクトリに clone します。

```bash
git clone https://github.com/<user>/hsp-script.git ~/.codex/skills/hsp-script
```

環境によっては、Codexの再起動またはskillの再読み込みが必要です。

## 使い方

プロンプト内で HSP、HSP3、OpenHSP、`.hsp`、`.as` などに触れると、このskillが使われます。明示的に呼び出すこともできます。

```text
Use $hsp-script to write a small HSP3 windowed sample.
```

プロンプト例:

```text
HSP3で簡単な時計スクリプトを書いて
```

```text
この .hsp ファイルの構文ミスをレビューして
```

```text
OpenHSPのsample/hsp3dish向けにタッチ入力のサンプルを作って
```

## ファイル構成

- `SKILL.md`: Codex向けのskill定義と発火条件。
- `references/hsp-notes.md`: HSPの構文メモ、コード例、ランタイム別の注意点、OpenHSPリポジトリの配置メモ。
- `agents/openai.yaml`: skill一覧表示などで使うUIメタデータ。
- `README.en.md`: 英語版README。

## 注意

このリポジトリは、単体のskillフォルダとしてインストールすることを想定しています。リポジトリ直下に `SKILL.md` がある構成にしてください。

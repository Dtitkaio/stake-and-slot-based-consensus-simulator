# consensus-simulator-of-PoSA

PoSA simulator は、Proof of Stake and Authority (PoSA) を使用して異なる Authority Validators の選出アルゴリズムを使った際のステークの変化をシミュレートするためのツールです。このシミュレータは、異なるバリデータ選択戦略がネットワークの分散性にどのように影響するかを分析するためのツールになります。

## 目的

このシミュレータの主な目的は、バリデータのステーク量の変化をエポックごとに追跡し、異なるバリデータ選択戦略が Validators 間のステーク分布に与える影響を観察することです。

## 設定

シミュレータの設定は、`config.py`ファイルで管理します。主な設定項目は以下の通りです：

- `EPOCHS`: シミュレーションを行うエポック数。
- `AUTHORITY_COUNT`: 一つのエポックにおける権限バリデータの数。
- `TOTAL_REWARD`: エポックごとの総報酬量。
- `REWARD_RATIO`: Authority Validators と Candidate Validators 間での報酬分配比率。
- `STAKE_DISTRIBUTION`: 初期ステーク分布。
- `SELECTION_STRATEGY`: Authority validators の選択方法を指定できます。利用可能な選択戦略は以下の通りです：
  - `stake`: ステーク量に基づいて上位のバリデータを選択します。
  - `random`: 完全にランダムにバリデータを選択します。ステーク量に関係なく、全バリデータが同じ確率で選出されます。
  - `multiplicative_ageing`: ステーク量と stake ageing（選択されていない期間）の積に基づいてバリデータを選択します。
  - `exponential_ageing`: ステーク量と stake ageing の指数関数に基づいてバリデータを選択します。`multiplicative_ageing`よりも ageing の影響度が高くなります。
  - `binomial_ageing`: ステーク量と stake ageing に基づく二項分布を用いてバリデータを選択します。
- `OUTPUT_MODE`: シミュレーション結果の出力モードを設定できます。利用可能な出力モードは以下の通りです。
  - `console`: 結果をコンソールに直接出力します。簡易に結果を確認するのに適しています。
  - `file`: 結果をファイルに出力します。出力は`output/`ディレクトリ内のタイムスタンプ付きの CSV ファイルに保存されます。データの後処理や分析を行いたい場合に使ってください。

## 使い方

シミュレーションを実行するには、以下の手順に従ってください：

1. 必要なライブラリをインストールするために、`requirements.txt`ファイルを使用して依存関係をインストールします。

   ```
   pip install -r requirements.txt
   ```

2. `config.py`ファイルを編集して、シミュレーションの設定を調整します。

3. シミュレータを実行します。

   ```
   python simulator.py
   ```

4. 出力モードをファイルまたは標準出力に設定することができます。ファイル出力を選択した場合、結果は `output/` ディレクトリ内のタイムスタンプ付きの CSV ファイルに保存されます。

## シミュレーション結果の読み方

シミュレーションの結果は、選択した出力モードに応じて表示されます：

- **ファイル出力**: `output/` ディレクトリに保存された CSV ファイルを開きます。ファイルには、シミュレーションの設定と、各エポックでのステーク分布が含まれています。
- **標準出力**: コンソールに表示される出力から、各エポックごとのステーク分布を確認できます。

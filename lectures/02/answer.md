# 第2回 解答

## 演習

- 使ったモデル・設定（`result.json` の `config` から）：
- 自分で学習を実行したか（`executed_training_myself`）：はい / いいえ（実行できた範囲：　）
- 学習前：`format_rate` =　 / `content_rate` =　
- 学習後：`format_rate` =　 / `content_rate` =　
- 退行した質問：
- 学習後に残った失敗と、その型（根拠なしの質問に断定した / 根拠ありの質問に確認要求で逃げた / 形式の崩れ）：
- 知識を問う質問（セクション 6）の結果（学習前の分類 → 学習後の分類）と気づいたこと：
- 学習で変わったこと・変わらなかったこと：

## 宿題

- 取り組んだレベル：実装
- 変えた設定やデータ：FAQやGROUNDED,UNGROUNDED,TEST_EXTRA_GROUNDED,TEST_EXTRA_UNGROUNDEDを「松江でイベントを行う設定」で変更．
- 結果（比較表や数字）：
- "before": {
    "label": "before",
    "n": 20,
    "format_rate": 0.25,
    "content_rate": 0.0,
    "both_rate": 0.0,
    "seconds": 17.5
  },
  "after": {
    "label": "after",
    "n": 20,
    "format_rate": 1.0,
    "content_rate": 0.55,
    "both_rate": 0.55,
    "seconds": 56.2
  },
- ファインチューニングが向く場面・向かない場面についての考察：
- 向く：形式を揃えたい時，特定のデータを元にし，それ以外のものを元にしたくないとき
- 向かない：早く済ませるべきタスク．secondsが17.5→56.2と3倍近く伸びていることから．

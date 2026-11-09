# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い： 「の意味は？」という質問形式が追加されたからか，の意味はなんでしょうか？という質問に変化していた．
- `--trace` で見えたツール呼び出し（ツール名と引数）：
[tool call]   make_quiz({'lecture': 2})
[tool return] make_quiz -> {"lecture": 2, "term": "PEFT", "question": "「PEFT」の意味は？", "answer": "モデルの全パラメータではなく、ごく一部や追加した小さなパラメータだけを学習する手法の総称。必要なGPU…
[usage] RunUsage(cost=Decimal('0.0004613'), details={'text_prompt_tokens': 896}, input_text_tokens=896, input_tokens=896, output_tokens=77, requests=2, tool_calls=1)
- 1つの質問での LLM 呼び出し回数（`requests`）：2回
- 追加したツールと、docstring に書いた説明：make_quiz
指定した回の用語から 1つを選び、
  確認問題と答えを返す。
  「第2回の確認問題を出して」のように、
  復習用の問題を求められたときに使う。
  引数: {"lecture": {"type": "integer"}}

## 宿題

- 取り組んだレベル：基礎 
- やったこと：
instructionの指示文で用語集に見つからないことは、推測で断定せず「用語集にはない」と伝える。
というところを変更し，以下のようにした．
「用語集に見つからないことは、一番近い言葉を絶対に探し，その定義を載せて回答する．」
両者に「三権分立について教えて」という質問を行なった．
- 結果：
変更前の回答：
AIエンジニアリング講座（AIE2026）の用語集には「三権分立」の定義や登録は見当たりません。

なお、一般的な社会科・政治の用語としての「三権分立」は、国家権力を「立法権」「行政権」「司法権」の3つに分け、それぞれ異なる機関に属させることで権力の集中や濫用を防ぎ、国民の権利や自由を守る仕組み（ Montesquieu の権力分立論に基づく民主主義の基本原則）を指します。

関連する回：（関係する回については用語集に該当回がないため記載しません）

--- trace ---
[tool call]   search_glossary({'query': '三権分立'})
[tool return] search_glossary -> 用語集に「三権分立」は見つかりませんでした。…
[usage] RunUsage(cost=Decimal('0.0006090'), details={'text_prompt_tokens': 680}, input_text_tokens=680, input_tokens=680, output_tokens=162, requests=2, tool_calls=1)

変更後の回答：
「三権分立」は、国家の権力を立法（法律を作る）・行政（政治を行う）・司法（法律に基づいて裁く）の3つに分け、それぞれ異なる機関に担当させることで権力の集中や暴走を防ぎ、国民の権利を守るための政治・法制度の基本的な仕組みです。

AIエンジニアリングの分野において、これに直接対応する用語は用語集に登録されていませんが、AIエージェントの安全性を高める仕組みである **「ガードレール」** の概念に通じる考え方と言えます。AIエージェントにおいても、行動のルールを定める役割（システムプロンプト）、実際にツール等を使って処理を実行する役割、そして結果を検証する仕組みなどを適切に分離・管理することが安全なシステム構築において重要視されます。

関連する回：第3回
--- trace ---
[tool call]   search_glossary({'query': '三権分立'})
[tool return] search_glossary -> 用語集に「三権分立」は見つかりませんでした。…
[tool call]   search_glossary({'query': '権限'})
[tool return] search_glossary -> [{"term": "ガードレール", "lecture": 3, "definition": "エージェントが望ましくない行動や出力をしないように設ける制約や検査。指示文でのルール、ツールの権限を絞る、出力をチェックする、重要な操作の前に…
[tool call]   search_glossary({'query': 'システムプロンプト'})
[tool return] search_glossary -> [{"term": "システムプロンプト", "lecture": 1, "definition": "利用者の質問とは別に、モデルの振る舞い（役割、口調、守るべきルールなど）を指定する入力。Pydantic AIでは Agent の in…
[usage] RunUsage(cost=Decimal('0.0011565'), details={'text_prompt_tokens': 1930}, input_text_tokens=1930, input_tokens=1930, output_tokens=231, requests=4, tool_calls=3)
- 気づき・疑問：
変更後のtraceの様子を見ると「三権分立」が用語集に見つからなかった後に，「権限」という用語に変えて探している．
人がGoogle検索をするときに文言を変えて変化を確かめる様子と同様のことが起こっていることを感じた．
また，システムプロンプトについても定義の確認を再び行なっているところが面白いと感じた．
類似用語というより，言葉の抽象度を上げて検索の引っ掛かりをしやすくしているようにも見えるところが不思議に感じた．

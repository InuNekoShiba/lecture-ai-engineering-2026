# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：glossary_search_glossary
- STEP 2 の [tool call]：glossary_search_glossary({'query': '3レベル'})
- STEP 3 の [tool call]： fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
- STEP 4 の [tool call]：aws_aws___search_documentation({'search_phrase': 'Amazon S3 Versioning overview', 'topics': ['general']})
- 気づき・疑問：MCPサーバーを設定に追加することでエージェントから用語集の検索、Webページの取得、AWSのドキュメント検索を利用できた。traceを見ると質問内容に応じて異なるツールが選ばれ、それぞれに必要な引数が渡されていることを確認できた。


## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：app/mcp_server.py に `server.tool()(tools.get_lecture_summary)` を追加し、講義の要点を取得するツールをMCPサーバーから公開した。
- 結果：ツール一覧に `glossary_get_lecture_summary` が追加された。「第2回では何を学びますか？」と質問したところ、`glossary_get_lecture_summary({'lecture': 2})` が呼び出され、第2回の講義概要が返された。`uv run pytest -q` では21件すべてのテストが成功した。
- 気づき・疑問：エージェント側のコードを変更しなくても、サーバー側でツールを公開することで、エージェントがツール一覧を取得して利用できることが分かった。また、traceを見ることで、モデルが選んだツールと引数、返された結果を確認できた。

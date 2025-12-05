# WOM-Educational-Scenario-Pack-for-WOM-Kernel-
WOM Kernel（Weekly Operation Model Kernel）は、 「週次で動くサプライチェーン計画・意思決定のミニマル OS カーネル」を目指して開発されているプロジェクトです。 本 Educ_Pac（Educational Scenario Pack）は、 WOM Kernel の構造・原理・可能性を 学生・研究者・コンサルタント・企業の企画部門 の方々に体験していただくための公式教材セットです。 実運用の実績はこれからですが、 Educ_Pac のシナリオを通じて「経営OSへの進化の予感」を感じ取っていただくことを目的としています。

Educ_Pac — Educational Scenario Pack for WOM Kernel
Version 0.9 Draft — for GitHub
WOM Kernel（Weekly Operation Model Kernel）は、
「週次で動くサプライチェーン計画・意思決定のミニマル OS カーネル」を目指して開発されているプロジェクトです。
本 Educ_Pac（Educational Scenario Pack）は、
WOM Kernel の構造・原理・可能性を 学生・研究者・コンサルタント・企業の企画部門 の方々に体験していただくための公式教材セットです。
実運用の実績はこれからですが、
Educ_Pac のシナリオを通じて「経営OSへの進化の予感」を感じ取っていただくことを目的としています。
________________________________________
目的（Purpose）
Educ_Pac の目的は、以下の3点です：
1.	週次 PSI 計画 × シミュレーション（PSI Simulator）
WOM Kernel が「ロットID と weekly loop」で世界をどのように“再現”するかを学ぶ。
2.	Hooks/Plugins による拡張性の体験
demand allocation / capacity constraint / expiry / FEFO など、
ロジックを差し替えるだけで世界が変わるという OS 的構造を理解する。
3.	経営意思入れ（Decision Hub）の雰囲気を掴む
c-speed ショックや capacity policy の変更など、
“週次の意思決定”が全体最適に影響する様子を体験する。
________________________________________
内容（Contents）
Educ_Pac は、4つの公式シナリオセットで構成されます。
ディレクトリ構成：
educ_pack/
  README.md
  scenarios/
    EDU_SIMPLE_LINEAR_DEMAND/
    EDU_RICE_HARVEST_BUFFER/
    EDU_OPT_CAPACITY_FLOW/
    EDU_PROCESS_SHOCK_C_SPEED_DROP/
  notebooks/
    00_edu_overview_wom_kernel.py
    10_edu_simple_linear_demand.py
    20_edu_rice_harvest_buffer.py
    30_edu_opt_capacity_flow.py
    40_edu_process_shock_cspeed.py
________________________________________
公式シナリオ 1
EDU_SCN1 — シンプル線形需要モデル
Simple Linear Consumer Goods Supply Chain
用途：WOM Kernel の“最初の一歩”教材
特徴：
•	需要：ほぼ一定の consumption speed（c-speed）
•	供給：一定ペースで生産（Capacity も弱め）
•	Demand Allocation：単純な FIFO / 先着順
•	可視化：
o	在庫量（Inventory）の週次推移
o	出荷量（Shipment）
o	基本的な PSI グラフ
•	使用プラグイン：最小構成
目的：
•	WOM Kernel の基本挙動（PSIロットの移動 / histログ / simple KPI）を理解する
•	「WOMとは何をするものか？」を気軽に体験する
________________________________________
公式シナリオ 2
EDU_SCN2 — 米の収穫 × 平坦な消費
Seasonal Supply × Flat Consumption (Rice Supply Chain)
用途：季節性と在庫戦略の教材
特徴：
•	秋に P-lots（生産）が集中（収穫の山）
•	消費 c-speed は年間ほぼ一定
•	Demand Allocation Plugin を切り替えることで
o	A：上流に溜める戦略
o	B：下流にバッファを寄せる戦略
が比較できる
目的：
•	「需要は平ら、供給は山」という典型的問題を在庫戦略でどう処理するか理解する
•	Educ_Pac の看板教材
________________________________________
公式シナリオ 3
EDU_SCN3 — Optimizer × Capacity / Flow 制約
Capacity-Constrained Network Planning
用途：最適化（LP/MIP）とサプライチェーン計画の橋渡し教材
特徴：
•	Demand Allocation の後、Optimiser Plugin が
node_capacity と edge_flow を最適化
•	Supply Planning は wom.psi_simulator が制約下で計画
目的：
•	需要側の希望 vs 制約を持つ供給側の実行計画
という“整合問題”を OS 的に理解する
•	経営工学の学生やコンサルの研修に最適
________________________________________
公式シナリオ 4
EDU_SCN4 — C-Speed 落下ショック × プロセス減産
Demand Shock & Process Node Downshift
用途：意思入れ（Decision Hub）の雰囲気を体験
特徴：
•	leaf_node の c-speed（消費速度）が急減
•	それに対して decision_hub が
大口バッチロット（Process Node）の減産を発動
•	P-lots（イベント）の生成パターンが変化する
目的：
•	「需要ショック→weekly 判断→上流プロセスの減産」
という 経営OS 的な意思決定サイクル を体験する
•	AI Agent 連携の未来像にもつながるテーマ
________________________________________
notebooks/ について
各 notebook-like .py は VS Code / Jupyter 拡張で
セル単位に実行できるスタイルになっています。
構成は以下に統一：
1.	初期設定（import, logger）
2.	cfg / calendar の設定
3.	WOM Kernel 実行（PSI Simulator）
4.	KPI 出力
5.	PSI グラフ描画
6.	World Map の簡易ネットワーク可視化（あれば）
GUI は“あえて凝らない”。
WOM Kernel の本質（PSIとweekly loop）に集中するため。
________________________________________
出力される KPI（ミニマルセット）
•	fill_rate
•	total_inventory
•	shipped / received
•	backlog（SYN-lot 数）
•	特定 node の PSI 系列（I/S の折れ線）
________________________________________
今後の拡張
•	FEFO / Expiry / 冷凍チェーンなどの industry plugins を追加
•	Decision Hub をより高度な rule-based → 小規模 ML へ発展
•	Pyomo/PuLP を使った network optimisation シナリオ
•	AI Agent と weekly loop の直結（プロトタイプ版）
________________________________________
参加方法
Educ_Pac はオープンソース（MIT License）で公開予定です。
Pull Request / Issue / Discussions への参加を歓迎しています。
研究機関での利用、授業サンプルへの組み込みも自由です。
________________________________________
ライセンス
MIT License
（WOM Kernel 本体・教育シナリオ・notebook-like scripts を含む）
________________________________________
まとめ
Educ_Pac は、
**「WOM Kernel の世界を誰でも体験できる公式教材」**として設計しています。
実務適用はこれからですが、
週次ループで世界を動かす感覚、
ロットが流れるサプライチェーンのダイナミズム、
そして“経営OS”の手触りを
少しでも感じていただければ幸いです。


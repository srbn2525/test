# 特定人物が出演するAI動画（PV/ドラマ風）制作リサーチ

## 目次
1. [アプローチの全体像](#アプローチの全体像)
2. [主要AIツール比較](#主要aiツール比較)
3. [必要な素材](#必要な素材)
4. [予算感](#予算感)
5. [推奨ワークフロー](#推奨ワークフロー)

---

## アプローチの全体像

特定の人物が出演するPV/ドラマ風AI動画を作るには、大きく **2つのアプローチ** がある。

### アプローチA：クラウドサービス型（手軽・高コスト）
- Kling AI、Runway、Sora などのSaaSツールに人物の参照画像をアップロード
- 「Elements」や「Identity Lock」機能で顔の一貫性を維持しながら動画生成
- **メリット**: セットアップ不要、すぐ使える
- **デメリット**: 月額課金、細かい制御が限定的

### アプローチB：オープンソース型（高自由度・技術力必要）
- Wan 2.2 + LoRAで特定人物を学習させて動画生成
- ComfyUI上でワークフロー構築
- **メリット**: 完全な制御、一度学習すれば無制限生成、商用利用可（Apache 2.0）
- **デメリット**: GPU必要、セットアップに技術力が必要

---

## 主要AIツール比較

### 1. Kling 3.0（クラウド型 / おすすめ度: ★★★★★）
- **特徴**: 人間の顔・動きのリアルさでトップクラス
- **顔の一貫性**: 「Elements 3.0」機能で参照画像4枚から顔・体型・服装を維持（"Director Memory"機能）
- **動画長**: 3〜15秒のマルチショット生成対応
- **解像度**: ネイティブ4K対応
- **料金**:
  - Standard: $6.99/月
  - Pro: $25.99/月
  - API: 約$0.10/秒
- **PV/ドラマ向き度**: ◎（マルチショット対応でストーリー性のある映像が作れる）
- 参考: [Kling AI](https://klingai.com/global/) / [レビュー](https://cybernews.com/ai-tools/kling-ai-review/)

### 2. Runway Gen-4.5（クラウド型 / おすすめ度: ★★★★☆）
- **特徴**: Text-to-Videoリーダーボード1位（Elo 1,247）、映像制作者向けの細かい制御
- **顔の一貫性**: リファレンスシステムで視覚的アイデンティティ＋声の特徴を維持
- **料金**:
  - Standard: $12/月
  - Pro: $28/月
  - Unlimited: $76/月
- **PV/ドラマ向き度**: ◎（プロ向け編集機能が充実）
- 参考: [Runway](https://runwayml.com/) / [比較記事](https://invideo.io/blog/kling-vs-sora-vs-veo-vs-runway/)

### 3. OpenAI Sora 2（クラウド型 / おすすめ度: ★★★★☆）
- **特徴**: 単一人物の顔リアリズムで最高峰、「Characters」機能（旧Cameos）
- **顔の一貫性**: 95%+の一貫性。iOSアプリで本人が3〜10秒の動画を撮影して登録
- **⚠️ 重要な制限**: 本人がSoraアプリで自撮り録画する必要あり。他人の写真アップロードは不可。1動画あたり最大2キャラクターまで
- **動画長**: Plus: 5秒(720p) / Pro: 最大20秒(1080p) / API: 最大25秒
- **料金**:
  - ChatGPT Plus: $20/月（制限あり、480p〜720p）
  - ChatGPT Pro: $200/月（拡張アクセス、1080p）
  - API: $0.10〜$0.50/秒
- **PV/ドラマ向き度**: ○（リアリズムは最高だが、本人録画が必須なのがネック）
- 参考: [Sora 2ガイド](https://wavespeed.ai/blog/posts/openai-sora-2-complete-guide-2026/) / [比較記事](https://www.imagine.art/blogs/veo-3-vs-top-ai-video-generators)

### 4. Google Veo 3.1（クラウド型 / おすすめ度: ★★★★☆）
- **特徴**: リップシンク・ボディランゲージで最強、参照画像4枚で顔の一貫性維持
- **顔の一貫性**: カメラアングルが変わっても顔・服装・体型が安定
- **料金**:
  - Google AI Ultra: $249.99/月
  - API: $0.40/秒
- **PV/ドラマ向き度**: ◎（セリフがある場面に最適）

### 5. Wan 2.2 + LoRA（オープンソース / おすすめ度: ★★★★★）
- **特徴**: Alibaba発、Apache 2.0ライセンス、27Bパラメータ（MoE）
- **顔の一貫性**: LoRAで特定人物を学習させれば100%一貫性を維持
- **料金**: 無料（GPUコストのみ）
- **必要GPU**: RTX 4090（24GB VRAM）で動作可能、A6000推奨
- **PV/ドラマ向き度**: ◎（完全な制御が可能、商用利用可）
- 参考: [GitHub](https://github.com/Wan-Video/Wan2.2) / [LoRAトレーニングガイド](https://www.apatero.com/blog/wan-2-2-lora-training-person-method-guide-2025)

### 6. HeyGen Avatar IV（クラウド型 / おすすめ度: ★★★☆☆）
- **特徴**: トーキングヘッド（話す人物映像）に特化、175言語以上対応
- **顔の一貫性**: アバター作成で完全に一貫性維持
- **料金**:
  - Creator: $29/月（実質$59/月程度）
  - Pro: $99/月
- **PV/ドラマ向き度**: △（プレゼン・説明動画向き、PV/ドラマには向かない）
- 参考: [HeyGen](https://www.heygen.com/) / [レビュー](https://aitoolanalysis.com/heygen-review/)

### 7. Minimax / Hailuo AI（クラウド型 / おすすめ度: ★★★★☆）
- **特徴**: キャラクターの微表情（唇の震え、目を細める等）が優秀。1080pネイティブ
- **顔の一貫性**: フレーム間の顔・服装・背景の一貫性が高い
- **動画長**: 6〜8秒/クリップ
- **料金**:
  - Standard: $9.99/月（1,000クレジット）
  - Unlimited: $94.99/月
- **PV/ドラマ向き度**: ◎（キャラクター主導のシネマティック映像に強い）
- 参考: [MiniMax Hailuo 2.3](https://www.minimax.io/news/minimax-hailuo-23)

### 8. Vidu Q3（Shengshu Technology）（クラウド型 / おすすめ度: ★★★☆☆）
- **特徴**: 連続コンテンツ（シリーズもの）特化。最大7枚の参照画像で複数キャラ管理
- **顔の一貫性**: 構造化されたサブジェクトライブラリでモジュラーにアセット再利用
- **料金**:
  - Free: 800クレジット
  - Standard: $10/月 / Creator: $15/月
  - API: 約$0.0375/秒（最安クラス）
- **PV/ドラマ向き度**: ○（シリーズものに特化、単発PVなら他ツールの方が良い）
- 参考: [Vidu SXSW 2026発表](https://www.manilatimes.net/2026/03/16/tmt-newswire/pr-newswire/vidu-unveils-the-worlds-first-ai-solution-for-animated-series-production-at-sxsw-2026/2300902)

### ツール比較まとめ

| 用途 | 最適ツール |
|---|---|
| **顔リアリズム（単体ショット）** | Sora 2 Pro |
| **マルチショット一貫性** | Kling 3.0 / Runway Gen-4 |
| **セリフ・リップシンク** | Veo 3.1 |
| **コスパ重視** | Kling 3.0（〜$0.10/秒） |
| **完全制御・商用利用** | Wan 2.2（LoRA学習） |
| **プロ編集ワークフロー** | Runway Gen-4.5 |

---

## 必要な素材

### クラウドサービス型（Kling / Runway / Sora）の場合

| 素材 | 必要量 | 備考 |
|---|---|---|
| **顔写真** | 4〜10枚 | 正面・斜め・横顔など多角度 |
| **全身写真** | 2〜5枚 | 服装・体型の参考用 |
| **動画素材** | あれば尚良 | 表情・動きの参考用 |
| **声のサンプル** | 1〜5分 | 音声クローン用（HeyGenなどの場合） |

### オープンソース型（Wan 2.2 + LoRA）の場合

| 素材 | 必要量 | 備考 |
|---|---|---|
| **顔写真** | 20〜50枚（推奨） | 最低10枚、高品質を目指すなら50枚以上 |
| **写真の条件** | 多様性が重要 | 正面/斜め/横顔、笑顔/真剣/驚きなど多表情 |
| **解像度** | 512×512 or 1024×1024 | リサイズ・背景除去が必要 |
| **動画クリップ** | あれば10〜30本 | 動きのパターン学習用 |
| **キャプション** | 各画像にタグ付け | WD14 Taggerで自動生成可 |

### 音声クローンツール

| ツール | 必要な音声量 | 特徴 | 料金 |
|---|---|---|---|
| **ElevenLabs** | 1〜5分 | 英語の忠実度が業界最高 | $5〜99/月 |
| **Fish Audio** | 10秒以上 | TTS-Arena 1位、多言語対応 | $9.99/月〜 |
| **Resemble AI** | 10秒 | ElevenLabsの1/3の価格、セルフホスト可 | 低価格 |
| **Chatterbox（OSS）** | 5秒 | MITライセンス、ブラインドテストでElevenLabsに勝利 | 無料 |

### 写真撮影のコツ
- 屋内外の異なるロケーションで撮影
- 異なる服装で撮影（特定の服に過学習させないため）
- 自然光を活用（過度な加工は避ける）
- 顔アップと全身の両方を用意
- カメラ目線だけでなく、視線を外したショットも含める

---

## 予算感

### ローバジェット（月額 $7〜30 / 約1,000〜4,500円）

| 項目 | ツール | 費用 |
|---|---|---|
| 動画生成 | Kling Standard | $6.99/月 |
| 音楽 | Suno AI / Udio（無料枠） | $0 |
| 編集 | CapCut / DaVinci Resolve（無料版） | $0 |
| **合計** | | **約$7〜10/月** |

- 月5〜10本の短い動画（5〜15秒）が作成可能
- 品質は中程度、SNS投稿レベル

### ミドルバジェット（月額 $50〜150 / 約7,500〜22,500円）

| 項目 | ツール | 費用 |
|---|---|---|
| 動画生成 | Kling Pro + Runway Pro | $25.99 + $28/月 |
| 音楽 | Suno Pro | $10/月 |
| 音声 | ElevenLabs Starter | $5/月 |
| 編集 | DaVinci Resolve（無料版） | $0 |
| **合計** | | **約$70〜100/月** |

- 複数ツールを使い分けて高品質な動画を制作
- 30秒〜1分のPV制作が現実的

### ハイバジェット（月額 $200〜500+ / 約30,000〜75,000円）

| 項目 | ツール | 費用 |
|---|---|---|
| 動画生成 | Sora Pro + Runway Unlimited + Kling Pro | $200 + $76 + $25.99/月 |
| リップシンク | Veo 3.1 API | $0.40/秒（従量） |
| 音楽 | Suno Premier | $30/月 |
| 音声 | ElevenLabs Scale | $99/月 |
| 編集 | Adobe Premiere Pro | $22.99/月 |
| **合計** | | **約$400〜500+/月** |

- プロレベルのPV/ドラマが制作可能
- 複数ショット、セリフ、音楽すべて高品質

### オープンソース型（初期投資 + ほぼ無料運用）

| 項目 | 費用 | 備考 |
|---|---|---|
| GPU（RTX 4090） | 約25〜30万円 | 既に持っていれば不要 |
| GPU（クラウドレンタル） | 約$1〜3/時間 | RunPod, Vast.ai等 |
| LoRA学習 | 1回24時間程度（A6000の場合） | RTX 4090で2〜3日 |
| 動画生成 | 電気代のみ | 一度学習すれば無制限 |
| **ランニングコスト** | **ほぼ$0** | GPU所有の場合 |

---

## 推奨ワークフロー

### PV/ドラマ風動画の制作フロー

```
1. 企画・絵コンテ作成
   └─ ChatGPT / Claude でシナリオ・絵コンテ作成

2. 素材準備
   ├─ 出演者の写真撮影（20〜50枚）
   ├─ 音声サンプル収録（1〜5分）
   └─ 参照画像の加工（リサイズ・背景除去）

3. 人物学習（オープンソースの場合）
   ├─ LoRA学習（Wan 2.2 + AI Toolkit）
   └─ 学習完了まで24時間〜3日

4. 動画生成
   ├─ Image-to-Video でキーフレームから動画化
   ├─ マルチショット生成（Kling 3.0）
   └─ セリフシーン生成（Veo 3.1 / HeyGen）

5. 音楽・SE制作
   ├─ BGM: Suno AI / Udio
   └─ SE: ElevenLabs / 効果音素材

6. ポストプロダクション
   ├─ DaVinci Resolve / Premiere Pro で編集
   ├─ カラーグレーディング
   ├─ テロップ・エフェクト追加
   └─ 最終書き出し
```

### おすすめの組み合わせ

#### 初心者向け（すぐ始めたい）
- **Kling 3.0**（動画生成）+ **CapCut**（編集）+ **Suno**（音楽）

#### 中級者向け（品質重視）
- **Kling 3.0 + Runway Gen-4.5**（動画生成）+ **DaVinci Resolve**（編集）+ **Suno**（音楽）+ **ElevenLabs**（音声）

#### 上級者向け（完全制御）
- **Wan 2.2 + LoRA**（動画生成）+ **ComfyUI**（ワークフロー）+ **DaVinci Resolve**（編集）+ **Suno**（音楽）

---

## 注意事項

- **肖像権・同意**: 出演者本人の書面による同意を必ず取得すること
- **各プラットフォームの規約**: AI生成コンテンツの利用規約を確認すること
- **ディープフェイク規制**: 国・地域によってはAI生成人物映像に規制がある場合がある
- **品質のばらつき**: AI動画はまだ完璧ではなく、生成→選別→再生成のサイクルが必要
- **顔の歪み**: 複雑なアングルや速い動きでは顔が歪むことがある（特にクローズアップ）

---

## 参考リンク

- [15 AI Video Models Tested: Kling 3.0 vs Veo 3.1 (TeamDay.ai)](https://www.teamday.ai/blog/best-ai-video-models-2026)
- [Best AI Video Generator Comparison (massive.io)](https://massive.io/gear-guides/the-best-ai-video-generator-comparison/)
- [Kling vs Sora vs Veo vs Runway (invideo.io)](https://invideo.io/blog/kling-vs-sora-vs-veo-vs-runway/)
- [HeyGen vs Synthesia 2026 (WaveSpeedAI)](https://wavespeed.ai/blog/posts/heygen-vs-synthesia-comparison-2026/)
- [Wan 2.2 GitHub](https://github.com/Wan-Video/Wan2.2)
- [Wan 2.2 LoRA Training Guide (Apatero)](https://www.apatero.com/blog/wan-2-2-lora-training-person-method-guide-2025)
- [Kling AI 公式](https://klingai.com/global/)
- [HeyGen レビュー (AI Tool Analysis)](https://aitoolanalysis.com/heygen-review/)
- [10 Best Image-to-Video AI Tools 2026 (Atlas Cloud)](https://www.atlascloud.ai/blog/guides/10-best-image-to-video-ai-tools-in-2026-from-static-photos-to-cinematic-masterpieces)

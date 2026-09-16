# アニメ・ゲーム版 作品協力調査

ブルーアーカイブ版・ポケットモンスター版と同じ2人協力型カードゲームの別バージョンです。元版とポケモン版のファイルは変更しません。`publish/anime-game/` にも公開用ファイルを配置します。

## 起動

```powershell
python -m http.server 8765 --directory anime-game
```

ゲームは `http://localhost:8765/`、カード編集は `http://localhost:8765/ContentEditor.html` です。2人接続は既存版と同じPeerJS外部サービスを使います。

## カードと出現条件

- 収録カードはアニメ359枚、ゲーム300枚、合計659枚です。明確な続編・派生作があるものは「～シリーズ」の1枚にまとめています。アニメは2005～2014年と2020年以降の作品を厚めに収録しています。
- アニメは初回放送または劇場公開年、ゲームは初作の初出年を採用します。シリーズの年はシリーズ初作の年です。国や媒体によって発売日が違う場合は最初の公開年を基準にします。
- ホストはアニメ・ゲームの媒体と放送・発売年を5年単位でON/OFFできます（1960～1964年から2025～2029年まで）。媒体と年の両方が一致するカードだけから25枚抽選します。候補が25枚未満ならルーム作成を止めます。現時点の収録作は2025年までです。
- ホバー情報は約0.5秒後に現れ、発売・放送年を表示します。カスタムメモを設定しても年は残ります。盤面ごとのカード情報は参加者にも同期します。
- `ContentEditor.html` では作品名、媒体、年、メモを編集できます。編集内容はブラウザに自動保存されます。ゲームへ反映するには `content.json` を書き出し、このフォルダの同名ファイルと置き換えてください。

収録作品と年の管理元は [`catalog.tsv`](catalog.tsv)、[`catalog_anime_additions.tsv`](catalog_anime_additions.tsv)、[`catalog_anime_priority.tsv`](catalog_anime_priority.tsv)、[`catalog_game_additions.tsv`](catalog_game_additions.tsv) です。新しい版を生成するときは `python anime-game/tools/build_data.py`、続いて `python anime-game/tools/build_variant.py` を実行します。データ再生成は手動編集した `content.json` を上書きします。

年の基準の例として、ドラゴンボールの初回放送年は[公式シリーズ年表](https://en.dragon-ball-official.com/about/dragon_ball_history.html)、葬送のフリーレンの初回放送年は[アニメ公式サイト](https://frieren-anime.jp/1st-anniv/)、スーパーマリオブラザーズの発売年は[任天堂の製品ページ](https://www.nintendo.com/jp/famicom/software/smb1/index.html)で確認できます。収録範囲は知名度を基準にした編集リストで、網羅的な作品目録ではありません。

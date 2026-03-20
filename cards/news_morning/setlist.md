---
title: 怪談ちゃんの朝イチニュース
speaker: 38
speed: 0.95
loop: false
pause_between: 1200
---

<!-- ============================================
  15分 朝のニュース・天気・今日は何の日
  テーマ: リアルタイムAPI取得 × AIトーク
  想定時間: 約15分
  ※ auto-news / auto-weather / auto-today は
    AIがリアルタイムにデータ取得＆トーク生成
============================================ -->

# オープニングジングル
[type: jingle]
[file: media/jingle1.mp3]
[overlay: media/opening.jpg]
[duration: 10]
[fadeOut: 2]
[speakAt: 2.5]
[speakText: おっはよ〜！怪談ちゃんの朝イチニュース、はじまるっす！]

# オープニングトーク
[type: talk]
[bgm: media/bgm_chill.mp3]
[emotion: happy]
[intensity: 0.9]
おはようございます！怪談ちゃんっす！
今日もニュースと天気をお届けするっすよ〜。
コーヒー片手に聴いてくれたら嬉しいっす！

# コーナージングル
[type: jingle]
[file: media/jingle2.mp3]
[duration: 6]
[fadeOut: 2]
[speakAt: 1.5]
[speakText: 今日は何の日コーナー！]

# 今日は何の日
[type: auto-today]
[bgm: media/bgm_chill.mp3]

# つなぎトーク
[type: talk]
[emotion: happy]
へぇ〜、面白いっすね！
先輩方は知ってたっすか？
さて、続いてはニュースコーナーっす！

# コーナージングル
[type: jingle]
[file: media/jingle2.mp3]
[duration: 6]
[fadeOut: 2]
[speakAt: 1.5]
[speakText: ニュースコーナー！]

# ニュース
[type: auto-news]
[bgm: media/bgm_chill.mp3]

# つなぎトーク
[type: talk]
[emotion: neutral]
いろんなニュースがあったっすね。
世の中、毎日いろいろ動いてるっす。
さぁ、最後は天気予報いくっすよ！

# コーナージングル
[type: jingle]
[file: media/jingle2.mp3]
[duration: 6]
[fadeOut: 2]
[speakAt: 1.5]
[speakText: 全国天気予報！]

# 全国天気予報
[type: auto-weather]
[bgm: media/bgm_chill.mp3]

# お便りコーナー
[type: comments]
[bgm: media/bgm_chill.mp3]

# エンディングトーク
[type: talk]
[bgm: media/bgm_chill.mp3]
[emotion: happy]
[intensity: 0.8]
はい！朝イチニュース、今日はここまで！
天気も確認できたし、準備万端っすね。
朝から聴いてくれた先輩方、ありがとうっす！
今日も一日、がんばっていきましょう！
それじゃ、いってらっしゃい！

# エンディングジングル
[type: jingle]
[file: media/jingle1.mp3]
[overlay: media/ending.jpg]
[duration: 12]
[fadeOut: 3]
[speakAt: 2]
[speakText: 朝イチニュース、また明日！いってらっしゃい！]

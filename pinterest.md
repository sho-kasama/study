## pinterestで良いと思ったサイトを分析していく


1: <a href="http://petitringo.net/top/">comocomo.cafe</a>
  - `background-attachement:fixed;`を使用すると背景画像は固定されるのでスクロールした際におしゃれ感が出る？(語彙力）
  - フレックスボックスが使われてなく、floatが使われていた
  
2: <a href="http://kazuki-art.com/">kazuki.art</a>
  - `writing-mode: 'vertical-rl`を使って文字方向を決めてる
  - アニメーションは擬似要素で指定されていて、`animation: scrollDown 1.25s cubic-bezier(.165,.84,.44,1) 0s infinite normal;`が使われている

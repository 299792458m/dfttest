gitの使い方が良くわかってないので変なところがあっても気にしないでください

# dfttest
181224
-SSE/AVX/AVX2の最適化調整 あくまで自分の環境(i7-4790K Haswell)で速くなるように (AVX2はあまり効果がないが)
 opt=4をAVX2用にした
-アライメント調整したらちょっと早くなったような気がする
-dither処理最適化 (ditherの値↓により処理分離させるようにした)
 dither<100
  1スレッド用最適化コード
 100<=dither<200
  dither処理が律速になるとき用にdll内でスレッド分割 
  (逆に、avisynth+でMTを使うときはdither<100の方が無意味にスレッドが増えなくて良い)
 200<=dither<300
  従来互換 元々のコード(なので遅い)

-バイナリはSSE2でコンパイルされているので、SSE2以上必須
 openmpを使っているのでvcomp140.dllが要る(VisualC++2015/2017再配布用パッケージをインストールすること)
 x64はちゃんと確認してない(一応コンパイルが通るようにはしてあるだけ)
 

this is fork of dfttest 1.9.4.3 and some speed tune for my enviroment is added.
mainly tuned at dither function(it costs wastefully a lot).
And not tested a lot.


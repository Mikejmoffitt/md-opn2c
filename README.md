# MD用YM3438アダプター・MD YM3438 Adapter

![PCB Render](guide-img/pcb.png)

![Installed unit](guide-img/installed.jpeg)

# 概要・Overview
このアダプターでメガドライブ初代はYM3438(OPN2C)が対応できるようになります。　元々の音源のステータスレジスターの読み込みの違いを解決するとジックがついています。　その上[オープンソースのとリップルバイパス](https://github.com/tianfeng33/triple-bypass-Version-2))より綺麗な音源のミクサーとバッファーがついていて、元々のヘッドホンも専用ライン出力が使えるようになります。

元々のFM音源(YM2612)を抜いて使用することも可能です。　その場合は[3BP](https://github.com/tianfeng33/triple-bypass-Version-2))と同じような使い方になります。　その場合でもヘッドホンもラインアウトも利用できます。

メガドラVA0の基板を参考しながら書いたんですが、基本的にすべての初代の基板は互換はずです。

This adapter facilitates the install of a YM3438 (OPN2C) in a Sega Mega Drive or Genesis console. Glue logic is present to solve status read bugs that invoke different behavior between the original YM2612 and the CMOS YM3438. In addition, a mixing and buffering circuit (courtesy of [the open source Triple Bypass PCB](https://github.com/tianfeng33/triple-bypass-Version-2)) to both handle the new YM3438 and also provide clean mixing for other signals. The buffer circuit also has provisions to output audio to the original signal path, so that the mono audio output and the headphone jack both work as designed.

An original YM2612 may also be installed, in which case this PCB simply provides a new mixing circuit and buffer, similar to the [Triple Bypass PCB](https://github.com/tianfeng33/triple-bypass-Version-2)).

These instructions were written using a Japanese VA0 unit as a reference, but principally can apply to any Megadrive or Genesis with a YM2612 in it.

## 互換の本体・Compatibility

メガドライブ（初代）VA0-VA6は互換です。 ジェネシス２のVA3でも動くかもしれませんが、未確認なので一応保証ができません。
Compatible with Genesis 1 / Megadrive 1 VA0-VA6. Genesis 2 VA3 (with discrete YM2612) may work, but has not been tested, and I cannot provide installation instructions at this time.

# 設置・Installation

## マザーの修正・Motherboard Preparation

マザーに付ける前に修正が必要です．

With the adapter unit ready, some work must be done to the Megadrive motherboard.

YM2612を外して、どこか保存しします。（依頼要らないけど捨てないでください！）　下の縦列のコンデンサーも外しましょう。(C40, C41, C42, C43, C44, C61, C62)

Desolder and remove the YM2612, and the column of capacitors below it (C40, C41, C42, C43, C44, C61, and C62).

![Motherboard top-side component removal diagram](guide-img/prep-topside.jpeg)

底面に赤く示している部品を外します。 (R34, R37, R40, R41, C45, C46, C47, C48)。　右の黄色いやつを外して、左のバツが付いている黄色い部品をその位置に移動します (R53/R43, R40/R41)。　C41とC43の穴にリンクを入れてください。

下面に印刷がないので下の絵を参考してください。

On the underside, remove the components marked in red (R34, R37, R40, R41, C45, C46, C47, C48). Remove the components marked in yellow (R53 and R43) and move them to the spot marked in yellow (R40 and R41). Install a link between the two pins of capacitors C41 and C43.

As there is no silkscreen on the underside of most revisions, the diagram will be a helpful reference. 

![Motherboard bottom-side SMT component removal diagram](guide-img/prep-underside.jpeg)

新しいミックスされた音声は元々のFM音源の端子に入ります（21ピンと20ピン）。　そのために元々のヘッドホンもモノの出力が使えます。

The new audio will enter through what used to be the MOL and MOR pins for the OPN2, at pins 21 and 20 respectively. The mixed stereo signals enter the original mixing circuit alone, where it then enters the headphone amp as well as the mono mixdown for the CXA-1145.

## 音源付け方・Installation of FM Sound Source

YM3438か先抜いたYM2612をアダプターの上面に付けます。　下面にピンが邪魔になってしまうので上面にハンダ付けても大丈夫です。　音源のICは完全に平にならないんですが、全ての端子がちゃんとついていたら問題がありません　(少距離は大丈夫です)。

アダプターのウラ面にジャンパーがあります。　音源の種類によって左側か右側を半田で閉めて下さい。　両方のジャンパーを同じ設置するようにご注意下さい。

Attach either a YM3438 or the previously removed YM2612 in the open position on the adapter PCB. As the header pins on the underside may obstruct your soldering, it is fine to apply solder on the top side. The IC may not lay perfectly flat, but if all pins are firmly soldered a slight distance is acceptable.

On the underside of the adapter, use solder to close the jumpers based on the sound source type. You must set both sets of jumpers in the same configuration.

| 設定Config | IC類Chip |
|------------|----------|
| `(---  )`  | YM2612   |
| `(  ---)`  | YM3438   |

## 基板の付け方・Installation in Megadrive

先の準備を完全似できたか確認しておいてください。

Please be sure you have completed the Motherboard Preparation steps first.

YM2612の位置にYM3438のアダプターを入れて、下面にハンダ付けます。　上面に5本の配線が必要です。　下の表を参考して

Place the assembled YM3438 adapter unit in the position that once held the original YM2612, and solder it in place on the underside. On the top, five wires are necessary to feed in the various audio signals that compliment the FM sound source. The table below describes the positions shown in the annotated picture below.

| 信号Signal | 出所Location |
|------------|--------------|
| PSG        | C40 (-)      |
| SL1        | C42 (-)      |
| SR1        | C44 (-)      |
| SL2        | C61 (-)      |
| SR2        | C62 (-)      |

![Signal wiring diagram](guide-img/wiring-topside.jpeg)

これで、どうやって出力を本体外に出すか自分の決まりです。　もしヘッドホンの端子が十分でしたらここまでストップしても大丈夫です。　しかし、ヘッドホンのアンプより直接LINE出力したらノイズが少なくなるので、LINEの出力はおすすめです。

アダプターにOUTのパッドがあります。　そこに配線付けて端子に繋げたらLINEの出力が可能です。

With everything installed, it's up to you how you want to route the audio out. If the headphone jack alone is adequate, you may stop here. However, I recommend a dedicated line out connection, as the headphone amp does introduce some noise.

The 'LINE OUT' pads are present so you may run a stereo output to the back of the console, or to some other connector of your choosing. Stereo audio will be present via the headphone jack, and mono audio will be delivered out of the rear A/V connector.

# フィルター調整・Filter Adjustment

アダプタのLPFフィルターの遮断周波数は約16KHzになっていますが、もしVA3みたいな~3KHzは希望だったらコンデンサー交換通じて可能です。　示しているコンデンサーを150Pfに交換すると、LPFの遮断周波数は~3KHzになります。　元々のは33pFです。

The filter situated on the adapter has a fairly high cutoff frequency of about 16KHz. Unlike the triple bypass PCB, there isn't a selection of filter parameters, but if a stronger filter that sounds similar to the VA3 is desired, you may exchange the two highlighted capacitors for 150pF units to achieve a ~3.5KHz cutoff. The originals are 33pF.


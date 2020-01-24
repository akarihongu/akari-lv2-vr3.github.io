# akari-lv2-vr3.github.io
【FB修正】
全体
・1080px以上
1080pxを超えるとinner幅におさまらず、画面の大きさに沿って
広がってしまう要素が複数あります。最大の2560pxになっても、
コンテンツ自体は「1080pxに全ておさまっている状態」が理想ですね！


→私の検証の仕方の前提として、「検証」画面上の幅指定の数値を「2560」に設定してみると一目瞭然でした…。これまでカーソルドラッグで画面を動かせる範囲でしか確認しておらず、ミスを多々見逃していました。ご指摘ありがとうございます！


大きく崩れている要素：
1「NAVI」 →左右margin修正
2「RECRUET」 →<p>テキスト幅修正（この時点では見本通り改行）
3「NEWS」の3つのブログ記事　→<p>テキスト幅修正（この時点では見本通り改行）

1「NAVI」
このヘッダー部分の親要素である「header」の左右marginをautoにする。

header {
    max-width: 1080px;
    margin-right: auto;
    margin-left: auto;
    height: 70px;
    color:#333;
}

2「RECRUET」

まず、画面幅によって飛び出していた<p>テキスト部分に、取りあえず見本通り改行を挿入してみる。

次にaboutの画像・<p>テキスト要素それぞれの左右marginを整える。
さらに、<p>を見本通りの幅・余白にしても文字の改行が一文字分乱れてしまうので「letter-specing」で整える。

.about-copy1 {
    margin-left: 70px;
}

.about-copy2 {
    margin-right:70px;
}

.about-p {
    line-height: 1.7；
    margin-top: 30px;
    margin-bottom: 30px;
    letter-spacing: -0.1em;
}

→スマホサイズでも崩れないようメディアクエリの方も修正。

.about-copy1 {
        margin: 0;
    }

スマホサイズの時に、テキストが<br>での改行を無効化して表示するよう指定。
（参照）
https://www.terakoya.work/css-br-element-none-howto/

br {
        display: none;
    }

→これにより、後続の「NEWS」のブログ記事のテキスト部分のスマホサイズにおける改行も無効化した。


3　「NEWS」の3つのブログ記事
2と同様、まずは飛び出していた記事のテキスト部分に、見本通り改行を挿入してみる。

また、これらの<p>にはwidthを指定しておらず画面サイズに合わせてどこまでも広がってしまっていたので、見本通りの幅に指定。

.news-p {
    max-width: 650px;
    margin-right: 16px;
}


・「768px以下
要素間の余白が開きすぎている
paddingやmarginで要素が圧迫されている
最初値の320pxまで、カンプ通りになっているか再度確認してみてください


まず全体をチェックし、違和感ある場所を検証しながら修正。

・タイトル「日本の会社を、みちびく会社」の文字幅を調節。

.headmain-ttl {
    font-size: 36px;
    font-weight: bold;
    line-height: 1.7;
}

その他の余白調節：

・「ーSERVICEー」とそのすぐ下のコンテンツの間の余白
→innerに余計なmargin190pxがあったので削除し調節。

・「ーNEWSー」前後の余白をmarginで調整。
.topic-n {
    margin-top: 20px;
    margin-bottom: 101px;
}


・フォントカラーがカンプと異なっている
結構あるあるなのでベースになっているフォントカラーが合っているかは今後も要チェックです◎

→フォントカラー指定していなかった
.headmain-ttl , .headmain-copy p, .srv, .about-p, .t-ttl
 のテキストに、

color: #333333;
を指定。


ヘッダー
・320〜370pxでNAVIとRECRUITがくっついてしまう

→ヘッダーのロゴ「NAVI」や「RECRUIT」のwidthを固定していたのを「max-width」とし、さらにNAVIとRECRUITがくっついてしまわないよう二つの要素の間に10％のmarginを指定。

.header-img {
    max-width: 130px;
    height: auto;
    margin-right: 10%;
}


メインビジュアル
・769〜inner幅(1080px)で崩れが発生している
テキストが画像に圧迫されて窮屈なレイアウトになってしまっています
(添付スクリーンショット1)

768pxで縦並びにするのは◎です！
769〜inner幅(1080px)でも不自然にならないように調整してみましょう。画像を縮小していくとバランスが良くなりそうですね

→テキストを圧迫している画像に「width:43%;」を指定

.heading-img {
    max-width: 560px;
    width: 43%;
    height: auto;
}

これらのコンテナとしての親要素である「.heading-inner」の左右にpaddingで余白を持たせる。

.headmain-inner {
    max-width: 1080px;
    margin-right: auto;
    margin-left: auto;
    display: flex;
    align-items: center;
    justify-content: space-around;
    margin-top: 80px;
    margin-right: auto;
    margin-left: auto;
    padding: 0 10%;
}


・768px以下での改行、文字幅(line-height)
少し細かいですが、カンプ通りの改行、文字幅になっているか確認しましょう！

→aboutのテキストをカンプ通りの改行・文字幅にするため、letter-spacingで調整。

 .about-p {
        color: #333333;
        line-height: 1.7;
        /* width: 450px; */
        margin-top: 30px;
        margin-bottom: 30px;
        letter-spacing: -0.2em;
    }


SERVICE
・769〜900くらいで少しズレが出ていますね(添付スクリーンショット2)
paddingの見直しをしてみてください

→SERVICEの3つのコンテンツをpaddingで調整していたのを削除し、
コンテナとしてのinnerの「 justify-content: spece-between;」を「center」に

.s-inner {
    max-width: 800px;
    display: flex;
    justify-content: center;
    margin-right: auto;
    margin-left: auto;
    margin-top: 109px;
    align-items: center;
}

中央に寄ったコンテンツの真ん中の要素「営業代行」にmarginを使って適度に離し余白を作る。

.s-innerbox2 {
    margin-right: 10%;
    margin-left: 10%;
}


ABOUT
・2つのarticleの両端がそろっていない
・メインビジュアル同様、769〜inner幅(1080px)でレイアウト崩れが発生している(添付スクリーンショット3)

→2つのarticl各々の左右marginの調整、また固定していたテキスト部分のwidthを削除、line-heightを-0.1emに。　→チマチマと調整しました。

.about-copy1 {
    margin-left: 70px;
}

.about-copy2 {
    margin-right:70px;
}

.about-p {
    line-height: 1.7;
    /* width: 450px; */
    margin-top: 30px;
    margin-bottom: 30px;
    letter-spacing: -0.1em;
}


フッター
・768px以下
左右、下に余白が空いてしまっている

まず、768px以下で出現していたフッター左右の余白がbodyに指定していたpaddingであることが判明→削除


次に、フッター下の余白を消す。
まず、htmlとbodyのheightを100%にしてみる。
（参考）
https://guuten.net/footer-margin/

html {
    height: 100%;
}

body {
    height: 100%;
    font-family: YuGothic,'Yu Gothic',sans-serif;
}

→変化なし…。

次に、positionを使って「bottom:0;」で余白を消してみる。
（参考）
https://pointsandlines.jp/front-end/html-css/footer-fix

body {
    height: 100%;
    font-family: YuGothic,'Yu Gothic',sans-serif;
    position: relative;
}

footer {
    width: 100%;
    height: 135px;
    background: #E8E8E8;
    position: absolute;
    bottom: 0;
}

→逆に画面幅が狭まると上に上がってしまう。　？？？

→一旦positionのプロパティを削除し、他の箇所を先に修正
　
　→余白消えてる…(ToT)
　　
フッター下の謎の余白の原因については、あれこれ検証を重ねましたが「これ！」という明確な原因は特定できませんでした。
他の余白やサイズ調整の過程で消滅していたので、全体的に影響を及ぼしていた何らかのプロパティに連動して発生していた可能性があるのでは、と考えています。
今後は一箇所の修正でも全体にどう影響するか、注意深く観察しながら検証していきます。



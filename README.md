# illustrator-to-MapTiles
- これはadobe Illustratorから、ZXY方式の地図タイルを出力する、Illustrator拡張スクリプトです
- 予め地図タイルにあわせた形でデータを作成している必要があります
- ***制作時の左上のXYタイル座標***と、***制作時にあわせた地図タイルのズームレベル***があればOK
    - 必要なのはz,x,y,z'の4つ
    - z,x,yは制作しているIllustratorの設計データ
    - z'は出力したいズームレベル
- 出力先のズームレベルを指定すれば、指定のフォルダ内に配置してくれます
- もちろん、***スクリプト実行前のバックアップをお忘れなく***
    - 開発者の私は、データの破壊による責任を負いません
- Illustrator CC 2018での動作は確認していますが、他のバージョンでは不具合があるかもしれません
- 動作が重いので気をつけて
    - より良い動作の為の改良は大歓迎！
- 出力タイルサイズを256px以外にもできます
    - 拡張スクリプト内の既定値をいじってください

---------------------------------------------

# バージョン履歴
[CHANGELOG.md](./CHANGELOG)に移動

---------------------------------------------

# 前提条件
- zxy方式の地図タイルに基づくIllustratorデータを作成している
- 制作データは、地図タイルに合わせられている
- 出力範囲全体がちょうど収まるアートボードがある
- ベースにある地図タイルのズームレベルを把握している
    - 256pxのz15地図タイルを512pxにして配置していた場合、z16とみなす
- 出力範囲左上のタイル座標(x,y)を把握している
    - 例えば国土地理院にはタイル座標確認サイトが。
    - [https://maps.gsi.go.jp/development/tileCoordCheck.html](https://maps.gsi.go.jp/development/tileCoordCheck.html)
    - どこかにメモをとっておくことを推奨

---------------------------------------------

# 導入方法・使い方
1. スクリプトを実行したいIllustratorデータを開く
1. 本githubの"ai2tiles.jsx"をRAWから名前を付けて保存する
1. PC内のどこかに"ai2tiles.jsx"を配置する
    - 例えば、adobe既定のスクリプト保管フォルダ
1. ***スクリプト実行前のIllustratorデータを保存します***
1. スクリプト実行前に、出力範囲全体がちょうど収まるアートボードを選択する
    - このスクリプトでは、選択されたアートボードに基づいて出力します
1. ファイル->スクリプトからPC内にあるai2tiles.jsxを指定、実行する
1. 入力画面で必要事項を入力する
    - スクリプトを実行したいデータのz,x,yを入力する
    - 実行後に出力したいズームレベルを4つ目に入力する
1. OKを押し、ファイル選択ダイアログで出力先を指定する
1. 気長に待ってください、とても遅いので
1. しばらく待てば、出力完了！

---------------------------------------------

# Q & A
## 入力画面での既定値を変更したい

拡張スクリプトの中身を直接弄ってください。テキストエディタで開くことができます。

拡張スクリプトの序盤に、既定値を設定できる箇所があります。この数値を変えることで、既定値を変更できます。

## 256px以外で出力したい

拡張スクリプト内の以下を変更してね。

```javascript
// ユーザーによるカスタマイズ可能変数
// (1)imgsize : 画像サイズの値(px)
    // ここで決めたサイズの正方形として地図タイルは出力される
    // 内部的には、一旦256でアートボードを用意した後、256とimgsizeの比率で出力画像の倍率を調整する。
var imgsize = 512;
```

## 制作時よりも低いズームレベルで出力したい

現在は想定外の挙動をするので注意。そのうち改良予定。

## 実行するのに時間がかかる

開発環境で動作確認を行うと、毎秒4枚程度出力されます。PC性能などにより異なりますが、遅いことは間違いないです。

内部的には、一時アートボードを1つ1つ移動して出力しているだけなので、出力枚数に比例して処理時間も伸びます。

加えて、処理を中断できないのもこの拡張スクリプトの難点です。ズームレベルが大きくなると、出力枚数も増えるので、この機能は欲しい所。いずれつけるかも。

---------------------------------------------

# スクリプト内容や開発設計など
[doc/設計.md](./doc/設計.md)を参照
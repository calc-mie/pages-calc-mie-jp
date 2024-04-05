---
title: "UnityとProcessingを比較する"
author: "Rinadehi_Mie"
---

<style>
img {
  margin: 0 auto;
  border: 2px solid #ccc;
  width: 100%;
}
hr {
  margin: 50px auto;
  width: 80%;
}
@media (min-width: 600px) {
  img {
    margin: 0 auto;
    display: block;
    width: 50%;
  }
}
</style>

Unityとは、様々なプラットフォームのソフトウェアを開発できる統合開発環境です。C#などの言語で書くことができます。

3D/2D描画やサウンド再生、UI部分などのツールが提供されるので、ゲームだけでなく様々なソフトウェアの開発ができます。

個人的には、3Dグラフィックエンジン（OpenGL,Dircet3Dなど）についての知識無しで3DCGを用いたソフトウェアを、しかもマルチプラットフォームで動作するものを開発できることが大きなメリットだと思います。

ということで最近Unityについて勉強し始めたのですが、Unityはプログラマーだけではなくアーティスト、デザイナーといった人でも学習がしやすいように開発環境が作られているように感じました。

私はこれまでにProcessingを書いたことがあります。Processingも3DCGを容易に扱え、マルチプラットフォームで動作し、アーティスト向けの言語ですが、Unityはさらにアーティスト向けだと感じました。


そこで、Unityでの開発をProcessingと比較しながら説明していき、Unityとはどうものか、そして同時にProcessingとはどういうものかを紹介していこうと思います。

# 1.新規プロジェクトの作成
## 1-1. Unityの新規プロジェクトの作成
まずはUnityについてです。
Unityのインストール後、初期セットアップを済ませるとメニュー画面が表示されます。ここでNEWをクリックすると次のような画面になります。

![](/images/Unity01.png)

ここでプロジェクト名、プロジェクトファイルの場所、そして3D/2Dのどちらのソフトウェアを開発するかを指定します。
3Dを選択して、プロジェクトファイルの場所や名前を設定しCreate Projectをクリックすると次のような画面になります。

![](/images/Unity02.png)

ここでポイントなのが、**プログラムのソースコードを入力する場所はまだ無い**、ということです。

##  1-2. Processingの新規プロジェクトの作成
次はProcessingについてです。
Processingのインストール後、起動すると、次のような画面になります。

![](/images/Processing01.png)

Unityとは違って、**ソースコードを入力する画面が表示されました。**
Processingでは`void setup()`内に初期処理、`void draw()`内に毎フレーム行う処理を書きます。
それでは以下のようなコードを入力します。

```
void setup() {
  size(640, 480, P3D);
}
```

これでウインドウのサイズが640x480、そして描画モードがP3D(Processing3D)になります。

# 2. 3Dオブジェクトの配置

今回は立方体の3DCGモデルが回転するものを作ろうと思います。
まず立方体を配置します。

## 2-1. Unityで3Dオブジェクトの配置
Hierarchyタブ内の[Create]->[3D Object]->[Cube]をクリックすると立方体を配置できます。

![](/images/Unity03.png)

立方体をクリックして選択すると画面右側にInspectorというタブがあり、ここで立方体の位置、角度、大きさなどを設定できます。

* Position X:0 Y:0 Z:0
* Rotation X:0 Y:0 Z:0
* Scale X:1 Y:1 Z:1

と設定しておきます。

![](/images/Unity04.png)

つぎに、同様にカメラを設定します。
HierarchyにMain CameraがあるのでそれをクリックするとInspectorタブがカメラの設定画面になります。

* Position X:0 Y:1 Z:-2
* Rotation X:25 Y:0 Z:0
* Scale X:1 Y:1 Z:1

と設定しておきます。

このままだと立方体が白い豆腐のような状態なので、色を付けます。
メニューバーの[Assets]->[Create]->[Material]を選択すると、

![](/images/Unity05.png)

下のProjectタブのAssetsの欄にNew Materialというのができます。

![](/images/Unity06.png)

これをクリックするとInspectorタブがマテリアルの設定画面になるので、
Albedoの白色のついた四角い部分をクリックします。

![](/images/Unity07.png)

カラーパネルウインドウが表示されるので、たとえば黄色などに調節します。

![](/images/Unity08.png)

これで3Dオブジェクトの色情報（マテリアル）ができたのでこれを立方体に適用します。
適用させるには、画面下のProjectタブのNew MaterialをSceneタブの立方体にドラッグします。
![](/images/Unity09.jpg)

以上で黄色い立方体を描画できるようになりました。
画面上部の実行ボタン（▶）を押すと実行できます。

**ポイントなのはここまで一つもソースコードを書いていないことです。**

![](/images/Unity10.png)

## 2-2. Processingで3Dオブジェクトの配置
Unityではソースコードを書くことがありませんでしたが、同じことをProcessingで行うにはソースコードを書きます。

以下のようなコードを入力します。

```
void setup() {
  size(640, 480, P3D);
}

void draw() {
  background(200);
  fill(255,255,0);
  noStroke();
  lights();
  translate(width/2, height/2, 0);
  rotateX(-0.5);
  box(200);
}
```

プログラムは上から順に処理されます。最初の`background(200);`で全体を明度200の色で塗り、最後の`box(200);`で一辺の長さが200の立方体を描画する。という内容です。

どんな立方体を描画するかは`box(200);`より前の行で決めています。

* `fill(255,255,0);`で色をR:255 G:255 B:0、つまり黄色に指定します。
* `noStroke();`でワイヤーフレームの線を表示しないように指定します。
* `lights();`で正面からライトに照らされたように陰影がつくようになります。
* `translate(width/2, height/2, 0);`でウインドウの中央に描画するよう指定します。
* `rotateX(-0.5);`で立方体を水平方向を軸に回転させます。

![](/images/Processing02.png)

# 3. キーボード入力の受け付け

それでは、キーボードの左右矢印キーを入力すると立方体が回転するようにしていきます。

## 3-1. Unityでキーボード入力の受け付け

ここまで一度もプログラムを書きませんでしたが、ここでやっとプログラムを書くことになります。

メニューバーの[Assets]->[Create]->[C# Scripts]を選択すると

![](/images/Unity11.png)

下のProjectタブのAssetsの欄にNewBehaviourScripts.csというのができます。

![](/images/Unity12.png)

これをダブルクリックするとエディターが立ち上がります。環境によって立ち上がるアプリケーションは違うとは思いますが操作は同じです。ちなみにWindowsだとVisual Studio、macOSだとMono Developが初期設定になっていると思います。

![](/images/Unity13.png)

最初からプログラムのひな形が書かれていると思います。

`void Start () {}`内にスクリプト呼び出し時に実行する処理、`void Update () {}`内に毎フレーム実行する処理を書きます。
物体をキーボードの左右矢印キーが入力されたときに回転するようにしたいので、`void Update () {}`内に以下のように追加します。

```
	void Update () {
        if (Input.GetKey(KeyCode.RightArrow))
            transform.Rotate(new Vector3(0.0f, -1.0f, 0.0f));
        if (Input.GetKey(KeyCode.LeftArrow))
            transform.Rotate(new Vector3(0.0f, 1.0f, 0.0f));
    }
```

1. 「もしキーボード入力のが右矢印だった場合、」: `if (Input.GetKey(KeyCode.RightArrow))` 
1. 「物体を垂直方向を軸に回転させる。」: `transform.Rotate(new Vector3(0.0f, -1.0f, 0.0f));`
1. 「もしキーボード入力のが左矢印だった場合、」: `if (Input.GetKey(KeyCode.LeftArrow))` 
1. 「物体を垂直方向を軸に回転させる。」: `transform.Rotate(new Vector3(0.0f, 1.0f, 0.0f));`

ソースコードを保存して、Unityの画面に戻ります。

このままではまだこのソースコードは実行されません。というのも、Unityではオブジェクトにプログラムをくっつけて、オブジェクトからプログラムを呼び出すという形をとっています。今回、立方体を回転させるため、立方体からこのソースコードを呼び出すよう設定します。

設定方法はマテリアルの時と同様に画面下のProjectタブのNewBehaviourScriptsをSceneタブの立方体にドラッグします。
これで立方体が今書いたソースコードの動作を行うようになりました。

![](/images/Unity14.jpg)

![](/images/Unity15.png)

## 3-2. Processingでキーボード入力の受け付け
以下のようにプログラムに追加します。

```
int r=0; //追加
void setup() {
  size(640, 480, P3D);
}

void draw() {
  if (keyPressed == true) { //追加
    if (keyCode == RIGHT) r++; //追加
    if(keyCode == LEFT) r--; //追加
  } //追加
  background(200);
  fill(255,255,0);
  noStroke();
  lights();
  translate(width/2, height/2, 0);
  rotateX(-0.5);
  rotateY(radians(r)); //追加
  box(200);
}
```

一番最初の`int r=0;`で立方体の回転角度を保管する変数`r`を定義します。

`void draw()`内において、

1. 「もしキーボード入力があった場合、」: `if (keyPressed == true) {`
1. 「もし入力が右矢印だった場合、 `r`の値を１多くする」: `if (keyCode == RIGHT) r++;` 
1. 「もし入力が左矢印だった場合、 `r`の値を１小さくする」: `if(keyCode == LEFT) r--;`

という処理を行うことでキーボード入力に応じて変数`r`の値を変えることができます。

そして`rotateY(radians(r));`で変数`r`分だけ立方体を垂直方向を軸に回転させることができます。

![](/images/Processing03.png)




# まとめ

以上で、Unity、Processingで3DCGの描画、そしてキーボード入力によって動かすことができました。
UnityとProcessingはどちらもアーティスト向けのプログラミングですが、

Processingはほとんどをプログラムのコードだけで構成していく。

Unityはマウスを用いて構成していき、動きの部分だけをプログラムで書く。

という違いがあります。

Processingはソースコードを実行するまでは結果がわかりません。これはJavaやC言語でプログラミングしていくのと同じです。それに対しUnityはやはりゲームエンジンというだけあって、3DCGのモデルを読み込んで、それを動かす、という流れがGUIで視覚的にわかりやすくなっています。

大規模になりやすい3DCGプログラムではUnityのほうが制作しやすいと思います。実際にスマートフォンアプリでは、メビウスファイナルファンタジーや、デレステはUntiyで開発されています。

それではProcessingのメリットは何かといいますと、個人的にはソースコードだけで3DCGを描画するという特徴を生かし、創発的な絵を描きやすいことだと思います。
ジェネラティブ・アートなんて言ったりもします。

Processingにそのサンプルが収録されています。
Processingの画面の左上のバーから[ファイル]->[サンプル]とクリックし、Javaサンプルという画面の中から[Demos]->[Graphics]->[RotatingArcs]とクリックしてください。そして実行すると画像のような映像が流れると思います。

![](/images/Processing04.png)

# 参考サイト

* [Unityマニュアル](https://docs.unity3d.com/ja/540/Manual/ExecutionOrder.html)
* [Processingリファレンス](https://processing.org/reference/)

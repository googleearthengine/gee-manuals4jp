# [Developer’s Guide - Get Started with Earth Engine](https://developers.google.com/earth-engine/getstarted)
Last updated on 2018/11/16 by Kouki Takesue

# Earth Engineをはじめてみよう！
このスタートガイドはEarth Engine JavaScript API のプログラミングを手っ取り早くはじめるためのものです。JavaScriptの紹介や更なるEarth Engine APIの経験を深めたい場合はチュートリアルを、JavaScriptのコーディングスタイルについてはGoogle JavaScriptスタイルガイドをご覧ください。
ユーザーはGoogleのインフラ上に保存されている座標が与えられた画像やベクトル・データに対してGoogle Earth Engineのアルゴリズムを実行することができます。Google Earth Engine APIは画像を表示や分析するための関数のライブラリを提供しています。Earth Engineのパブリックデータカタログには膨大な量の利用可能な画像があります。ベクターデータセットはGoogle Fusion Tablesを通して利用可能です。開発者は既存あるいは自作のベクターデータセットにアクセスすることができます。

図1. Earth Engine Code Editor  code.earthengine.google.com

Code EditorはEarth Engineアプリケーションを開発するための対話型環境です（図1）。中央のパネルがコードエディエタとなっていて、上には現在のスクリプトを保存するボタン（Save）と動作させるボタン（Run）、そしてマップをクリアするボタン（Reset）があります。Get LinkボタンはアドレスバーにスクリプトのユニークなURLを生成します。下のマップはスクリプトによって追加されたレイヤーを表示します。上部にはデータセットや地名を検索するための検索ボックスがあります。左パネルにはコードサンプル、保存したスクリプトおよび検索可能なAPIリファレンスがありまし。右パネルにはマップに対する照会結果を表示するインスペクターや出力コンソール、そして長時間の処理を管理するタスクマネージャーがあります。Helpボタンはユーザーガイド、ヘルプフォーラム、そしてCode Editor の機能に対する便利なキーボードショートカットリストへのリンクがあります。更に知りたい場合はCode Editor sectionをご覧ください。

# Code Editor 開始とコードの実行
このステップではCode Editor の開き方とカスタムスクリプトによって画像を表示する方法を説明します。最適な結果を得るために、GoogleのWebブラウザであるChoromeの最新版をインストールしてください。こちらから利用可能です。

1. code.earthengine.google.comにアクセスしてEarth Engine Code Editorを開きます。登録済みのGoogleアカウントでログインしていない場合には利用可能なアカウントでログインしてください。
2. Code Editorの左端のScriptsに移動します。そこにはEarth Engineデータにアクセス、表示あるいは分析するためのサンプルスクリプトがあります。
3. “Image Collection”内にある“Filtered Composite”のサンプルを選択します。すると、中央のコンソールにスクリプトが表示されます。Runボタンをクリックするとスクリプトが実行されます。検索条件が与えられた合成画像のサンプルコードがコロラド州とユタ州にまたがる範囲のLandsat 7の画像を選択します。そして、トゥルーカラーで合成された画像を表示します。このサンプルはfilter()、 clip()、そして Map.addLayer()といった頻繁に使用するメソッドを紹介しています。

# Earth Engineデータの構造
Earth Engine の二つの最も基本的な地理データの構造はImageとFeatureであり、それぞれ、ラスター型とベクター型に対応します。Imagesは複数のバンドとプロパティのディクショナリで構成されます。Featureは Geometryとプロパティのディクショナリで構成されています。イメージのスタック（時系列画像など）はImageCollectionによって扱われます。Featureの集合はFeatureCollectionによって扱われます。ほかの基本的なEarth Engineのデータ構造は Dictionary、 List、 Array、 Geometry、 Date、 Number、 Stringを含みます。これらが全てサーバー・サイド・オブジェクトであることを忘れないようにしてください。つまり、あなたが明示的にオブジェクトに関する情報をリクエストしない限り、クライアント・ブラウザはスクリプト内のオブジェクトについて何も知り得ません。そのリクエストはGoogleからCode Editorへと渡されたメッセージがトリガーとなります。メッセージが大きい場合には通信は遅くなります。

# Earth Engineのアルゴリズム
APIで操作を実行する様々な方法があります。

* オブジェクトに付属しているメソッドの呼び出し
* アルゴリズムの呼び出し
* Code Editorの特定の関数の呼び出し
* 新しい関数の定義

Code EditorのDocsタグにはそれぞれのメソッドのAPIクラスが列挙されています。例えばImageクラスはaddメソッドを持っています。
var image3 = image1.add(image2);
このメソッドはimage2のバンドをimage1のバンドに加えます。ee.Algorithmsのカテゴリーには現在サポートされている特化した処理あるはドメイン固有の処理に関するアルゴリズムのリストが含まれています。例えば、Digital Elevation Model (DEM)の入力から地形学的なレイヤーを作るには次のようになります。

var terrainImage = ee.Algorithms.Terrain(dem);
Code Editorの特定の関数は MapとExport メソッドなどを含みます。これらは、それぞれ、レイヤがどのようにMapパネルやGoogleドライブに追加するかを操作します。次に示すように、関数はJavaScript の中で作ることもできます。

var myFunction = function(args) {
  // do something
  return something;
};

Mapping sectionで説明されているように、ユーザー定義関数はカスタム関数やコレクションの要素を修正する場合に有効です。
var collection2 = collection1.map(aFunction);
次のセクションでは、さまざまな使用するケースを説明します。

Notation used in the guides:
Static methods called on an Earth Engine class (for example ee.Image) are written as Image.staticMethod(). Methods called on an instance of a class are written as image.instanceMethod(). The lowercase image means that a variable named image refers to an instance of the ee.Image class.

このガイドにおける注記について
Earth Engineのクラスで呼び出される静的なメソッド (ee.Imageなど) はImage.staticMethod() のように書かれます。クラスのインスタンスで呼び出されるメソッドはimage.instanceMethod()のように書かれます。小文字で始まるimageはee.Imageクラスを参照参照するimageというインスタンスの変数名を表します。

# ‘Hello world!’ JavaScript
コンソールに情報を表示するのはオブジェクトや計算の数値結果の表示、オブジェクトのメタデータの表示やデバックの手助けについて基本的なタスクです。その象徴であるCode Editorの’Hello World!’サンプルは次のように書かれます。

`print(‘Hello world!’);`

この行をCode editorにコピーして、Runをクリックします。するとアウトプットはCode Editorの右側にあるConsoleタブに表示されます。よりリモートセンシングに関連する例では、以下の行はLandsat 8イメージのメタデータを表示します。

`print(ee.Image('LANDSAT/LC08/C01/T1/LC08_044034_20140318'));`

コンソールの出力を注意深く調べて、Landsatイメージで使用できるメタデータを確認します。


# マップにデータを追加する
コンソールに情報を表示することに加えて、地図にデータを追加することは、地理的データを視覚化する方法です。この場合、Map.addLayer()を使用します。このサンプルでは、ee.Image()を使用してImageをインスタンス化し（これらのイメージの検索方法は後で説明します）、Map.addLayer()でマップに追加され、マップはイメージの中央に配置されます。

`
// Load an image.
var image = ee.Image('LANDSAT/LC08/C01/T1/LC08_044034_20140318');

// Center the map on the image.
Map.centerObject(image, 9);

// Display the image.
Map.addLayer(image);
`

The second parameter of Map.centerObject() is a zoom level, where higher numbers indicate larger scale (more zoomed in). The parameters for the Map functions are described in depth in the API reference accessible from the Docs tab. If the appearance of the image is unsatisfactory, configure the display parameters with an additional argument to Map.addLayer(). For example:

`
// Load the image from the archive.
var image = ee.Image('LANDSAT/LC08/C01/T1/LC08_044034_20140318');

// Define visualization parameters in an object literal.
var vizParams = {bands: ['B5', 'B4', 'B3'], min: 5000, max: 15000, gamma: 1.3};

// Center the map on the image and display.
Map.centerObject(image, 9);
Map.addLayer(image, vizParams, 'Landsat 8 false color');
`

Map.centerObject()の2番目のパラメータはズームレベルです。数値が大きいほどスケールが大きくなります（ズームイン）。Map関数のパラメータについては、DocsタブからアクセスできるAPIリファレンスに詳しく説明されています。画像の外観が不満足な場合は、Map.addLayer()の引数を追加して表示パラメータを設定します。以下は例です。

`
// Load the image from the archive.
var image = ee.Image('LANDSAT/LC08/C01/T1/LC08_044034_20140318');

// Define visualization parameters in an object literal.
var vizParams = {bands: ['B5', 'B4', 'B3'], min: 5000, max: 15000, gamma: 1.3};

// Center the map on the image and display.
Map.centerObject(image, 9);
Map.addLayer(image, vizParams, 'Landsat 8 false color');
Observe that the visualization parameters are defined by an object literal, which includes a list of bands to display, a minimum and maximum digital number and a gamma value. (Learn more about Landsat bands here. Learn more about image visualization here).
Use Map.addLayer() to add features and feature collections to the map. For example,
var counties = ee.FeatureCollection('ft:1S4EB6319wWW2sWQDPhDvmSBIVrD3iEmCLYB7nMM');
Map.addLayer(counties, {}, 'counties');
Note that the encrypted key of this table is everything after the ft: and before the quote.
`

視覚化パラメータは、表示するバンドのリスト、最小および最大デジタル数、およびガンマ値を含むオブジェクトリテラルによって定義されることに注意してください。 （Landsat bandsの詳細はこちら、イメージビジュアライゼーションの詳細はこちらをご覧ください）。
Map.addLayer()を使用してfeaturesとfeature collectionsをマップに追加します。以下が例です。

`
var counties = ee.FeatureCollection('ft:1S4EB6319wWW2sWQDPhDvmSBIVrD3iEmCLYB7nMM');
Map.addLayer(counties, {}, 'counties');
`

この表の暗号化されたキーは、ft:の後ろと引用符の前のすべてです。




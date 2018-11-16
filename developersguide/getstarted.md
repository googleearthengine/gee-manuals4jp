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


# images、image collections、feature collectionsを探す
Earth Engineのデータカタログを検索することで、画像や画像コレクションを検出できます。たとえば、「Landsat 8」を検索フィールドに入力すると、ラスタデータセットのリストが表示されます。 （Earth Engineのデータセットの完全なリストはthe Earth Engine Data Catalogにあります）。データセット名をクリックすると、簡単な説明、一時的なアベイラビリティ、データプロバイダ、ImageCollection IDに関する情報が表示されます。Importボタンをクリックすると、スクリプトの先頭にImportsセクションが自動的に作成され、このコレクションの変数が設定されます。

または、ImageCollection IDをコピーしてコードに貼り付けます。たとえば、 'Landsat 8'検索の最初の結果を選択し、次のようにIDをコピーします。

`var collection = ee.ImageCollection('LANDSAT/LC08/C01/T1');`

これは地球の表面にまたがる多くのイメージの集合であるため、コレクション内の個々のイメージを見つけるには検索を絞り込むためにフィルタリングが必要です。あるいは、イメージの集合は、合成およびモザイク技術を用いて単一の画像に縮小することができます。次のセクションでは、フィルタリングと合成について詳しく説明します（抑制を参照してください）。

Feature collectionsは、画像のように、キュレーションされたFusion Tablesカタログがないため、簡単に見つけることはできません。ただし、Code Editorで検索すると、 'Table'（ベクター）データセットも表示されます。これらは、一般に、さまざまな品質と完全性を持つユーザーがアップロードしたコンテンツです。いくつかの有用なデータセットがここにリストされています。 Fusion Tableを作成するには、CSVまたはKMLのテキストを地理座標でアップロードします。ベクターデータセットのインポートについてはこちらをご覧ください。


# フィルタリングとソート
結果の数を制限するために、コレクションを空間および/または時間でフィルタリングする必要があることがよくあります。たとえば、サンフランシスコのクラウドフリーシーンを見つけるために、Landsat 8シーンコレクションをソートするタスクを考えてみましょう。まず、関心領域を定義する必要があります。ポイントはしばしばそれに役立ちます。Code Editorの右側にあるInspectorタブをアクティブにして、関心領域の中心付近をクリックし、Inspectorタブから座標をコピーしてから、次のようにしてPointを作成します。

`var point = ee.Geometry.Point(-122.262, 37.8719);`

開始日と終了日を設定します。

`
var start = ee.Date('2014-06-01');
var finish = ee.Date('2014-10-01');
`

ポイントと日付を使用してLandsat 8コレクションをフィルタリングし、次にLandsat 8シーンメタデータの検査中に検出されたメタデータプロパティを使用してソートします。

`
var filteredCollection = ee.ImageCollection('LANDSAT/LC08/C01/T1')
  .filterBounds(point)
  .filterDate(start, finish)
  .sort('CLOUD_COVER', true);
`

このコレクションは安全に表示して検査することができます。（コレクションに画像が多すぎる場合は、表示が非常に遅くなるか、タイムアウトになるか、エラーが返されます。）コレクション内のイメージはImageCollectionの 'features'プロパティに格納されたListであることに注意してください。上記のように、コレクション内の任意のイメージのIDをImage constructorにコピーすることができます。あるいは、最初の画像を取得します（最低雲量）。

var first = filteredCollection.first();

ee.Filterを引数としてfilter()を使用して、完全なEarth Engineフィルタリング機能にアクセスします。 （上で使用されたfilterBounds()およびfilterDate()メソッドはショートカットです）。たとえば、次のようにフィルタを作成し、それを使用してFeatureCollectionをフィルタリングし、結果を表示します。

// Load a feature collection from a Fusion Table.
var featureCollection = ee.FeatureCollection('ft:1fRY18cjsHzDgGiJiS2nnpUU3v9JPDc2HNaR7Xk8');

// Filter the collection.
var filteredFC = featureCollection.filter(ee.Filter.eq('Name', 'California'));

// Display the collection.
Map.addLayer(filteredFC, {}, 'California');

以下のリンクには、この時点までに使用されたコードが含まれています。Code Editorの上部にあるGet Linkボタンをクリックし、ブラウザのアドレスバーからURLをコピーして、これらのリンクを取得します。
https://code.earthengine.google.com/74508b22766c10e74e87a7ebaccec9e7


# バンド間演算 Band Math
Imageメソッドを使用してイメージに対して数学演算を実行する。これは、バンド再結合（スペクトルインデックス）、画像差分、または定数による乗算などの数学的演算を含むことができます。たとえば、標準化差植生指数（NDVI）画像の差を20年ごとに計算します。

// This function gets NDVI from Landsat 5 imagery.
var getNDVI = function(image) {
  return image.normalizedDifference(['B4', 'B3']);
};

// Load two Landsat 5 images, 20 years apart.
var image1 = ee.Image('LANDSAT/LT05/C01/T1_TOA/LT05_044034_19900604');
var image2 = ee.Image('LANDSAT/LT05/C01/T1_TOA/LT05_044034_20100611');

// Compute NDVI from the scenes.
var ndvi1 = getNDVI(image1);
var ndvi2 = getNDVI(image2);

// Compute the difference in NDVI.
var ndviDifference = ndvi2.subtract(ndvi1);

この例では、ユーザー定義であるfunctionの使用に注目してください。次のセクションの関数の詳細。


# マッピング（for-loopを使わない方法）
コレクション内のアイテムを繰り返し処理するには、map()を使用します。 （for-loopは、Earth Engineで行うループではありませんので避けてください）。 map()関数は、ImageCollection、FeatureCollection、またはListに適用され、その引数として関数を受け入れることができます。関数の引数は、それがマップされているコレクションの要素です。これは、追加など、同じ方法でコレクションのすべての要素を変更する場合に便利です。たとえば、次のコードは、NDVIバンドをImageCollectionのすべてのイメージに追加します。

// This function gets NDVI from Landsat 8 imagery.
var addNDVI = function(image) {
  return image.addBands(image.normalizedDifference(['B5', 'B4']));
};

// Load the Landsat 8 raw data, filter by location and date.
var collection = ee.ImageCollection('LANDSAT/LC08/C01/T1')
  .filterBounds(ee.Geometry.Point(-122.262, 37.8719))
  .filterDate('2014-06-01', '2014-10-01');

// Map the function over the collection.
var ndviCollection = collection.map(addNDVI);

別の一般的なタスクは、FeatureCollectionのフィーチャに新しいプロパティ（’attribute’'または 'field'）を追加することです。次の例では、新しいプロパティは2つの既存の属性を含む計算です。

// This function creates a new property that is the sum of two existing properties.
var addField = function(feature) {
  var sum = ee.Number(feature.get('property1')).add(feature.get('property2'));
  return feature.set({'sum': sum});
};

// Create a FeatureCollection from a list of Features.
var features = ee.FeatureCollection([
  ee.Feature(ee.Geometry.Point(-122.4536, 37.7403),
    {property1: 100, property2: 100}),
    ee.Feature(ee.Geometry.Point(-118.2294, 34.039),
    {property1: 200, property2: 300}),
]);

// Map the function over the collection.
var featureCollection = features.map(addField);

// Print a selected property of one Feature.
print(featureCollection.first().get('sum'));

// Print the entire FeatureCollection.
print(featureCollection);



# 






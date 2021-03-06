## QGISで扱えるデータ形式について

QGISでは様々なデータを扱うことができます。

次の表ではそれぞれの特徴を簡単に示しています。

|  | ESRI Shapefile | GeoPackage | SpatialLite | GeoJSON | FlatGeobuf |
| -------- | -------- | -------- | ----------- | ------- | --------- |
| 空間インデックス | ○ | ○ | ○ | × | ○ |
| マルチレイヤ | × | ○ | ○ | ○ | × |
| 単一ファイル | × | ○ | ○ | ○ | ○ |
| web対応 | × | △ | △ | ○ | ◎ |
| ラスタ対応 | × | ○ | × | × | × |

### ESRI Shapefile

ESRI Shapefile(以下Shapefile)は古くからベクター向け地図データとして使われてきたファイル形式です。

ファイルの拡張子は`.shp`ですが、これ以外にもデータを格納する`.dbf`や、投影法などを管理するための`.prj`ファイルなどに分割されているため、一ファイルだけでは役に立たないという特徴があります。

また、過去の遺産として使えるケースがありますが、日本語の扱いに問題があるケースが多いため、現在では保存形式としては推奨されていません。

代わりにGeoPackageやFlatGeobufなどの最新のファイルを使うことを推奨します。

### GeoPackage

GeoPackageはベクター及びラスタ向けの地図データ形式で、QGIS 3系から標準の保存形式として使われています。

ファイルの拡張子は`.dpkg`で、中身はSQLite3というデータベースの形式となります。

GeoPackageは複数のレイヤーを一つのファイルに保存することができ、またラスタデータのレイヤーに対してはタイル形式の出力をするようになっていて、大きなラスタデータでも軽量に動かすことが可能となっています。

また、大きな特徴としてQGISのスタイル設定も保存できたり、SpatialLiteの空間分析関数が使えたりと大変便利な機能があります。

### SpatialLite

SpatialLiteはSQLite3の拡張機能を用いた実装で、ベクター向けの地図データ形式として使われているファイル形式です。

ファイルの拡張子は`.db`や`.sqlite`、`.sqlite3`などが使われています。

SpatialLiteはQGISの古いバージョンからサポートされているため、Shapefileで扱うのが困難なデータを扱うケースがありました。

ただし、SpatialLiteの特徴である空間クエリがGeoPackageでもサポートされているため、現在では比較的考慮しなくても良くなりました。

### GeoJSON

GeoJSONはJSON(JavaScript Object Notation)形式を地図に応用したファイル形式で、ベクター向けの地図データ形式として使われてるファイル形式です。

ファイルの拡張子は`.geojson`です。

特徴としてはJavaScriptというプログラミング言語で簡単に扱えるため、webサイトでの地図表示が簡単にできるため、インターネット上で地図を閲覧するサイトで多く使われています。

また、テキストフォーマットなのでテキストエディタで作成や編集もできるという利点があります。

ただし、空間インデックスを持っていないため、ファイルの全てを読む必要があり、速度としては低速でかつ、ファイルサイズも大きくなります。

### FlatGeobuf

FlatGeobufは比較的新しいファイル形式で、単一レイヤーのベクター向けのファイル形式です。

ファイルの拡張子は`.fgb`です。

特徴としては[FlatBuffers](https://google.github.io/flatbuffers/)によるバイナリでエンコードされたファイルで、非常に高速で動作する上、ストリーミングをサポートしているためwebサイトの地図データとして最適化されています。

QGISでは3.16からサポートをしています。また編集の対応などはQGIS 3.18以降のサポートとなっているため、比較的最新のQGISを要求する所に注意が必要です。

単純にShapefileをそのまま扱い安くするためにFlatGeobufを、複数のShapefileを一つにまとめたい場合はGeoPackageを、という風に使い分けると良いでしょう。

### その他のファイル形式

QGISでは上記以外にも様々なファイルをサポートしています。

全ては記載できないため、一部のファイルを記載します。

#### GeoTiff

写真などに地理上の座標を付与したラスタファイル形式です。

ファイルの拡張子は`.geotiff`です。

GeoTiffはTiffという画像ファイル形式を地図上で扱えるように拡張されたもので、航空写真や紙地図などをGIS上で扱うために使われています。

写真そのものは画像として扱う場合に位置情報を持っていません。そのため、GeoTiffはジオリファレンスという仕組みを使って画像の各ピクセルに位置情報を付与します。

例えば紙地図をスキャンした場合、GISではそのままでは使えないため、特徴がある点に位置情報を付与していき、ある程度の点に座標をつけたところでジオリファレンスを実施することでその画像自体が位置を持つことができます。

これらの作業自体はQGISでも行う事ができ、その結果としてGeoTiffに保存するという流れになります。

#### Keyhole Markup Language (KML)

Keyhole Markup Language(以下KML)は、Google Earthで使われている位置情報と時系列を持ったベクターデータを扱うファイル形式です。

ファイルの拡張子は`.kml`です。

KMLはGoogleのプロダクトでよく使われていましたが、XMLである事はファイル仕様が複雑であるため、Web上での主流としてはGeoJSONに取って代われました。

ただ、KMLを出力可能なプラットフォームやアプリケーションが多く存在し、アイコンの表示を標準でサポートしている点などからも現在でも用途によっては使われています。

#### CSV

CSVは表計算ソフトで使われるファイル形式です。QGISでは位置情報(緯度、軽度)を持つCSVファイルを扱うことができます。

CSVファイルは例えばオープンデータなどで、座標と名称などの属性などを持つデータとして公開されているものを取り込む事が多くあります。ただし、空間インデックスを持たないため、QGISではGeoPackageやFlatGeobufなどに保存して扱うと良いでしょう。

## QGISで扱えるデータ形式について

QGISでは様々なデータを扱うことができます。

### ESRI Shapefile

ESRI Shapefile(以下Shapefile)は古くからベクター向け地図データとして使われてきたファイル形式です。

ファイルの拡張子は`.shp`ですが、これ以外にもデータを格納する`.dbf`や、投影法などを管理するための`.prj`ファイルなどに分割されているため、一ファイルだけでは役に立たないという特徴があります。

また、過去の遺産として使えるケースがありますが、日本語の扱いに問題があるケースが多いため、現在では保存形式としては推奨されていません。

代わりにGeoPackageなどの最新のファイルを使うことを推奨します。

### GeoPackage

TBD...

### SpatialLite

TBD...

### GeoJSON

TBD...

### FlatGeobuf

TBD...

### Keyhole Markup Language (KML)

TBD...

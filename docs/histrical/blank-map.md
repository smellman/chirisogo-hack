## 世界地図の白地図

世界地図を表示するにはOpenStreetMapなど便利なタイルを使うことができますが、歴史的な表現をする場合には白地図から開始した方が良いこともあります。

世界地図のデータとしては[Natural Earth](https://www.naturalearthdata.com/)が利用可能ですが、執筆現在でダウンロードに問題があります。代わりにNatural Earthの[Github](https://github.com/nvkelso/natural-earth-vector)からダウンロードするという方法があり、執筆現在ではこちらからダウンロードをするのをお勧めします。

まず、Githubのページに移動します。そして、Releaseの箇所をクリックします。

![GithubのReleaseの箇所](./images/blank-1.png)

次に、Releaseページの一番下にある`Source code(zip)`をダウンロードします。

![Source code(zip)の箇所](./images/blank-2.png)

なお、Natural Earthの全てのファイルをダウンロードすることになるので、時間がかかります。ただし、Natural Earthのデータは多岐にわたっているので、白地図以外のデータの作成にも使えるのでダウンロードしておいて損はありません。

ダウンロードが終わったらファイルを展開して、中にある`10m_cultural/ne_10m_admin_0_countries.shp`をQGISで開きます。

![QGISで開いた状態](./images/blank-3.png)

初期状態では色がついているので、レイヤを選択して右クリックからプロパティを開き、色を変更しましょう。

![プロパティで色の塗りつぶしを変更](./images/blank-4.png)

色が白く変更されたら作成が完了です。

![白地図の完成](./images/blank-5.png)

あとは使いませるようにプロジェクトファイルを保存しておくと便利です。また、Shapefileは取り回しが面倒なので、GeoPackageなどにしておくとさらに便利になります。

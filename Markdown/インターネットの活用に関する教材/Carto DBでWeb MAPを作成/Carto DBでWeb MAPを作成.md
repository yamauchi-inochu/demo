# Carto DBでWeb MAPを作成
本教材は、CartoDBを用いて空間データを表示する手法について解説しています。CartoDBを用いたインターネットによる地図データの分析や公開を行います。
本教材を使用する際は、[利用規約]をご確認いただき、これらの条件に同意された場合にのみご利用下さい。

[利用規約]:https://github.com/yamauchi-inochu/demo/blob/master/利用規約.md

**Menu**
------
* [CartoDBとは？](#CartoDBとは？)
* [アカウント取得](#アカウント取得)
* [データを読み込む](#データを読み込む)
* [NEWマップを作成する](#NEWマップを作成する)
* [SQLでデータを分析する](#SQLでデータを分析する)

**使用データ**

* [越前市オープンデータ] 越前市防災安全課　一次避難場所（風水害）、浸水想定区域（風水害）のデータを加工し、利用。
(http://www.city.echizen.lg.jp/office/010/021/open-data-echizen.html )



[越前市オープンデータ]:http://www.city.echizen.lg.jp/office/010/021/open-data-echizen.html


**スライド教材**
スライドのダウンロードは[こちら]
[こちら]:https://github.com/yamauchi-inochu/demo/raw/master/Markdown/%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%8D%E3%83%83%E3%83%88%E3%81%AE%E6%B4%BB%E7%94%A8%E3%81%AB%E9%96%A2%E3%81%99%E3%82%8B%E6%95%99%E6%9D%90/Carto%20DB%E3%81%A7Web%20MAP%E3%82%92%E4%BD%9C%E6%88%90/Carto%20DB%E3%81%A7Web%20MAP%E3%82%92%E4%BD%9C%E6%88%90.pptx
--------

## CartoDBとは？

- 地図データや地図を編集・共有できるサービス
- データのインポート・表示が簡単にできる
- SQLによるデータの分析がブラウザ上で可能
- 時系列データのなど表現が多様

[▲メニューへもどる]  
[▲メニューへもどる]:https://github.com/yamauchi-inochu/demo/blob/master/Markdown/%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%8D%E3%83%83%E3%83%88%E3%81%AE%E6%B4%BB%E7%94%A8%E3%81%AB%E9%96%A2%E3%81%99%E3%82%8B%E6%95%99%E6%9D%90/Carto%20DB%E3%81%A7Web%20MAP%E3%82%92%E4%BD%9C%E6%88%90/Carto%20DB%E3%81%A7Web%20MAP%E3%82%92%E4%BD%9C%E6%88%90.md#menu

## アカウント取得
![アカウント取得](pic/pic_1.png)  
[CartoDBの公式サイト]にアクセスする、SIGN UPをクリックし、アカウント作成を行う。

[CartoDBの公式サイト]:https://cartodb.com

[▲メニューへもどる]  

## データを読み込む
![データを読み込む](pic/pic_2.png)  
DATASETSをクリックして、dashboardを開く。

![データを読み込む](pic/pic_3.png)  
NEW DATASETをクリックし、Drag & drop か　BROWSEからファイルを選択し、データを読み込む。

![データを読み込む](pic/pic_4.png)  
DATA VIEW でテーブルデータが表示でき、MAP VIEWで地図が表示できる。
黄色枠のボタンで戻ることができるため、一次避難所のデータも読み込む。

[▲メニューへもどる]  

## <a name="NEWマップを作成する">NEWマップを作成する
![NEWマップ](pic/pic_5.png)  
Datasetsの横の下三角ボタンから、Your mapsをクリックする。

![NEWマップ](pic/pic_6.png)  
NEW MAP をクリックし、読み込むデータをDatasetsから選択する。

![NEWマップ](pic/pic_7.png)  
MAPが表示できたので、各レイヤのスタイル、凡例などを変更する。

![NEWマップ](pic/pic_8.png)  
CATEGORYを選択し、想定浸水深で色分けを行う。

![NEWマップ](pic/pic_9.png)  
想定浸水深のフィールドを選択し、ポッポアップで浸水深が表示されるようにする。

![NEWマップ](pic/pic_10.png)  
凡例の設定を行う。

![NEWマップ](pic/pic_11.png)  
フィルターをかけ、表示するレイヤを設定することができる。

![NEWマップ](pic/pic_12.png)  
想定浸水区域のポリゴンと同じように、ポイントデータのスタイルを変更する。

![NEWマップ](pic/pic_13.png)  
地図の名前を変更し、Optionsから地図表示の設定を行う。

![NEWマップ](pic/pic_14.png)  
Change basemap から　ベースマップを変更することができる。  
※　Yoursからタイル読み込みも可能。

![NEWマップ](pic/pic_15.png)  
レイヤの設定が完了したら、右上のPUBLISHをクリックする。  
Get the link からURLをコピーし、ブラウザで検索する。

![NEWマップ](pic/pic_16.png)  
ブラウザで地図が表示できるようになった。

[▲メニューへもどる]  

## <a name="SQLでデータを分析する">SQLでデータを分析する
![SQL](pic/pic_17.png)  
Apply queryをクリックして、コードを実行する。  
ＳＱＬから、上のコードを入力し、想定浸水区域内の一時避難所を抽出する。

```
SELECT
    flood_assumed_area.SAFIELD001,refuge.SAFIELD004 ,refuge.the_geom
FROM flood_assumed_area
JOIN refuge
ON ST_Contains(flood_assumed_area.the_geom ,refuge.the_geom)

```

![SQL](pic/pic_18.png)  
想定浸水区域内のデータが抽出されたのをDATA VIEWとMAP VIEWで確認する。  
create dataset from query or clear viewをクリックし、新規にデータセットを作成する。

![SQL](pic/pic_19.png)  
新規にデータセットが作成できた（必要があれば名称を変更しておく）。  
作成していたマップに戻り、新規に作成したデータセットを追加する。

![SQL](pic/pic_20.png)  
create dataset from query をクリックし、+ボタンから新規に作成したデータセットを追加する。

![SQL](pic/pic_21.png)  
地図のレイアウトを整え、ブラウザで表示する。

[▲メニューへもどる]  

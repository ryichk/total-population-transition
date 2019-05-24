# total-population-transition

> 都道府県別の総人口推移グラフを表示するSPA

## アプリ詳細

1. RESAS(地域経済分析システム) APIの「都道府県一覧」からAPIを取得する

2. APIレスポンスから都道府県一覧のチェックボックスを動的に生成する

3. 都道府県にチェックを入れると、RESAS APIから選択された都道府県の「人口構成」を取得する

4. 人口構成APIレスポンスから、X軸:年、Y軸:人口数の折れ線グラフを動的に生成して表示する

## 制約

* Reactをベースに、最新版(9/26時点で v16.5.2)でSPAを構築すること

* 都道府県一覧および総人口情報はRESAS APIのデータを用いること

* グラフは Highcharts や Rechart.js サードパーティ製のグラフライブラリを用いて描画すること

* グラフライブラリは任意のものを用いる

* Google Chrome最新版で正しく動くこと


## 参考
* [RESAS API](https://opendata.resas-portal.go.jp/)

* [RESAS API仕様書](https://opendata.resas-portal.go.jp/docs/api/v1/index.html)

* [React.js](https://reactjs.org/)

* [Highcharts](https://www.highcharts.com/)

* [Recharts.js](http://recharts.org/en-US/)


## Build Setup

``` bash
# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, checkout the [Nuxt.js docs](https://github.com/nuxt/nuxt.js).


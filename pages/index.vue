<template>
  <section>
    <v-container pl-5 fluid>
      <v-layout>
        <v-btn outline color="indigo">都道府県</v-btn>
      </v-layout>
      <v-layout row wrap>
        <v-flex xs3 sm2 v-for="(prefecture, i) in this.prefectures" :key="i">
          <v-checkbox
            :input-value="check"
            :label="prefecture.prefName"
            :value="prefecture.prefCode"
            @change="onChange(prefecture.prefCode, prefecture.prefName)"
          />
        </v-flex>
      </v-layout>
      <div class="chart">
        <vue-highcharts :options="options" ref="lineCharts"></vue-highcharts>
      </div>
    </v-container>
  </section>
</template>

<script>
import axios from 'axios'
import VueHighcharts from 'vue2-highcharts'

export default {
  components: {
      VueHighcharts
  },
  data(){
    return{
      check: false,
      result: [],
      asyncData: {
        name: '',
        marker: {
          symbol: 'square'
        },
        data: []
      },
      options: {
        chart: {
          type: 'spline'
        },
        title: {
          text: '都道府県別の総人口推移'
        },
        subtitle: {
          text: 'Source: <a href="https://opendata.resas-portal.go.jp/docs/api/v1/population/composition/perYear.html">RESAS API'
        },
        xAxis: {
          title: {
            text: '年度'
          },
          categories: ['1960','1965','1970','1975','1980', '1985', '1990', '1995', '2000', '2005',
            '2010', '2015', '2020', '2025', '2030', '2035', '2040', '2045']
        },
        yAxis: {
          title: {
            text: '人口数'
          },
          labels: {
            formatter: function () {
              return this.value;
            }
          }
        },
        tooltip: {
          crosshairs: true,
          shared: true
        },
        credits: {
          enabled: false
        },
        plotOptions: {
          spline: {
            marker: {
              radius: 2,
              lineColor: '#666666',
              lineWidth: 1
            }
          }
        },
        series: []
      }
    }
  },
  asyncData({params}){
    return axios
        .get("https://opendata.resas-portal.go.jp/api/v1/prefectures", {
          headers: {
            "X-API-KEY": "LBWtY3kaN34EwSDpoCYYdYk1HQL4YNFoiPimyKeV"
          }
        })
        .then((response)=>{
          return {
            prefectures: response.data.result
          }
        })
  },
  methods:{
    onChange(prefCode, prefName){
      this.check = true;
      this.asyncData.name = prefName;
      axios
        .get("https://opendata.resas-portal.go.jp/api/v1/population/composition/perYear?prefCode="+ prefCode, {
          headers: {
            "X-API-KEY": "LBWtY3kaN34EwSDpoCYYdYk1HQL4YNFoiPimyKeV"
          }
        })
        .then(response => this.asyncData.data = response.data.result.data.find(re => re.label === "総人口").data.map(x => x.value));
      let lineCharts = this.$refs.lineCharts;
      lineCharts.delegateMethod('showLoading', 'Loading...');
      setTimeout(() => {
          lineCharts.addSeries(this.asyncData);
          lineCharts.hideLoading();
      }, 2000)
    }
  }

}
</script>

<style>
.chart{
  margin-top: 50px;
}
</style>


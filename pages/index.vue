<template>
  <section>
    <v-container pl-5 fluid>
      <v-layout>
        <v-btn outline color="indigo">都道府県</v-btn>
      </v-layout>
      <v-layout row wrap>
        <v-flex xs3 sm2 v-for="(prefecture, i) in this.prefectures" :key="i">
          <v-checkbox
            v-model="prefecture.prefCode"
            :label="prefecture.prefName"
            :input-value="prefecture.prefCode"
            @change="onChange(prefecture.prefCode)"
          />
        </v-flex>
      </v-layout>
    </v-container>
  </section>
</template>

<script>
import axios from 'axios'

export default {
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

}
</script>

<style>
</style>


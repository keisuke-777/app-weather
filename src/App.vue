<template>
  <v-container grid-list-md>
    <v-layout wrap>
      <v-flex xs4>
        <v-card>
          <v-img
            v-bind:src="imgUrl"
            aspect-ratio="1.45"
          ></v-img>

          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">{{ card_title }}</h3>
              <div> {{ temp }} </div>
              <div> {{ temp_max }} </div>
              <div> {{ temp_min }} </div>
              <div> {{ humidity }} </div>
              <div> {{ weather }} </div>
            </div>
          </v-card-title>
        
          <!-- <v-card-actions>
              <v-btn flat color="orange">Share</v-btn>
              <v-btn flat color="orange">Explore</v-btn>
          </v-card-actions> -->
        </v-card>
      </v-flex>

      <v-flex xs4>
        <v-card>
          <v-img
            v-bind:src="imgUrl_t"
            aspect-ratio="1.45"
          ></v-img>

          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">{{ card_title_t }}</h3>
              <div> {{ temp_t }} </div>
              <div> {{ temp_max_t }} </div>
              <div> {{ temp_min_t }} </div>
              <div> {{ humidity_t }} </div>
              <div> {{ weather_t }} </div>
            </div>
          </v-card-title>
        
          <!-- <v-card-actions>
              <v-btn flat color="orange">Share</v-btn>
              <v-btn flat color="orange">Explore</v-btn>
          </v-card-actions> -->
        </v-card>
      </v-flex>

      <v-flex xs4>
        <v-card>
          <v-img
            v-bind:src="imgUrl_l"
            aspect-ratio="1.45"
          ></v-img>

          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">{{ card_title_l }}</h3>
              <div> {{ temp_l }} </div>
              <div> {{ temp_max_l }} </div>
              <div> {{ temp_min_l }} </div>
              <div> {{ humidity_l }} </div>
              <div> {{ weather_l }} </div>
            </div>
          </v-card-title>
        
          <!-- <v-card-actions>
              <v-btn flat color="orange">Share</v-btn>
              <v-btn flat color="orange">Explore</v-btn>
          </v-card-actions> -->
        </v-card>
      </v-flex>
    </v-layout>

    

    <input type="number" v-model="lat" placeholder="緯度を入力" maxlength="3" min="-90">
    <br>
    <input type="number" v-model="lon" placeholder="経度を入力" maxlength="4" min="-180">
    <br>
    <v-btn outlline round class="green lighten-4" @click="getWeather()">天候情報を入手</v-btn>
  </v-container>
</template>


<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

<script>
import axios from 'axios';
export default {
  data () {
    return {
      imgUrl: "https://www.silhouette-illust.com/wp-content/uploads/2016/05/1327-300x300.jpg",
      card_title: "任意の都市の天候を表示できます",
      temp: "緯度/経度を下のテキストボックスに入力し、「天候情報を入手」を押して下さい。",
      temp_max: "※正の値が北緯および東経を、負の値が南緯および西経を示します。OpenWeatherMapに登録されている緯度・軽度のみしか取得できません。(例: 30,130)",
      temp_min: "",
      humidity: "",
      weather: "",
      lat : "",
      lon : "",

      imgUrl_t: "",
      card_title_t: "",
      temp_t: "",
      temp_max_t: "",
      temp_min_t: "",
      humidity_t: "",
      weather_t: "",
      lat_t : "",
      lon_t : "",

      imgUrl_l: "",
      card_title_l: "",
      temp_l: "",
      temp_max_l: "",
      temp_min_l: "",
      humidity_l: "",
      weather_l: "",
      lat_l : "",
      lon_l : "",
    }
  },
  mounted: function () {
    this.$nextTick(function () { //ビュー全体がレンダリングされた後にのみ実行されるコード
      //tokyo
      axios.get("https://api.openweathermap.org/data/2.5/weather?q=Tokyo,jp&units=metric&appid=f632841c19fe9de0df3f4075e860a60d")
      .then( (response) => {
        this.imgUrl_t = "https://openweathermap.org/img/w/" + response.data.weather[0].icon + ".png";
        this.card_title_t = response.data.name;
        this.temp_t = "気温 : " + response.data.main.temp;
        this.temp_max_t = "最高気温 : " + response.data.main.temp_max;
        this.temp_min_t = "最低気温 : " + response.data.main.temp_min;
        this.humidity_t = "湿度 : " + response.data.main.humidity;
        this.weather_t = "天気 : " + response.data.weather[0].main;
      })
      .catch( (e) => {
        this.imgUrl_t = "https://www.silhouette-illust.com/wp-content/uploads/2016/05/1327-300x300.jpg";
        this.card_title_t = "東京の気候データを取得できませんでした";
        this.temp_t = "更新して下さい";
        this.temp_max_t = "";
        this.temp_min_t = "";
        this.humidity_t = "";
        this.weather_t = "";
      });

      //london
      axios.get("https://api.openweathermap.org/data/2.5/weather?q=London,GB&units=metric&appid=f632841c19fe9de0df3f4075e860a60d")
      .then( (response) => {
        this.imgUrl_l = "https://openweathermap.org/img/w/" + response.data.weather[0].icon + ".png";
        this.card_title_l = response.data.name;
        this.temp_l = "気温 : " + response.data.main.temp;
        this.temp_max_l = "最高気温 : " + response.data.main.temp_max;
        this.temp_min_l = "最低気温 : " + response.data.main.temp_min;
        this.humidity_l = "湿度 : " + response.data.main.humidity;
        this.weather_l = "天気 : " + response.data.weather[0].main;
      })
      .catch( (e) => {
        this.imgUrl_l = "https://www.silhouette-illust.com/wp-content/uploads/2016/05/1327-300x300.jpg";
        this.card_title_l = "ロンドンの気候データを取得できませんでした";
        this.temp_l = "更新して下さい";
        this.temp_max_l = "";
        this.temp_min_l = "";
        this.humidity_l = "";
        this.weather_l = "";
      });
    })
  },

  methods: {
    getWeather () {
      var baseUrl = 'https://api.openweathermap.org/data/2.5/find?';
      var APIKEY = 'f632841c19fe9de0df3f4075e860a60d';
      var url = baseUrl + 'lat=' + this.lat + '&lon=' + this.lon + '&cnt=1&appid=' + APIKEY;
      axios.get(url)
      .then( (response) => {
        this.imgUrl = "https://openweathermap.org/img/w/" + response.data.list[0].weather[0].icon + ".png";
        this.card_title = response.data.list[0].name;
        this.temp = "気温 : " + (response.data.list[0].main.temp - 273.15).toFixed(2);
        this.temp_max = "最高気温 : " + (response.data.list[0].main.temp_max - 273.15).toFixed(2);
        this.temp_min = "最低気温 : " + (response.data.list[0].main.temp_min - 273.15).toFixed(2);
        this.humidity = "湿度 : " + response.data.list[0].main.humidity;
        this.weather = "天気 : " + response.data.list[0].weather[0].main;
      })
      .catch( (e) => {
        this.imgUrl = "https://www.silhouette-illust.com/wp-content/uploads/2016/05/1327-300x300.jpg";
        this.card_title = "不正な緯度/経度です。";
        this.temp = "";
        this.temp_max = "";
        this.temp_min = "";
        this.humidity = "";
        this.weather = "";
      });
    }

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

html {
  height:100%;
  background: linear-gradient(rgb(190, 189, 194), rgb(230, 225, 225));
}

</style>
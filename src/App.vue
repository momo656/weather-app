<template>
  <div
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''
    "
  >
    <main>
      <div class="search-box">
        <input
          list="city"
          type="text"
          v-model="city"
          class="search-bar"
          @keypress="search"
          placeholder="Enter Your City"
        />
        <datalist class="list" id="city">
          <option
            :key="name.name"
            :value="name.name"
            v-for="name in cities"
          ></option>
        </datalist>
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">{{ getdate() }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ temp }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      city: "",
      weather: {},
      temp: "",
      cities: [
        { name: "Cairo" },
        { name: "Giza" },
        { name: "Alexandria" },
        { name: "Shubrā al Khaymah" },
        { name: "Sinnūris" },
        { name: "Al Manşūrah" },
        { name: "Ḩalwān" },
        { name: "Al Maḩallah al Kubrá" },
        { name: "Shibīn al Qanāţir" },
        { name: "Al Fayyūm" },
        { name: "Akhmīm" },
        { name: "Al Marāghah" },
        { name: "Ţanţā" },
        { name: "Awsīm" },
        { name: "Asyūţ" },
        { name: "Az Zaqāzīq" },
        { name: "Al ‘Ajamī" },
        { name: "Shibīn al Kawm" },
        { name: "Râs el-Barr" },
        { name: "Al ‘Āshir min Ramaḑān" },
        { name: "Damanhūr" },
        { name: "Al Minyā" },
        { name: "Mallawī" },
        { name: "Damietta" },
        { name: "Qinā" },
        { name: "Banī Suwayf" },
        { name: "Banhā" },
        { name: "Qalyūb" },
        { name: "Kafr ash Shaykh" },
        { name: "Disūq" },
        { name: "Mīt Ghamr" },
        { name: "Munūf" },
        { name: "Fāqūs" },
        { name: "Jirjā" },
        { name: "Al Badrashayn" },
        { name: "Ibshawāy" },
        { name: "Al Khānkah" },
        { name: "‘Izbat al Burj" },
        { name: "Kirdāsah" },
        { name: "Abnūb" },
        { name: "Al Minshāh" },
        { name: "Al Qurayn" },
        { name: "Abū Za‘bal" },
        { name: "Al Balyanā" },
        { name: "Al ‘Ayyāţ" },
        { name: "Al Badārī" },
        { name: "Kafr al Kurdī" },
        { name: "Abū Qīr" },
        { name: "Qahā" },
        { name: "Al Karnak" },
        { name: "Kafr Shukr" },
        { name: "Mīt Namā" },
        { name: "Banī Murr" },
        { name: "Al Madāmūd" },
        { name: "Birqāsh" },
        { name: "Kafr Ţaḩlah" },
      ],
    };
  },
  methods: {
    async search(e) {
      if (e.key === "Enter") {
        await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=bc6bcf8827d2dacd1b3352b0db8f252a`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setWeather);
      }
    },
    setWeather(data) {
      this.weather = data;
      this.temp = Math.round(this.weather.main.temp);
      console.log(data);
    },
    getdate() {
      let d = new Date();
      let months = [
        "january",
        "february",
        "march",
        "april",
        "may",
        "june",
        "july",
        "august",
        "september",
        "october",
        "november",
        "december",
      ];
      let days = [
        "sunday",
        "monday",
        "tuesday",
        "wednesday",
        "thursday",
        "friday",
        "saturday",
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;

  background-image: url("./assets/img-1.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  height: 100vh;
}
#app .warm {
  font-family: Avenir, Helvetica, Arial, sans-serif;

  background-image: url("./assets/warm.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  height: 100vh;
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 80%;
  padding: 10px;
  border-radius: 0px 15px 0px 15px;
  color: #313131;
  font-size: 16px;
  margin: 20px auto;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.5);
  transition: 0.4s;
}

.search-box .search-bar:focus {
  border-radius: 15px 0px 15px 0px;
  background-color: rgba(255, 255, 255, 0.8);
}
main {
  height: 100vh;
  padding: 5px;
  background-image: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.7));
}
.location-box .location {
  text-align: center;
  color: #fff;
  font-size: 35px;
  font-weight: 500;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  text-align: center;
  color: #fff;
  font-style: italic;
  font-size: 20px;
  font-weight: 500;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  text-align: center;
  color: #fff;
  font-size: 106px;
  font-weight: 900;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 16px;
  margin: 30px auto;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  text-align: center;
  color: #fff;
  font-style: italic;
  font-size: 48px;
  font-weight: 700;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

</style>

<template>
  <p class="header container">{{appData.title}}</p>
  <RowList :dataa="shownData" />
  <div class="btnContainer">
    <button class="moreBtn" @click="showData()">VIEW MORE</button>
  </div>
</template>

<script>
import RowList from "./components/RowList.vue";

export default {
  props: ["dataa"],
  name: "App",
  data() {
    return {
      appData:[],
      alldata: [],
      shownData: [],
      showFlag: false,
    };
  },
  components: {
    RowList,
  },
  mounted() {
    fetch(
      "https://api.rss2json.com/v1/api.json?rss_url=http://rss.cnn.com/rss/edition.rss"
    )
      .then((response) => response.json())
      .then((data) => {
        this.appData = data.feed;
        this.alldata = data.items;
        this.shownData = data.items.slice(0, 7);
      })
      .catch((e) => console.log(e.message));
  },
  watch: {
    showFlag: {
      handler() {
        this.shownData = [];
        if (this.showFlag == true) {
          this.shownData = this.alldata;
        } else {
          this.shownData = this.alldata.slice(0, 7);
        }
      },
      immediate: true,
    },
  },
  methods: {
    showData: function () {
      this.showFlag = !this.showFlag;
      console.log("The Shown Flag:", this.showFlag);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.header {
  display: flex; 
  align-self: start;
  font-size: 30px;
  font-weight: bold; 
  position: relative;
  color: #3a3a3a;
}

.header:after {
  content: '';
  position: absolute;
  width: 100%;
  transform: scaleX(0);
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #c7ca00;
  transform-origin: bottom right;
  transition: transform 1s ease-out;
}
.header:hover:after {
  transform: scaleX(1);
  transform-origin: bottom left;
}

.btnContainer {
  display: flex;
  margin: 3%;
  justify-content: center;
}

button{
  background-color: white;
  color: black;
}
</style>

<template>
  <Transition appear>
    <div>
      <div
        class="ImgComponent"
        :style="{ backgroundImage: 'url(' + dataa.enclosure.link + ')' }"
      >
        <div class="overlay" />
        <div class="content">
          <p class="title">{{ dataa.title }}</p>
          <p v-if="dataa.pubDate" class="date">
            {{ fixDate() }}
          </p>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
import { Transition } from "vue";
export default {
  name: "OneItem",
  data(){
    return{
      date:this.dataa.pubDate?.split(" ")[0]  // the date without hours
    }
  },
  props: ["dataa"],
  components: {
    Transition,
  },
  methods:{
    fixDate: function(){
      return this.date.split("-").reverse().join("/"); 
    }
  }
};
</script>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 2s ease, transform 1s ease-in-out;
  transform: translateY(0px);
}
.v-enter-from,
.v-leave-to {
  opacity: 0;
  transform: translateY(150px);
}
.ImgComponent {
  margin-top: 10px;
  height: 210px;
  background-size: cover;
  display: flex;
  align-items: flex-end;
  position: relative;
}
.overlay {
  width: 100%;
  height: 210px;
  z-index: 2;
  position: absolute;
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    color-stop(0%, rgba(137, 255, 241, 0)),
    color-stop(100%, rgba(0, 0, 0, 1))
  );
}
.content {
  z-index: 3;
}
.title {
  color: white;
  font-size: 20px;
  font-weight: bold;
  margin: 2%;
  text-overflow: ellipsis;
  overflow: hidden;
  display: -webkit-box;
  text-align: start;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
}
.title:hover {
  -webkit-box-orient: horizontal;
}
.date {
  color: rgb(179, 179, 179);
  font-size: 13px;
  margin: 0% 0% 3% 3%;
  align-self: start;
  display: flex;
}
</style>

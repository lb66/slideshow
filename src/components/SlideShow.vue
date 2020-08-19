<template>
  <div class="slideShow-wrap" @mouseenter="stop" @mouseleave="begin">
    <transition-group tag="ul" name="list">
      <li v-for="(item,index) in slideList" :key="index" v-show="index===currentIndex">
        <img :src="item.image" />
      </li>
    </transition-group>
    <div class="slideShow-items">
      <span
        v-for="(item,index) in slideList.length"
        :key="index"
        :class="{'active':index===currentIndex}"
        @click="change(index)"
      ></span>
    </div>
  </div>
</template>

<script>
export default {
  name: "SlideShow",
  data() {
    return {
      slideList: [
        { image: require("@/assets/img/1.jpg") },
        { image: require("@/assets/img/2.jpg") },
        { image: require("@/assets/img/3.jpg") },
      ],
      currentIndex: 0,
      timer: "",
    };
  },
  methods: {
    change(index) {
      this.currentIndex = index;
    },
    autoPlay() {
      this.currentIndex++;
      if (this.currentIndex > this.slideList.length - 1) {
        this.currentIndex = 0;
      }
    },
    begin() {
      this.timer = setInterval(() => {
        this.autoPlay();
      }, 4000);
    },
    stop() {
      clearInterval(this.timer), (this.timer = "");
    },
  },
  created() {
    this.begin();
  },
};
</script>

<style scoped lang='scss'>
* {
  padding: 0;
  margin: 0;
}
.slideShow-wrap {
  position: relative;
  overflow: hidden;
  width: 100%;
  height: 50vw;
  li {
    list-style: none;
    position: absolute;
    width: 100%;
    height: 100%;
    img {
      width: 100%;
      height: 100%;
    }
  }
  .slideShow-items {
    position: absolute;
    top: 45vw;
    width: 100%;
    text-align: center;
    span {
      display: inline-block;
      height: 8px;
      width: 32px;
      margin: 3px;
      background-color: #b2b2b2;
      cursor: pointer;
    }
    .active {
      background-color: orange;
    }
  }
}
.list-enter-active {
  transition: all 2s;
}
.list-leave-active {
  transform: translateX(-80%);
  transition: all 2s;
}
.list-enter {
  opacity: 0;
  transform: translateX(100%);
}
.list-leave-to {
  opacity: 0;
}
</style>

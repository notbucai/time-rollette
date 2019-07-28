<template>
  <div id="app">
    <div class="change">
      <p>{{langIndex===0?'小写':'大写'}}</p>
      <button @click="handleChange">切换</button>
    </div>
    <div class="year">
      <ul>
        <li class="active">{{year}}</li>
      </ul>
    </div>

    <div class="month" :style="{'transform':`rotate(-${date.month * 360/12}deg)`}">
      <ul>
        <li
          v-for="(item,index) in 12"
          :key="item"
          :class="{active: index === date.month}"
        >{{curretnLang.list[item]}}月</li>
      </ul>
    </div>

    <div class="noday" :style="{'transform':`rotate(-${date.date * 360/date.month_day_num}deg)`}">
      <ul>
        <li
          :style="{'transform':`rotate(${(index * 360/date.month_day_num)}deg) translate(100px)`}"
          v-for="(item,index) in date.month_day_num"
          :key="item"
          :class="{active: index === date.date}"
        >{{curretnLang.list[item]}}号</li>
      </ul>
    </div>

    <div class="day" :style="{'transform':`rotate(-${date.day * 52.4}deg)`}">
      <ul>
        <li
          v-for="(item,index) in curretnLang.weekday"
          :key="item"
          :class="{active: index === date.day}"
        >{{item}}</li>
      </ul>
    </div>

    <div class="h" :style="{'transform':`rotate(-${date.h * 15}deg)`}">
      <ul>
        <li
          v-for="(item) in 24"
          :key="item"
          :class="{active: (item-1) === date.h}"
        >{{curretnLang.list[item-1]}}点</li>
      </ul>
    </div>

    <div class="m" :style="{'transform':`rotate(-${date.m * 6}deg)`}">
      <ul>
        <li
          v-for="(item) in 60"
          :key="item"
          :class="{active: (item-1) === date.m}"
        >{{curretnLang.list[item-1]}}分</li>
      </ul>
    </div>

    <div class="s" :style="{'transform':`rotate(-${date.s * 6}deg)`}">
      <ul>
        <li
          v-for="(item) in 60"
          :key="item"
          :class="{active: (item-1) === date.s}"
        >{{curretnLang.list[item-1]}}秒</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      lang: [
        {
          chnNumChar: [
            "零",
            "一",
            "二",
            "三",
            "四",
            "五",
            "六",
            "七",
            "八",
            "九"
          ],
          list: [
            "零",
            "一",
            "两",
            "三",
            "四",
            "五",
            "六",
            "七",
            "八",
            "九",
            "十",
            "十一",
            "十二",
            "十三",
            "十四",
            "十五",
            "十六",
            "十七",
            "十八",
            "十九",
            "二十",
            "二十一",
            "二十二",
            "二十三",
            "二十四",
            "二十五",
            "二十六",
            "二十七",
            "二十八",
            "二十九",
            "三十",
            "三十一",
            "三十二",
            "三十三",
            "三十四",
            "三十五",
            "三十六",
            "三十七",
            "三十八",
            "三十九",
            "四十",
            "四十一",
            "四十二",
            "四十三",
            "四十四",
            "四十五",
            "四十六",
            "四十七",
            "四十八",
            "四十九",
            "五十",
            "五十一",
            "五十二",
            "五十三",
            "五十四",
            "五十五",
            "五十六",
            "五十七",
            "五十八",
            "五十九",
            "六十"
          ],
          weekday: [
            "星期天",
            "星期一",
            "星期二",
            "星期三",
            "星期四",
            "星期五",
            "星期六"
          ]
        },
        {
          // 拾
          chnNumChar: [
            "零",
            "壹",
            "贰",
            "叁",
            "肆",
            "伍",
            "陆",
            "柒",
            "捌",
            "玖"
          ],
          list: [
            "零",
            "壹",
            "贰",
            "叁",
            "肆",
            "伍",
            "陆",
            "柒",
            "捌",
            "玖",
            "拾",
            "拾壹",
            "拾贰",
            "拾叁",
            "拾肆",
            "拾伍",
            "拾陆",
            "拾柒",
            "拾捌",
            "拾玖",
            "贰拾",
            "贰拾壹",
            "贰拾贰",
            "贰拾叁",
            "贰拾肆",
            "贰拾伍",
            "贰拾陆",
            "贰拾柒",
            "贰拾捌",
            "贰拾玖",
            "叁拾",
            "叁拾壹",
            "叁拾贰",
            "叁拾叁",
            "叁拾肆",
            "叁拾伍",
            "叁拾陆",
            "叁拾柒",
            "叁拾捌",
            "叁拾玖",
            "肆拾",
            "肆拾壹",
            "肆拾贰",
            "肆拾叁",
            "肆拾肆",
            "肆拾伍",
            "肆拾陆",
            "肆拾柒",
            "肆拾捌",
            "肆拾玖",
            "伍拾",
            "伍拾壹",
            "伍拾贰",
            "伍拾叁",
            "伍拾肆",
            "伍拾伍",
            "伍拾陆",
            "伍拾柒",
            "伍拾捌",
            "伍拾玖",
            "陆拾"
          ],
          weekday: [
            "星期天",
            "星期壹",
            "星期贰",
            "星期叁",
            "星期肆",
            "星期伍",
            "星期陆"
          ]
        }
      ],
      langIndex: 0,
      date: {
        h: 0,
        m: 0,
        s: 0,
        day: 0,
        month: 0,
        date: 0,
        year: 0,
        month_day_num: 30
      }
    };
  },
  computed: {
    curretnLang() {
      return this.lang[this.langIndex];
    },
    year() {
      const year_list = this.date.year.toString().split("");

      const year = year_list.map(item => this.curretnLang.chnNumChar[item]);

      return year.join("");
    }
  },
  mounted() {
    setInterval(this.handleUpdate, 30);
  },
  methods: {
    handleUpdate() {
      const date = new Date();
      this.date.h = date.getHours();
      this.date.m = date.getMinutes();
      this.date.s = date.getSeconds();
      this.date.day = date.getDay();
      this.date.month = date.getMonth();
      this.date.date = date.getDate();
      this.date.year = date.getFullYear();
      // 获取当月总天数
      this.date.month_day_num = new Date(
        this.date.year,
        this.date.month + 1,
        0
      ).getDate();
    },
    handleChange() {
      this.langIndex === 0 ? (this.langIndex = 1) : (this.langIndex = 0);
    }
  }
};
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
}
body {
  position: fixed;
  width: 100%;
  height: 100%;
  /* background-color: rgba(232,160,184,1); */
  /* background-image: linear-gradient(to top, #fad0c4 0%, #fad0c4 1%, #ffd1ff 100%); */
  /* background-image: linear-gradient(to top, #a18cd1 0%, #fbc2eb 100%); */
}
#app {
  width: 100%;
  height: 100%;
  background-image: linear-gradient(120deg, #89f7fe 0%, #66a6ff 100%);
  & > div {
    transition: all 1s linear;
    width: 0;
    height: 0;
    border-radius: 50%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
  }
}
#app .change {
  position: fixed;
  top: 30px;
  left: unset;
  right: 30px;
  z-index: 999;
  background-color: #303030;
  box-shadow: 0 0 10px 6px #4a4a4a;
  width: 100px;
  height: 100px;
  border-radius: 4px;
  padding: 10px;
  transform: none;
  color: #fff;
  font-size: 16px;
  font-weight: bold;
  display: flex;
  box-sizing: border-box;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  button {
    padding: 6px 10px;
    margin-top: 10px;
    background-color: #ee3b77;
    color: #fff;
    border: none;
    outline: none;
  }
}

ul {
  width: 100px;
  height: 60px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  li {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    display: inline-block;
    line-height: 60px;
    color: #fff;
    font-size: 12px;
    transition: all 0.2s ease-in-out;
    &.active {
      text-shadow: #02c9c9 0 0 10px, #02c9c9 0 0 20px, #02c9c9 0 0 30px,
        #02c9c9 0 0 30px, #02c9c9 0 0 70px, #02c9c9 0 0 80px, #02c9c9 0 0 100px;
    }
  }
}
.year li {
  font-size: 14px;
  font-weight: bold;
}

@for $i from 0 through 12 {
  .month ul li:nth-child(#{$i + 1}) {
    transform: rotate(30deg * $i) translate(50px);
  }
}

@for $i from 0 through 7 {
  .day ul li:nth-child(#{$i + 1}) {
    transform: rotate(1deg * $i * 360/7) translate(150px);
  }
}

@for $i from 0 through 24 {
  .h ul li:nth-child(#{$i + 1}) {
    transform: rotate(15deg * $i) translate(200px);
  }
}

@for $i from 0 through 60 {
  .m ul li:nth-child(#{$i + 1}) {
    transform: rotate(6deg * $i) translate(260px);
  }
}

@for $i from 0 through 60 {
  .s ul li:nth-child(#{$i + 1}) {
    transform: rotate(6deg * $i) translate(320px);
  }
}
</style>

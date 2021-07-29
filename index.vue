<template>
  <div class="c-ruler-time">
      <div class="ruler">
          <div class="time-box">
              <div :class="t.half?'half':'full'" v-for="(t, idx) in time_arr" :key="idx" @click="select_time(t, idx)">
                  <span v-if="!t.half&&!t.focus" class="text">{{t.text}}</span>
                  <span v-if="t.half" class="short"></span>
                  <span v-if="!t.half" class="long"></span>
                  <span v-if="t.focus" class="blue-text">{{t.text}}</span>
                  <div v-if="t.focus" class="blue-div"></div>
              </div>
          </div>
      </div>
  </div>
</template>
<script>
import { time_arr } from './data/time.js'
import { deepCopy } from './js/c_common.js'
export default {
  name: 'c-ruler-time',
  data() {
    return {
        cur_time: '12:00',
        time_arr: deepCopy(time_arr)
    }
  },
  props: {

  },
  methods: {
      select_time(t, idx) {
          this.cur_time = t.text
          this.time_arr.forEach(t => {
             t.focus = false
          })
          this.time_arr[idx].focus = true
          this.$emit('getTime', this.cur_time)
      }
  },
  watch: {

  },
  created() {
      this.$emit('getTime', this.cur_time)
  }
}
</script>
<style lang="less" scoped>
.ruler {
    width: fit-content;
    height: 38px;
    border: 1px solid #E9EBF5;
    box-sizing: border-box;
    border-radius: 5px;
    padding: 0px 14px;
    margin: 0 auto;
}

.time-box {
    display: flex;
    height: 100%;
    .half {
        cursor: pointer;
        width: 10px;
        height: 100%;
        position: relative;
        .short {
            position: absolute;
            left: 50%;
            top: 78%;
            transform: translate(-50%, -50%);
            width: 1px;
            height: 5px;
            background: #DFE1EB;
        }
    }
    .full {
        cursor: pointer;
        width: 30px;
        height: 100%;
        position: relative;
        .text {
          color: #C2C4CC;
          font-size: 10px;
        }
        .long {
            position: absolute;
            left: 50%;
            top: 77%;
            transform: translate(-50%, -50%);
            width: 1px;
            height: 8px;
            background: #DFE1EB;
        }
    }
    .blue-text {
        position: absolute;
        top: -24px;
        left: 50%;
        transform: translateX(-50%);
        color: #5EB2E4;
        font-size: 14px;
        font-weight: 600;
    }
    .blue-div {
        position: absolute;
        width: 3px;
        height: 42px;
        top: -3px;
        left: 50%;
        background: #5EB2E4;
        border-radius: 3px;
    }
}
</style>

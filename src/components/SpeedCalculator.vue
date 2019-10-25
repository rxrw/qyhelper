<template>
  <div>

      <div class="form-group">
        <label for="origin">原始天数</label>
        <input
          type="text"
          class="form-control"
          id="origin"
          aria-describedby="originHelp"
          placeholder="原始天数"
          v-model="origin_days"
        />
        <small id="originHelp" class="form-text text-muted">以点分隔，比如10.2.3.39代表10天2小时3分39秒</small>
      </div>

      <div class="form-group">
        <label for="speed">速度加成</label>
        <input
          type="number"
          class="form-control"
          id="speed"
          aria-describedby="speed"
          v-model="speed"
        />
        <small id="speed" class="form-text text-muted">只需要输入数字，百分号不用写</small>
      </div>


      <div class="form-group">
        <label for="help_time">联盟帮助次数</label>
        <input
          type="number"
          class="form-control"
          id="help_time"
          aria-describedby="help_time"
          v-model="help_time"
        />
        <small id="help_time" class="form-text text-muted">输入最大的可帮助次数</small>
      </div>


      <div class="form-group">
        <label for="actual_days">实际天数</label>
        <input
          type="text"
          class="form-control"
          id="actual_days"
          aria-describedby="actual_days"
          v-model="actual_days"
          disabled
        />
        <small id="actual_days" class="form-text text-muted">当前加成下点满联盟帮助后的天数</small>
      </div>

      <button type="submit" class="btn btn-primary" @click="calculate">计算</button>



  </div>
</template>
<script>
export default {
  name: "calculator",
  data() {
    return {
      origin_days: '',
      speed: 100,
      help_time: 30,
      actual_days: 0
    };
  },
  methods:{
    calculate(){
      let origin = this.origin_days.split(".")
      let seconds = origin[0] * 86400 + origin[1] * 3600 + origin[2] * 60 + Math.floor(origin[3])

      let actual_second = seconds / (1 + this.speed/100)

      let onepercent100 = actual_second * 0.01
      let helps = 0
      if (onepercent100 < 60) {
        helps = 60
      }else{
        helps = actual_second * 0.01
      }

      let help_secnods = this.help_time * helps
      let actual_seconds = actual_second - help_secnods

      let days = Math.floor(actual_seconds / 86400)
      let hours = Math.floor((actual_seconds % 86400) / 3600)
      let minutes = Math.floor(((actual_seconds % 86400) % 3600) / 60)
      let seconds1 = Math.round(((actual_seconds % 86400) % 3600) % 60)

      this.actual_days = days + "天" + hours + "时" + minutes + "分" + seconds1 + "秒";
    }
  }

};
</script>
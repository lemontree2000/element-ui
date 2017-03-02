<template>
  <div class="hello">
    <el-select v-model="value8" filterable placeholder="请选择" @click.native="select" :loading="loading">
        <el-option
          v-for="item in options"
          :label="item.label"
          :value="item.value">
        </el-option>
      </el-select>
  </div>
</template>

<script>
import ElementUI from 'element-ui';

export default {
  name: 'hello',
  data () {
    return {
      value8: '',
      options: [],
      loading: false
    }
  },
  methods: {
    select () {
      if (this.options.length) {
          return;
      }
      this.loading = true;
      this.$http({
        method: 'post',
        url: '/b_api_cian/get_select_brand'
      }).then((response) => {
        this.loading = false;
        let dataArr = response.data.RESULT;
        
        for (let i = 0; i < dataArr.length; i++) {
          this.options.push({value: dataArr[i].ID,label: dataArr[i].NAME});
        } 
        console.log(this.options);
      }).catch((response) => {
        console.log(response);
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("//unpkg.com/element-ui/lib/theme-default/index.css");
</style>

<template>
  <div class="hello">
    <h2>{{msg}}</h2>
    <ul>
      <li v-for="item in personInfo" v-bind:key="item.SN">
        <p>姓名：{{item.name}}</p>
        <p>年龄：{{item.age}}</p>
        <p>籍贯：{{item.address}}</p>
      </li>
    </ul>
    <div>
      <el-button @click="show3 = !show3">Click Me</el-button>
      <div style="margin-top: 20px; height: 200px;">
        <el-collapse-transition>
          <div v-show="show3">
            <div class="transition-box">el-collapse-transition</div>
            <div class="transition-box">el-collapse-transition</div>
          </div>
        </el-collapse-transition>
      </div>
    </div>
    <el-date-picker
      type="datetimerange"
      range-separator="至"
      start-placeholder="开始日期"
      end-placeholder="结束日期"
    >
    </el-date-picker>
  </div>
  
</template>

<script>
import  Vue  from 'vue'
import axios from 'axios'
Vue.prototype.$axios = axios
export default {
  name: 'HelloWorld',
  data () {
    return {
     personInfo:[],
     msg:'',
     show3:true
    }
  },
  mounted() {
    this.getPageData();
  },
  methods: {
    getPageData () {
      this.personInfo = []
      this.$nextTick(() => {
        this.$axios.post('http://easymock.dev.e6gpshk.com:30081/mock/5d1c19b753377c0021069806/testdataAPI/testdataAPI')
          .then(e => {
            this.personInfo = e.data.data.dataList
             console.log(this.personInfo)
            this.msg = e.data.data.msg
          })
          .catch(err => {
            console.log(err)
          })
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h2{
  border-bottom: 1px solid #666;
}
li{
  list-style: none;
  border-bottom: 1px solid #666;
}
.transition-box {
    margin-bottom: 10px;
    width: 200px;
    height: 100px;
    border-radius: 4px;
    background-color: #409EFF;
    text-align: center;
    color: #fff;
    padding: 40px 20px;
    box-sizing: border-box;
    margin-right: 20px;
  }
</style>

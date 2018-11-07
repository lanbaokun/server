<template>
    <div class="right">
            <div class="right-box">
                <div class="right-title">
                    <h5>自定义表单项</h5>
                </div>
                <div class="right-content">
                    <form role="form" class="form-horizontal">
                        <p><b>常用项</b></p>
                        <table>
                            <tr>
                                <td v-for="(item,key) in newarr" :key="key" @click="btnList(item)" @mouseover="hoveBag(key)" @mouseout="hoveBag(null)" :class="{ background : hovebag == key}">
                                    <div id="name">
                                       {{item.name}}
                                    </div>
                                </td>
                            </tr>
                        </table>
                        <p><b>自定义项</b></p>
                        <div id="text" class="form-group" v-for="(item,key) in listData" :key="key" @click="btnList(item)" @mouseover="hoveBor(key)" @mouseout="hoveBor(null)" :class="{ border : hovebor == key}">
                            <label class="label"> <i class="icon iconfont icon-jia"></i> {{item.name}} 
                            <img :src='item.img'></label>
     
                        </div>
                    </form>
                </div>
       </div>
   </div>



</template>

<script>
 import listData from '../js/data.js'
 export default {
   data () {
    return {
        newarr : [{
                name:'姓名',
                type:'text'
            },{   
                name:'电话',
                type:'text'
            },{
                name:'邮箱'
            },{
                name:'身份证',
                type:'text'      
            },{
                name:'个人网站',
                type:'text'
            },{
                name:'上传Logo',
                type:'text'
            },{
                name:'性别',
                type:'radio'
            },{
                name:'职位',
                type:'text'
            },{
                name:'个人简历',
                type:'text'
            }],
        hovebag:null,
        hovebor:null
    }
  },
  props: {
       listData: {
           type:Array,
           default:()=>listData
       }
   },
  methods:{
     btnList(name){
      this.$emit('btnList',name)
     },
     hoveBag(key){
         this.hovebag = key;
     },
     hoveBor(key){
         this.hovebor = key;
     }
  }
}
</script>
<style scoped>
 .right .right-box .right-content .form-horizontal .background{
    background: #0099FF;
}
 .right .right-box .right-content .form-horizontal .background #name{
    color:#fff;
}
 .right .right-box .right-content .form-horizontal .border{
   border: 1px solid #0099FF;
}
</style>
<template>
    <div class="left" :class="showFlag === true ? `left` : `newleft`">
       <div class="left-box">
          <div class="left-title">
            <h5>拖拽/点击右侧表单项到此区域</h5>
            <div class="left-btn">
                <button type="submit" class="btn btn-warning" data-clipboard-text="testing" id="copy-to-clipboard" @click="copyJS">复制代码</button>
                <button type="button" class="btn btn-yulan" @click="btnPreview">预览</button>
            </div>
          </div>
          <div class="left-content" ref="copybox">
            <div class="row form-body form-horizontal m-t">
                 <ul>
                     <li v-for="(item,key) in list" :key="key">
                  
                         <p>{{item.name}}:</p>
                         <input :type="item.type" :placeholder="`请输入你的${item.name}`">
                         <i class="icon iconfont icon-set" @click="addArr(key)"></i>
                         <i class="icon iconfont icon-lajitong" @click="removeArr(key)"></i>
                        <div class="check-box" >
                          <input type="checkbox" @change="isTian(key)">
                          <span>必填</span>
                        </div>
                     </li>
                 </ul>
            </div>
            <div class="mark-box"  v-show="flag">
              <div class="mark">
                <p>表单信息设置 <span @click="remove">X</span> </p>
                 <ul>
                     <li>
                         <p>标题:</p>
                         <input type="text" :placeholder="`${inputVal.name}`" v-model="setval.name">
                     </li>
                     <li>
                         <p>提示信息:</p>
                         <input type="text" :placeholder="`请输入你的${inputVal.name}`" v-model="setval.value">
                     </li>
                 </ul>
                 <button @click="setArr">确定</button>
              </div>
            </div>
            <div class="copy-mock"  v-if="copyflag">
             <div class="copy">
                  <div class="copy-h">
                      <p>复制HTML代码</p>
                      <span @click="setCopy">x</span>
                  </div>
                
                <div class="copy-section">
                    {{html}}
                </div>
              </div>
            </div>
             
         </div>
       </div>
    </div>
</template>
<script>
export default{
    props:{
        arr:{
            type:Array,
            default:[]
        }
    },
    data(){
        return{
            list:this.arr,    
            flag:false,
            setval:{
                name:'',
                value:''
            },
            showFlag:true,
            inputVal:'',
            copyflag:false,
            key: null      
        }
    },
    methods:{
        //控制mark显示
        addArr(key){
            this.key = key;
            this.flag = true;
            // this.key = key;
            this.inputVal = this.list[key]
        },
        //点击修改mark里面的内容
        setArr(){
             this.flag = false;
             this.arr[this.key].name = this.setval.name;
             this.arr[this.key].value = this.setval.value;
            //  if(this.flag === false){
            //    this.setval.name = '';
            //  }
        },
        //点击预览
        btnPreview(){
           this.showFlag = !this.showFlag;
           this.$emit('show',this.showFlag)
        },
        //点击是否删除
        removeArr(key) {
            let flag = confirm('是否删除');
                if(flag){
                    this.arr.splice(key,1);
                }
        },
        remove(){
          this.flag = false;
        } ,
        isTian(key){
          let flag = confirm('选中');
        },
        copyJS(){
           this.copyflag = true;
           this.html = this.$refs.copybox.innerHTML;
        },
          setCopy(){
                this.copyflag = false;
            },

    }
}
</script>
<style scoped>
.left-content ul li{
    width: 80%;
    height: .4rem;
    display: flex;
    align-items: center;
    margin: .1rem auto;

}
.left-content ul li p{
    width: 15%;
    line-height: .4rem;
    text-align: right;
    color:#898A8B;
}
.left-content ul li input{
   width: 60%;
   height: .4rem;
   margin-left: .1rem;

}
.left-content ul li i{
   margin-left: .1rem;
   color:#898A8B;
}
.mark-box{
    width: 100%;
    height: 100%;
    position: absolute;
    left:0;
    top:0;
    background: rgba(0, 0, 0, .5)
}
.mark-box .mark{
width: 60%;
margin: 0 auto;
margin-top: .2rem;
height: 2.5rem;
border: 1px solid #ccc;
background: #fff;
border-radius: .02rem;
}
.mark-box .mark>p{
    height: .5rem;
    line-height: .5rem;
    padding: 0 .1rem;
    font-size: .18rem;
    color:#676a6c;
    border-bottom: 1px solid#ccc;
    display: flex;
    justify-content: space-between;
}
.mark-box .mark>p span{
      color:#676a6c;
}
.mark-box .mark button{
    margin-left: .2rem;
    background: #1c84c6;
    border: 1px solid #1c84c6;
    color:#fff;
    border-radius: .03rem;
    padding: .05rem .1rem ;
}
.check-box{
    display: flex;
}
.copy-mock{
    width: 100%;
    height: 100%;
    position: absolute;
    left:0;
    top:0;
    background: rgba(0, 0, 0, .5)
}
.copy{
   border: 1px solid #ccc;
   width: 60%;
    margin: 0 auto;
    margin-top: .2rem;
    height: auto;
    border: 1px solid #ccc;
    background: #fff;
    border-radius: .02rem;
}
.copy .copy-h{
    display: flex;
    height: .5rem;
    line-height: .5rem;
    justify-content: space-between;
    padding: 0  .1rem;
    border-bottom: 1px solid #ccc;
}

</style>


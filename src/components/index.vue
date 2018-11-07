<template>
   <div class="wraps">
      <div class="wrap">
        <header></header>
        <section>
          <Left :arr="arr" @show="getFlag"/>
          <Right @btnList="pushList" v-if="showFlag"/>
        </section>
      </div>
   </div>
    
</template>

<script>
import Left from './left'
import Right from './right'
export default {
  data () {
    return {
        arr:[],
        showFlag:true
    }
  },
  props:{
    name
  },
  methods:{
    pushList(item){
      console.log(item)
        this.arr.push(
          item
        )
        // console.log(item)
    },
    getFlag(key){
      this.showFlag = key;
    }
  },
  components:{
    Left,Right
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

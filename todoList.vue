<template>
  <div class="wrapper">
      <h1>what you need to do is follows</h1>
      <input v-model="newList" @keyup.enter='addNew'>
      <ul>
          <li v-for="list in lists" :key="list.id" :class="{grey:list.isFinished}">
              {{list.id}}--{{list.label}}<button v-if='!list.isFinished' @click='changeStatus'>已完成</button>
              <button v-else @click='changeStatus'>未完成</button>
          </li>
      </ul>
      <p>共计：{{nums}};已完成:{{finished}};待完成:{{unFinished}}</p>
  </div>
</template>

<script>
export default {
  components:{},
  props:{},
  data(){
    return {
        lists:[
            {id:1,label:'HTML',isFinished:false},
            {id:2,label:'CSS3',isFinished:false},
            {id:3,label:'Node',isFinished:false}
        ],
        newList:''
    }
  },
  watch:{},
  computed:{
      nums(){
          return this.lists.length;
      },
      finished(){
          let finished=0;
          for(let i of this.lists){
              if(i.isFinished==true){
                  finished++;
              }
          }
          return finished;
      },
      unFinished(){
          return this.nums-this.finished;
      }
  },
  methods:{
      addNew(){
          let index=this.nums+1;
          this.lists.push({
              id:index,
              label:this.newList,
              isFinished:false
          });
          this.newList='';

      },
      changeStatus(event){
          let targetIndex=parseInt(event.target.parentNode.innerHTML.trim().substring(0,1));
          this.lists[targetIndex-1].isFinished=!this.lists[targetIndex-1].isFinished;
      }
  },
  created(){},
  mounted(){}
}
</script>
<style scoped>
.grey{
    color: grey;
}
li{
    list-style: none;
}
</style>
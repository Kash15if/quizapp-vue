<template>
<div>

<Questions v-if="!end" :qNo="qNo" :Quest="Quest" :last="last" v-on:submit="submitNext($event)" v-on:skip="skipNext($event)"></Questions>
<Result v-else :marks="marks" :rightAns="rightAns" :Ans="Ans"></Result>

</div>



</template>

<script>
import Questions from './question.vue'
import Result from './result.vue'


export default {
  name: 'Dashboard',
  props: {
  },
  components:{
    Questions,
    Result
  },
  data(){
      return{

Quest: [],
qNo: 1,
Ans: [],
rightAns: [],
end: false ,
last: false,
marks: 0
      }
  },

  methods:{

      skipNext(qAns){
          if(!this.last){
          this.Ans.push(qAns);
          this.qNo++;
          }

          if(this.qNo >= 5)
            this.last = true; 
      },

      submitNext(qAns){    
          if(this.qNo <= 5){
          this.Ans.push(qAns);
          this.qNo++;
          }
        
          if(this.qNo > 5){
            this.end = true;
            for(let i = 1 ; i <= 5 ; i++){
                if(this.Ans[i-1] == this.rightAns[i-1]){
                    this.marks++;
                }  
            }
            }
      }

  },

  async created(){

      this.Quest = await require("../data/data.json")

      let j = 0;
      await this.Quest.forEach(element => {
          if(j >0)
            this.rightAns.push(element[7]);
          else
            j++;
      });

  }
}
</script>


<style >
</style>

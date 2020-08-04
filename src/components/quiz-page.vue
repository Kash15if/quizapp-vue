<template>
<div>
<div><h1 style="text-align:center;">Level {{level}}</h1></div>
<Questions v-if="!end" :qNo="qNo" :Quest="Quest" :last="last" v-on:submit="submitNext($event)" v-on:skip="skipNext($event)" v-on:timeEnds="timeExceed()"></Questions>
<Result v-else :marks="marks" :rightAns="rightAns" :Ans="Ans" v-on:nextLevel="nextLevel" :warning="warning"></Result>

</div>



</template>

<script>
import Questions from './question.vue'
import Result from './result.vue'


export default {
  name: 'Quiz-page',
  props: {
  },
  components:{
    Questions,
    Result
  },
  data(){
      return{

level: 1,
Quest: [],
qNo: 1,
Ans: [],
rightAns: [],
end: false ,
last: false,
marks: 0,
warning: '',
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
      },

      timeExceed(){
        this.end = true;
        this.Ans[this.qNo - 1 ] = "Not Answered";
        this.qNo++;

        while(this.qNo <= 5){
          this.Ans[this.qNo - 1 ] = "Unseen";
          this.qNo++;
        }
            for(let i = 1 ; i <= 5 ; i++){
                if(this.Ans[i-1] == this.rightAns[i-1]){
                    this.marks++;
                }  
            }
      },

      async nextLevel(){
        if(this.level < 2){
        this.last = false;
        this.end = false;
        this.qNo = 1;
        this.Ans = [];
        this.rightAns = [];
        this.marks = 0;
        this.level++;
        var data = await require("../data/data.json");
        this.Quest = await data[this.level - 1];
        console.log(this.Quest);

        let k = 0;
        await this.Quest.forEach(element => {
          if(k >0)
            this.rightAns.push(element[7]);
          else
            k++;
        });
        }
        else{
          this.warning = "Only 5 levels available"
        }
          
        
      }

  },

  async created(){

      var data = await require("../data/data.json");
      this.Quest = data[this.level - 1];

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

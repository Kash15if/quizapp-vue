<template>

<div class="Box">
    
    <Timer/>

    <div>
        <button type="button" class="skipBtn" @click="skip" >Skip<span class="material-icons">skip_next</span></button>

   </div><br>
    
    <div class="Ques">

        <h2 style="text-align: center;"> Question No. {{ qNo }}</h2>
    
        <h3>{{ Quest[qNo][2] }}</h3>

        <div style="font-family: 'Righteous', cursive;">
            <input type="radio"  name="ans" v-model="qAns" value="A" >
            <label for="A">{{ Quest[qNo][3] }}</label><br>
            <input type="radio"  name="ans" v-model="qAns" value="B">
            <label for="B">{{ Quest[qNo][4] }}</label><br>
            <input type="radio"  name="ans" v-model="qAns" value="C">
            <label for="C">{{ Quest[qNo][5] }}</label><br>
            <input type="radio"  name="ans" v-model="qAns" value="D">
            <label for="D">{{ Quest[qNo][6] }}</label>
        </div><br><br>

    </div>

    <button type="button" @click="submit" >Save and Next</button> 
   
    <p style="color:red; text-align:center;font-weight:bold" v-if="last">Can't skip , Quiz contains only {{qNo}} questions</p>

</div>

</template>

<script>
import Timer from './timer.vue'


export default {
  name: 'Question',
  props: {
      qNo: {
          type: Number,
          },
      Quest: {
          type: Array,
          },
      last:{
          type: Boolean
      }
  },
  components:{
    Timer
  },
  data(){
      return{
          qAns:""
      }
  },
  methods:{
      async skip(){ 
          await this.$emit('skip' , this.qAns);
          this.qAns = "Not Answered"
      },

      async submit(){
            await this.$emit('submit' , this.qAns);
            this.qAns = "Not Answered"
      }

  },
  created(){
      this.qAns = "Not Answered"
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>


.Box{
            margin-top: 3vh; 
            border: 2px solid #3D9970; 
            border-radius: 15px;
            height: auto;
        }

        .Box .Ques{
            text-align: left;
            padding: 5% 10% 0 10%;
            font-family: 'Righteous', cursive;
        }

        .Box button {
            font-size: 6vw;
            width: 80%;
            margin: 0% 10% 2.5% 10%;
            padding: 10px;
            background-color: #4CAF50;
            color: white; 
            border: 2px solid #4CAF50;  
            border-radius: 5px;  
        }


        .Box .skipBtn{
            float: right;
            width: auto;
            margin: 3%;
            border: 2px solid #ff0037;
            background-color: #ff0037;
        }

       
        .Box button:hover {
            background-color: white; 
            color: black;
            
        }

        .header {
            padding: 2px 25px 7px 25px;
            background: #1abc9c;
            color: white;

        }


        /* mediA query*/
        @media(min-width: 768px){
            .Box {
            margin: 10vh 15vw 0 15vw;
            }

        .Box button {
            font-size: 2vw;
            }
        }

        

</style>

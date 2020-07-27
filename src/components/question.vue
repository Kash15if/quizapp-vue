<template>
<div>

<div class="Box" v-if="!end">

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

    <button type="button" @click="submitNext" >Save and Next</button> 
   
    <p style="color:red; text-align:center;font-weight:bold" v-if="end">Can't skip , Quiz contains only 5 questions</p>

</div>

<div class="results" v-else>
    <h1>Your score is <b>{{marks}}</b></h1>
    <h1>Answers</h1>

    <table>
    <tr>
        <th>Q.No</th>
        <th>Right answer</th>
        <th>Your answer</th>
    </tr>
    <tr v-for="answer in Ans" :key="answer">
        <td>{{ }}</td>
        <td>{{ rightAns[i] }}</td>
        <td>{{answer}}</td>
    </tr>
    
    </table>

</div>

</div>



</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    
  },
  data(){
      return{
          Quest:[
    [
      "Q.No",
      "Q.Status",
      "Question",
      "Opt1",
      "Opt2",
      "Opt3",
      "Opt4",
      "Ans"
    ],
    [
        "1",
        "",
        "A student measured the length of a rod and wrote it as 3.50 cm. Which instrument did he use to measure it?",
        "Aaaaa lelleeeeee eeeeeeeee eeeeee eeeeeeeeeeeeeeeeee",
        "B",
        "C",
        "D",
        "C"
      ],
      [
        "2",
        "",
        "[qrdd         ",
        "pagal diwana",
        "B",
        "C",
        "D",
        "D"
      ],
      [
        "3",
        "",
        "A student measured the length of a rod and wrote it as 3.50 cm. Which instrument did he use to measure it?",
        "kaise bahana",
        "B",
        "C",
        "D",
        "A"
      ],
      [
        "4",
        "",
        "A student measured the length of a rod and wrote it as 3.50 cm. Which instrument did he use to measure it?",
        "A",
        "B",
        "C",
        "D",
        "A"
      ],
      [
        "5",
        "",
        "A student measured the length of a rod and wrote it as 3.50 cm. Which instrument did he use to measure it?",
        "A",
        "B",
        "C",
        "D",
        "A"
      ]

],

qNo: "",
qAns: "",
Ans: [],
rightAns: ["A","B","C","D","A"],
end: false ,
marks: 0
      }
  },

  methods:{

      skip(){
          if(this.qNo >= 5)
            this.end = true; 

          if(!this.end){
          this.Ans.push(this.qAns);
          this.qNo++;
          this.qAns = "";  
          }
          
      },

      submitNext(){   
          if(this.qNo >= 5)
            this.end = true; 

          if(this.end){
            for(let i = 1 ; i <= 5 ; i++){
                if(this.Ans[i-1] == this.rightAns[i-1]){
                    this.marks++;
                }
            }
            console.log(this.marks);
            console.log(this.Ans);
            console.log(this.rightAns);
          }
          else{
          this.Ans.push(this.qAns);
          this.qNo++;
          this.qAns = "";
          }
      }


  },

  created(){

      this.qNo = 1;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.results{
    margin-top: 10%;
    text-align: center;
}

table{
    width: 60%;
    margin-top: 5%;
    margin-left: 20%;
}

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

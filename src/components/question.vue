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
    <tr v-for="(answer , index) in rightAns" :key="index">
        <td>{{ index+1 }}</td>
        <td>{{ Ans[index] }}</td>
        <td>{{answer}}</td>
    </tr>
    
    </table>

    <button type="button" class="btnDn" style="margin-top:5%">Get Question paper on Email</button>

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
        "A can do a work in 15 days and B in 20 days. If they work on it together for 4 days, then the fraction of the work that is left is :",
        "1/4",
        "1/10",
        "7/15",
        "8/15",
        "D"
      ],
      [
        "2",
        "",
        "A can lay railway track between two given stations in 16 days and B can do the same job in 12 days. With help of C, they did the job in 4 days only. Then, C alone can do the job in:",
        "46/5",
        "47/5",
        "48/5",
        "10",
        "C"
      ],
      [
        "3",
        "",
        "A, B and C can do a piece of work in 20, 30 and 60 days respectively. In how many days can A do the work if he is assisted by B and C on every third day?",
        "16 days",
        "12 days",
        "15 days",
        "18 days",
        "C"
      ],
      [
        "4",
        "",
        "A is thrice as good as workman as B and therefore is able to finish a job in 60 days less than B. Working together, they can do it in:",
        "20 days",
        "45/2 days",
        "25 days",
        "30 days",
        "B"
      ],
      [
        "5",
        "",
        "A alone can do a piece of work in 6 days and B alone in 8 days. A and B undertook to do it for Rs. 3200. With the help of C, they completed the work in 3 days. How much is to be paid to C?",
        "Rs 400",
        "Rs 375",
        "Rs 600",
        "Rs 800",
        "A"
      ]

],

qNo: 1,
qAns: "Not answered",
Ans: [],
rightAns: [],
end: false ,
marks: 0
      }
  },

  methods:{

      skip(){
           

          if(!this.end){
          this.Ans.push(this.qAns);
          this.qNo++;
          this.qAns = "Not answered";  
          }

          if(this.qNo > 5)
            this.end = true;
          
      },

      submitNext(){   
           
          if(this.qNo <= 5){
          this.Ans.push(this.qAns);
          this.qNo++;
          this.qAns = "Not answered";
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

  created(){


      let j = 0;
      this.Quest.forEach(element => {
          if(j >0)
            this.rightAns.push(element[7]);
          else
            j++;
      });

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.results{
    margin-top: 10%;
    text-align: center;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  margin-top: 5%;
  margin-left: 0%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
  text-align: center;
}

.btnDn{
    padding: 15px;
    background-color: #1abc9c;
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

        table {
                width: 70%;
                margin-left: 15%;
            }

   
        }

        

</style>

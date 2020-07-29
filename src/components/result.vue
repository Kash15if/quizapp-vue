<template>
<div class="results">
    <h1>Your score is : <b>{{marks}}</b></h1>
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
</template>

<script>
export default {
  name: 'Result',
  props: {

      marks:{
          type: Number,
      },
      rightAns:{
          type: Array
      },
      Ans:{
          type: Array
      }

  },
}
</script>


<style>

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


        /* mediA query*/
        @media(min-width: 768px){
        table {
                width: 70%;
                margin-left: 15%;
            }
        }

        

</style>

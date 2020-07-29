<template>

<h3 v-bind:class="{timeout : timeout}">{{time}}</h3>


   
</template>

<script>


export default {
  name: 'Timer',
  props: {
    
  },

  data(){
    return{
      time : "00:01:00",
      timeout : false

    }
  },

  mounted(){
    this.showtimer();
  },

  methods: {

  showtimer: function(){
      
    const timer =  setInterval(()=>{
        
        let time = this.time;
        let t = time.split(":")
        let hour = parseInt(t[0]);
        let min = parseInt(t[1]);
        let sec = parseInt(t[2]);


    //programming logic 
        if(sec == 0){
            if(min >0){
                sec = 59;
                min--;
            }
            else if(hour>0){
                min = 59;
                sec = 59;
                hour--;
            }
            else
                this.timeout = true;
        }
        else
            sec--;

           

        if(hour<10)
            hour = "0" + hour;
        if(min<10)
            min = "0" + min;
        if(sec<10)
            sec = "0" + sec;

        
        time = hour + ":" + min + ":" + sec;

        //color change after timeout and using clearinterval 
        if(this.timeout){
            time = "time Out";
            clearInterval(timer);
        }
        

        this.time = time;

    } , 1000);

    }
   
  }


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h3{
  color: white;
  background-color: green;
  text-align: center;
  padding: 15px;
  width: auto;
  margin-left: 2%;
  float: left;
  margin-right: 30%;
}


        /* mediA query*/
        @media(min-width: 768px){
          h3{
            margin-left: 4%;
            margin-right: 0;
        }
        }
.timeout{
  background-color: #ff0037;
}
</style>

<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn ac">AC</div>
     <div @click="sign" class="btn ac">+/-</div>
      <div @click="percentage" class="btn ac">%</div>
       <div @click="divide" class="btn op">/</div>
        <div @click="append(7)" class="btn">7</div>
         <div @click="append(8)" class="btn">8</div>
          <div @click="append(9)" class="btn">9</div>
           <div  @click="multi" class="btn op">x</div>
            <div @click="append(4)" class="btn">4</div>
             <div @click="append(5)" class="btn">5</div>
              <div @click="append(6)" class="btn">6</div>
               <div @click="sub" class="btn op">-</div>
                <div @click="append(1)" class="btn">1</div>
                 <div @click="append(2)" class="btn">2</div>
                  <div @click="append(3)" class="btn">3</div>
                  <div @click="add" class="btn op">+</div>
                  <div @click="append(0)" class="btn zero">0</div>
                  <div @click="dot" class="btn">.</div>
                  <div @click="equal" class="btn op">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data(){
    return{
      previous:null,
      current: '',
      operator: null,
      operatorclicked:false,
    }

  },
  methods:{
    clear(){
      this.current="";
    },
    sign(){
      this.current=this.current.charAt(0)==='-'?this.current.slice(1):`-${this.current}`
    },
    percentage(){
      this.current=`${parseFloat(this.current)/100}`
    },
    append(number){
      if(this.operatorclicked){
        this.current='';
        this.operatorclicked = false;
      }
      if(this.current === '0'){
      this.current=`${number}`}
      else{
        this.current=`${this.current}${number}`
      }
    },
    dot(){
      if(this.current.indexOf('.')===-1){
        this.append('.')
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorclicked=true;
    },
    divide(){
      this.operator = (a,b) => b/a;
      this.setPrevious();
    },
    multi(){
      this.operator = (a,b) => a*b;
      this.setPrevious();
    },
    sub(){
      this.operator = (a,b) => b-a;
      this.setPrevious();
    },
    add(){
      this.operator = (a,b) => a+b;
      this.setPrevious(); 
    },
    equal(){
      this.current=`${this.operator(parseFloat(this.current),parseFloat(this.previous))}`;
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator
{ 
  margin: 0 auto;
  width:400px;
  font-size:42px;
  display:grid;
  grid-template-columns: repeat(4,1fr);
  grid-template-rows: minmax(50px,auto);
}
.display
{
  grid-column: 1 / 5;
  background-color: yellow;
  border:1px solid black;

}
.zero
{
  grid-column: 1/3;
}
.btn
{
  background-color:white;
  border:1px solid #999;

}
.op
{
  background-color: black;
  color:white
}
.ac
{
  background-color: orange;
  color:white;

}
</style>
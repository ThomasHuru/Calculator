<template>
    <div class = "Calculator" onselectstart='return false'>
        <div class ="displayField">{{ display }}</div>
        <div @click="C" class = "button">C</div>
        <div @click="ans" class = "button">ANS</div>
        <div @click="del" class = "button">DEL</div>
        <div @click="add" class = "button">+</div>
        <div @click="addSymbol(1)" class = "button">1</div>
        <div @click="addSymbol(2)" class = "button">2</div>
        <div @click="addSymbol(3)" class = "button">3</div>
        <div @click="subtract" class = "button">-</div>
        <div @click="addSymbol(4)" class = "button">4</div>
        <div @click="addSymbol(5)" class = "button">5</div>
        <div @click="addSymbol(6)" class = "button">6</div>
        <div @click="multiply" class = "button">x</div>
        <div @click="addSymbol(7)" class = "button">7</div>
        <div @click="addSymbol(8)" class = "button">8</div>
        <div @click="addSymbol(9)" class = "button">9</div>
        <div @click="divide" class = "button">/</div>
        <div class = "button"></div>
        <div @click="addSymbol(0)" class = "button">0</div>
        <div @click="addDecimal" class = "button">,</div>
        <div @click="equal" class = "equal button">=</div>
        <div class = "log"><pre>{{logger}}</pre></div>
        <div @click="changeSymbol" class ="button">+/-</div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      display: 0,
      operator: null,
      operatorClicked: false,
      logger: "",
      ans: 0,
      operatorSymbol: 0,
      decimalAdded: false
    };
  },
  methods: {
      changeSymbol() {
            this.display = this.display - 2*this.display;
      },
      C() {
          this.display = 0;
      },
      ans() {
          this.display = this.ans;
      },
      del() {
          this.display = this.display.substr(0,this.display.length-1);
      },
      add() {
          this.operator = (a,b) => a + b;
          this.previous = this.display;
          this.operatorClicked = true;
          this.operatorSymbol = "+";
      },
      subtract() {
          this.operator = (a,b) => a - b;
          this.previous = this.display;
          this.operatorClicked = true;
          this.operatorSymbol = "-";
      },
      multiply() {
          this.operator = (a,b) => a*b;
          this.previous = this.display;
          this.operatorClicked = true;
          this.operatorSymbol = "*";
      },
      divide() {
          this.operator = (a,b) => b/a;
          this.previous = this.display;
          this.operatorClicked = true;
          this.operatorSymbol = "/";
      },
      equal() {
          this.ans = this.operator(Number(this.display),Number(this.previous));
          this.logger = this.logger +" "+ this.previous+" "+ this.operatorSymbol +" "+ this.display + " = " + this.ans +"\t\n";
          this.display = 0;
          this.operatorClicked = false;
          this.decimalAdded = false;
      },
      addSymbol(number) {
         if (this.operatorClicked === true) {
        this.display = '';
        this.operatorClicked = false;
        this.decimalAdded = false;
      }
      if (this.display === 0){
          this.display = number;
      }
      else{
        this.display = ""+this.display+number;
      }
      },
      addDecimal() {
          if (this.decimalAdded === false){
            this.display = ""+this.display+".";
            this.decimalAdded = true;
          }
      }
  }
};
</script>

<style scoped>
.Calculator {
display:grid;
grid-template-columns: repeat(4, 1fr);
grid-auto-rows: minmax(10v,auto);
width: 80vw;
}
.button {
    cursor: pointer;
}
.displayField {
  grid-column: 1 / 5;
  background: #ddd;
  border: 1px solid #111;
  border-top: 0;
  font-size: 2.5rem;
  cursor: default;
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 1rem;
}
.button {
  background: hsl(0, 0%, 80%);
  background: linear-gradient(15deg,hsl(0, 0%, 70%) 0%, hsl(0, 0%, 80%) 100%);
  border: 1px solid #111;
  cursor: pointer;
}
.log {
  white-space: pre-wrap; 
  word-wrap: break-word;
  font-family: inherit;
}
</style>


                    
        
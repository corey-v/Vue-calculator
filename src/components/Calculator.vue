<template>
    <div class="calcContainer">
        {{calc}}
        <div class="calculator">
            <div class="output">
                <p v-if="output">{{output}}</p>
                <p v-else>0</p>
            </div>
            <button class="btn btn-danger" @click="clear">C</button>
            <button class="btn btn-success" @click="enterOp(4)">/</button>
            <button class="btn btn-success" @click="enterOp(3)">X</button>
            <button class="btn btn-danger" @click="del">DEL</button>
            <br>
            <button class="btn btn-primary" @click="enterNum(7)">7</button>
            <button class="btn btn-primary" @click="enterNum(8)">8</button>
            <button class="btn btn-primary" @click="enterNum(9)">9</button>
            <button class="btn btn-success">-</button>
            <br>
            <button class="btn btn-primary" @click="enterNum(4)">4</button>
            <button class="btn btn-primary" @click="enterNum(5)">5</button>
            <button class="btn btn-primary" @click="enterNum(6)">6</button>
            <button class="btn btn-success" @click="enterOp(1)">+</button>
            <br>
            <button class="btn btn-primary" @click="enterNum(1)">1</button>
            <button class="btn btn-primary" @click="enterNum(2)">2</button>
            <button class="btn btn-primary" @click="enterNum(3)">3</button>
            <button class="btn btn-default">&nbsp;</button>
            <br>
            <button class="btn btn-primary" @click="enterNum(0)">0</button>
            <button class="btn btn-primary" @click="addDecimal">.</button>
            <button class="btn btn-default"> &nbsp;</button>
            <button class="btn btn-success" @click="sum">=</button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      calc: 'Welcome to my calculator project',
      output: '',
      currentNum: 0,
      total: 0,
      prevOp: 0,
      decimalAdded: false
    }
  },
  methods:{
    addDecimal(){
      if (this.decimalAdded == false) {
        if (this.prevOp != 0) {
          this.output = '0.';
        } else {
          this.output += '.';
        }
        this.decimalAdded = true;
      }
    },
    enterNum(val){
        if (this.currentNum == 0) {
        if (this.prevOp == 0)
          this.total = 0;

        if (this.decimalAdded == true) {
          this.currentNum = val / 10;
          this.output += val.toString();
        } else {
          this.currentNum = val;
          this.output = val.toString();
        }
      } else {
        if (this.decimalAdded == true) {
          if (this.currentNum.toString().indexOf('.') == -1) {
            this.currentNum = parseFloat(this.currentNum.toString() + '.' + val.toString());
          } else {
            this.currentNum += val.toString();
            this.currentNum = parseFloat(this.currentNum);
          }
        } else {
          this.currentNum *= 10;
          this.currentNum += val;
        }
        this.output += val.toString();
      }
    },
    enterOp(op){
        if (this.total == 0 && this.currentNum == 0) {
        return;
      }
      if (this.total == 0) {
        this.total += this.currentNum;
      }
      switch (this.prevOp) {
        case 1:
          this.total += this.currentNum;
          break;
        case 2:
          this.total -= this.currentNum;
          break;
        case 3:
          this.total *= this.currentNum;
          break;
        case 4:
          this.total /= this.currentNum;
          break;
        case 0:
          break;
      }

      if (this.decimalAdded == true) {
        this.decimalAdded = false;
      }
      this.currentNum = 0;
      this.prevOp = op;
    },
    clear(){
        this.output = '';
        this.currentNum = 0;
        this.total = 0;
        this.decimalAdded = false;
        this.prevOp = 0;
    },
    sum(){
        switch (this.prevOp) {
        case 1:
          this.total += this.currentNum;
          break;
        case 2:
          this.total -= this.currentNum;
          break;
        case 3:
          this.total *= this.currentNum;
          break;
        case 4:
          this.total /= this.currentNum;
          break;
        case 0:
          break;
      }
      this.output = this.total.toString();
      this.prevOp = 0;
      this.currentNum = 0;
    },
    del(){
        if (this.currentNum > 0) {
        if (this.decimalAdded == false) {
          this.currentNum = parseInt(this.currentNum.toString().slice(0, -1), 10);
        } else {
          this.currentNum = parseFloat(this.currentNum.toString().slice(0, -1));
        }

        if (isNaN(this.currentNum))
          this.currentNum = 0;
        this.output = this.currentNum;
      } else if (this.currentNum == 0) {
        this.output = '';
      }
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calcContainer{
    background: white;
    min-width: 50%;
    max-width: 80%;
    margin: auto;
    border-radius: 5px;
    box-shadow: 2px 2px 2px black;
    padding: 50px 0px;
    margin-bottom: 50px;
}
.calculator{
    min-width: 40%;
    max-width: 60%;
    margin: auto;
    border: 1px solid black; 
}
button{
    margin: 5px auto;
}
</style>

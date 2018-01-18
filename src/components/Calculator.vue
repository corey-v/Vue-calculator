<template>
<div>
    <div class="calcContainer">
		<div class="calculator">
			<div class="output">
                <p v-if="output">{{output}}</p>
                <p v-else>0</p>
            </div>
			<div @click="clear">C</div>
			<div @click="enterOp(4)">/</div>
			<div @click="enterOp(3)">X</div>
			<div @click="del">DEL</div>
			<div @click="enterNum(7)">7</div>
			<div @click="enterNum(8)">8</div>
			<div @click="enterNum(9)">9</div>
			<div @click="enterOp(2)">-</div>
			<div @click="enterNum(4)">4</div>
			<div @click="enterNum(5)">5</div>
			<div @click="enterNum(6)">6</div>
			<div @click="enterOp(1)">+</div>
			<div @click="enterNum(1)">1</div>
			<div @click="enterNum(2)">2</div>
			<div @click="enterNum(3)">3</div>
			<div></div>
			<div></div>
			<div @click="enterNum(0)">0</div>
			<div @click="addDecimal">.</div>
			<div @click="sum">=</div>
		</div>
	</div>
</div>
</template>

<script>
/* eslint-disable */
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

            if (this.decimalAdded) {
                this.currentNum = val / 10;
                this.output += val.toString();
            } else {
                this.currentNum = val;
                this.output = val.toString();
            }
        } else {
            if (this.decimalAdded) {
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
    background: rgba(255,255,255, 0.8);
    min-width: 50%;
    max-width: 60%;
    margin: auto;
    border-radius: 5px;
    box-shadow: 2px 2px 2px black;
    padding: 50px 0px;
    margin-bottom: 50px;
}
.calculator{
    border: 1px solid black;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(40px, auto);
    grid-column-gap: 10px;
    grid-row-gap: 1em;
    min-width: 50%;
    max-width: 70%;
    margin: auto;
    background: linear-gradient(to top, rgba(145, 247, 180, 0.2), rgba(81, 235, 133, 0.4)) no-repeat;
}
.calculator>div{
    border: 1px solid black;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
}
.calculator>div:hover{
    background: lightgreen;
    transition: 0.3s;
}
.output{
    grid-column-start: 1;
    grid-column-end: 5;
}
.output p{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 0px;
    font-weight: bold;
    font-size: 32px;
}
</style>

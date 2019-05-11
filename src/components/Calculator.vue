<template>
    <div class="calculator">
        <div class="display">{{ current || '0' }}</div>
        <div @click="clear" class="btn">C</div>
        <div @click="sign" class="btn">+/-</div>
        <div @click="percent" class="btn">%</div>
        <div @click="divide(current)" class="btn operator">/</div>
        <div @click="append('7')" class="btn">7</div>
        <div @click="append('8')" class="btn">8</div>
        <div @click="append('9')" class="btn">9</div>
        <div @click="multip(current)" class="btn operator">*</div>
        <div @click="append('4')" class="btn">4</div>
        <div @click="append('5')" class="btn">5</div>
        <div @click="append('6')" class="btn">6</div>    
        <div @click="subst(current)" class="btn operator">-</div>
        <div @click="append('1')" class="btn">1</div>
        <div @click="append('2')" class="btn">2</div>
        <div @click="append('3')" class="btn">3</div>
        <div @click="addit(current)" class="btn operator">+</div>
        <div @click="append('0')" class="btn zero">0</div>
        <div @click="dot" class="btn">.</div>
        <div @click="endp(current)" class="btn operator">=</div>
        <div class="displayunder">{{ ucurrent || '0' }}</div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            current: '',
            number1: '',
            number2: '',
            operation: '',
            ucurrent: ''
        }
    },
    methods: {
        clear() {
            this.current = '';
            this.ucurrent = '';
        },
        sign() {
            if(this.current === '' || this.current === '0'){
                this.current = '';
            } else if(this.current.charAt(0) === '-'){
                this.current = this.current.slice(1);
            } else {
                this.current = `-${this.current}`;
            }
            // this.current = this.current.charAt(0) === '-' ? 
               // this.current.slice(1) : `-${this.current}`;
        },
        percent() {
            this.current = `${parseFloat(this.current) / 100}`;
        },
        append(number) {
            if((this.current === '0' && number === '0') || (this.current === '' && number === '0')){
                this.current = '';
            } else {
                this.current = `${this.current}${number}`;
            }
        },
        dot() {
            if(this.current.indexOf('.') === -1) {
                if(this.current === ''){
                    this.current = '0.';
                } else {
                    this.append('.');
                }
            }
        },
        divide(number) {
            this.number1 = number;
            this.operation = '/';
            this.current = '';
            this.ucurrent = number;
        },
        multip(number) {
            this.number1 = number;
            this.operation = '*';
            this.current = '';
            this.ucurrent = number;
        },
        subst(number) {
            this.number1 = number;
            this.operation = '-';
            this.current = '';
            this.ucurrent = number;
        },
        addit(number) {
            this.number1 = number;
            this.operation = '+';
            this.current = '';
            this.ucurrent = number;
        },
        endp(number) {
            if(this.operation === '/'){
                this.current = `${parseFloat(this.number1) / parseFloat(number)}`;
                this.ucurrent = `${this.number1} / ${number}`;
            } else if(this.operation === '*'){
                this.current = `${parseFloat(this.number1) * parseFloat(number)}`;
                this.ucurrent = `${this.number1} * ${number}`;
            } else if(this.operation === '-'){
                this.current = `${parseFloat(this.number1) - parseFloat(number)}`;
                this.ucurrent = `${this.number1} - ${number}`;
            } else if(this.operation === '+'){
                this.current = `${parseFloat(this.number1) + parseFloat(number)}`;
                this.ucurrent = `${this.number1} + ${number}`;
            }
        }
    }
}
</script>

<style scoped>
.calculator{
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
}
.display{
    grid-column: 1 / 5;
    background-color: black;
    color: white;
}
.zero{
    grid-column: 1 / 3;
}
.btn{
    background-color: #f2f2f2;
    border: 1px solid #333;
    cursor: pointer
}
.operator{
    background-color: orange;
}
.displayunder{
    grid-column: 1 / 5;
    background-color: darkgray;
    color: white;
}
</style>
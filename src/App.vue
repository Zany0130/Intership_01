<template>
  <div id="app">
        <div class="calculator">
            <div class="result">
                <input type="text" class="input" v-model="current">
            </div>
            <button @click="changeModeEvent" class="toggle-button">
                changeMode
            </button>
            <div class="mode" v-if="changeMode">
                <button class="button" @click="press">7</button>
                <button class="button" @click="press">8</button>
                <button class="button" @click="press">9</button>
                <button class="button" @click="press">*</button>
                <button class="button" @click="press"><=</button>
                <button class="button" @click="press">C</button>
                <button class="button" @click="press">4</button>
                <button class="button" @click="press">5</button>
                <button class="button" @click="press">6</button>
                <button class="button" @click="press">/</button>
                <button class="button" @click="press">(</button>
                <button class="button" @click="press">)</button>
                <button class="button" @click="press">1</button>
                <button class="button" @click="press">2</button>
                <button class="button" @click="press">3</button>
                <button class="button" @click="press">-</button>
                <button class="button" @click="press">x²</button>
                <button class="button" @click="press">±</button>
                <button class="button" @click="press">0</button>
                <button class="button" @click="press">.</button>
                <button class="button" @click="press">%</button>
                <button class="button" @click="press">+</button>
                <button class="button equal-sign" @click="press">=</button>
            </div> 
            <div class="mode" v-else>
                <button class="button" @click="press">sin</button>
                <button class="button" @click="press">cos</button>
                <button class="button" @click="press">tan</button>
                <button class="button" @click="press">x^</button>
                <button class="button" @click="press"><=</button>
                <button class="button" @click="press">C</button>
                <button class="button" @click="press">log</button>
                <button class="button" @click="press">ln</button>
                <button class="button" @click="press">e</button>
                <button class="button" @click="press">°</button>
                <button class="button" @click="press">rad</button>
                <button class="button" @click="press">√</button>
                <button class="button" @click="press">7</button>
                <button class="button" @click="press">8</button>
                <button class="button" @click="press">9</button>
                <button class="button" @click="press">/</button>
                <button class="button" @click="press">x²</button>
                <button class="button" @click="press">x!</button>
                <button class="button" @click="press">4</button>
                <button class="button" @click="press">5</button>
                <button class="button" @click="press">6</button>
                <button class="button" @click="press">*</button>
                <button class="button" @click="press">(</button>
                <button class="button" @click="press">)</button>
                <button class="button" @click="press">1</button>
                <button class="button" @click="press">2</button>
                <button class="button" @click="press">3</button>
                <button class="button" @click="press">-</button>
                <button class="button" @click="press">%</button>
                <button class="button" @click="press">±</button>
                <button class="button" @click="press">0</button>
                <button class="button" @click="press">.</button>
                <button class="button" @click="press">π</button>
                <button class="button" @click="press">+</button>                    
                <button class="button equal-sign" @click="press">=</button>
              </div>
        </div>

    </div>
</template>

<script>
export default {
  data (){
        return{
            current: '',
            changeMode: true
        }
    },
    methods: {
        press(event) {          
            let key = event.target.textContent;
            const arr = ['=', 'X', 'C', 'x²', '%', '±', '<=', 'sin', 'cos', 'tan',
                           'log', 'ln', 'e', 'x^', '°', '√', 'x!', 'π', 'rad'];
           
            if (arr.includes(key) === false) {
                this.current += key;
            } else {
                switch(key) {
                    case'=':
                        if (this.current.indexOf('^') > -1) {
                            let num1 = this.current.substring(0, this.current.indexOf('^'));
                            let num2 = this.current.substring(this.current.indexOf('^') + 1);
                            this.current = Math.pow(num1, num2);
                        }
                        this.current = eval(this.current);
                        break;
                    case'C':
                        this.current = '';
                        break;
                    case'x²':
                        this.current = this.current * this.current;
                        break;
                    case'%':
                        this.current = this.current/100;
                        break;
                    case'±':
                        if ((this.current).charAt(0) === '-') {
                            this.current = (this.current).slice(1);
                        } else {
                            this.current = '-' + this.current;
                        }
                        break;
                    case"<=":
                        this.current = this.current.substring(0, this.current.length - 1);
                        break;
                    case'sin':
                        this.current = Math.sin(this.current);
                        break;
                    case'cos':  
                        this.current = Math.cos(this.current);
                        break;
                    case'tan':
                        this.current = Math.tan(this.current);
                        break;
                    case'log':
                        this.current = Math.log(this.current);
                        break;
                    case'ln':
                        this.current = Math.log10(this.current);
                        break;
                    case'√':
                        this.current = Math.sqrt(this.current);
                        break;
                    case'π':
                        this.current = this.current * Math.PI;
                        break;
                    case'e':
                        this.current = this.current * Math.exp(this.current);
                        break;
                    case'rad':
                        this.current = this.current * (Math.PI / 180);
                        break;
                    case'°':
                        this.current = this.current * (180 / Math.PI);
                        break;
                    case'x^':
                        this.current += '^';
                        break;
                    case'x!':
                        if (this.current === 0) {
                            return 1;
                        } else if (this.current < 0) {
                            return 'Err';
                        } else {
                            let num = 1;
                            for (let i = 1; i <= this.current; i++) {
                                num *= i;
                            }
                            this.current = num;
                        }
                        break;             
                }
            }  
        },
        changeModeEvent() {
            this.changeMode = !this.changeMode;
        }
    }
}
</script>

<style>
body {
    background: whitesmoke;
  }
  
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    text-align: center;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  
  .calculator {
    width: 440px;
    padding: 20px;
    border-radius: 10px;
    margin: 20px auto;
    font-size: 16px;
    background-color: #e0e0e0;
    box-shadow: 8px 8px 14px #a4a4a4;
  }
  
  .input {
    width: 420px;
    height: 75px;
    border: 1px solid black;
    background-color: #333333;
    color: #d9d9d9;
    padding: 0 5px 0 5px;
    margin: 0 0px 10px 0px;
    font-size: 30px;
  }
  
  .input:focus,
  .input:active {
    border-color: #03a9f4;
    box-shadow: 0 0 4px #03A9F4;
  }
  
  .button {
    margin: 5px;
    width: 60px;
    height: 60px;
    border: 0px;
    border-radius: 50%;
    color: #242323b9;
    cursor: pointer;
    outline: none;
    box-shadow:  8px 8px 14px #a4a4a4,
                -8px -8px 14px #ffffff;
  }

  .button:active {
    transform: translateY(2px)
  }

  .button:hover {
    box-shadow: 14px 14px 14px #a4a4a4,
               -10px -10px 14px #ffffff;
  }
  
  .mode {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
  }
  
  .equal-sign {
    width: 133px;
  }

  .toggle-button {
    margin: 0 0 5px;
  }
</style>

<template>
    <div class="main-page">
        <h1>Random keys</h1>
        <h2>Choose settings</h2>
        <div>
            <Checkbox
                :labelName="'with upper case'"
            />
        </div>
        <div>
            <div class="field_container">
                <input
                    v-model="inputValue" 
                    class="field_input" 
                    type="text"
                    readonly
                />
                <button 
                    class="field_button"
                    @click="copyToClipboard"
                >
                    <img src="@/assets/img/copy-icon.svg" alt="copy"/>
                </button>
            </div>

            <button
                @click="createCode" 
                class="generate_btn"
                >generate
            </button>
        </div>
       
    </div>
</template>

<script>
import Checkbox from './Checkbox.vue';

    export default {
        components: {
            Checkbox
        },
        data() {
            return {
                inputValue: '',
                characters: 3,
                alphabet: ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"],
                numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
                symbols: ['[', '`', '!', '@', '#', '$', '%', '^', '&', '*', '(',  ')', '_', '+', '-', '=', '[', ']', '{', '}', ';',"'", ':', '"', '|', ',', '.', '<', '>', '?', '~', ']']

            }
        },

        computed: {
            // createCode(){
            //     let code = []
                
            //     code.push(this.getSymbols(this.alphabet))
            //     code.push(this.getSymbols(this.numbers))
            //     code.push(this.getSymbols(this.symbols))
            //     code = code.flat(2)

            //     return code.join('')
            // }
        },

        methods: {

            
            getRandom(element){
                let random = Math.floor(Math.random() * element.length)

                return random
            },
            getSymbols(symbols){
                let poolOfSymbols = []
                for(let i = 0; i < this.characters; i++) {
                    poolOfSymbols.push(symbols[this.getRandom(symbols)])
                }
                // indexes.push(this.alphabet[this.getRandom(this.alphabet)])
                
                return poolOfSymbols
            },

            createCode(){
                let code = []
                
                code.push(this.getSymbols(this.alphabet))
                code.push(this.getSymbols(this.numbers))
                code.push(this.getSymbols(this.symbols))
                code = code.flat(2)
                console.log('code', code)
                this.inputValue = code.join('')
            },

            copyToClipboard(){
                if(this.inputValue !== '') {
                    navigator.clipboard.writeText(this.inputValue)
                }
            }
        },

        mounted(){
            console.log(navigator)
            // this.getRandom(this.alphabet)
            // console.log(this.createCode())
        }
    }
</script>

<style lang="scss" scoped>
    .main-page {
        max-width: 400px;
        width: 100%;
        margin: 0 auto;
    }
    .field {
        &_container {
            position: relative;
            max-width: 100%;
        }
        &_input {
            height: 40px;
            box-sizing: border-box;
            width: 100%;
            outline: none;
            font-size: 28px;

        }
        &_button {
            position: absolute;
            top: 0;
            right: 0;
            cursor: pointer;
            height: 40px;
            width: 40px;
            padding: 0;
            & > img {
                width: 20px;
                height: 20px;

            }
        }
    }

    .generate_btn {
        margin-top: 50px;
        padding: 3px 10px;
        height: 40px;
        max-width: 100px;
        width: 100%;
        cursor: pointer;
    }
</style>
<template>
    <div>
        <div class="function">antilogicWaves
            ( input: <input type="text" id="in" size="3" class="input" v-model="inputValue" @keyup="runWaves()"> )
        </div>
        <div class="parentesis">
            <span v-for="element in results" :key="element.result" :style="element.style">) </span>
        </div>        
        <div class="imgContainer">
            <div class="output" v-if="results.length > 0">
            <div>Outputs</div>
            <span v-for="element in results" :key="element.result">{{ element.result }}, </span>
        </div>
            <img src="../assets/antilogicWavesFunction.png" class="img">
        </div>
    </div>
</template>

<script>
export default {
    name: 'AntilogicWavesRecursiveFunction',
    data: function() {
        return {
            inputValue: '',
            results: []
        }
    },
    created: function() {
        window.onload = () => {
            document.getElementById('in').focus()
        }
    },
    methods: {
        runWaves: function() {
            if(isNaN(parseInt(this.inputValue)) || parseInt(this.inputValue) < 1)
                return
            this.inputValue = parseInt(this.inputValue)
            this.results    = []
            for(let i=1; i<=this.inputValue; i++) {
                let result = this.antilogicWaves(i)
                let style  = {
                    color         : 'aqua',
                    'font-family' : 'Verdana, Geneva, Tahoma, sans-serif',
                    'font-size'   : result + 'px',
                    position      : 'relative',
                    left          : (result - i) + 'px',
                    top           : 0 + 'px',
                    transition    : 'left 1s, top 1s'
                }
                this.results.push({ result, style })
                setInterval(() => {
                    style.left = (Math.floor(Math.random() * (i/2)) + 1) + 'px'
                    style.top  = (Math.floor(Math.random() * i) + 1) + 'px'
                }, 500)
            }
        },
        antilogicWaves: function(input) {
            if(input == 0)
                return 0
            return input + this.antilogicWaves(input - 1)
        }
    }
}
</script>

<style scoped>
    .imgContainer {
        display: flex;
        justify-content: flex-end;
    }
    .img {
        border: solid 5px lime;
        border-radius: 50px;
        position: absolute;
        bottom: 50px;
    }
    .input {
        font-size: 25px;
        font-family: 'Stalinist One', cursive;
        background-color: black;
        color: lime;
        border-radius: 10px;
    }
    .parentesis {
        border-bottom: solid 1px yellow;
        padding-bottom: 55px;
    }
    .function {
        font-size: 20px;
        font-family: 'Stalinist One', cursive;
    }

    .output  {
        font-size: 20px;
        font-family: 'Stalinist One', cursive;
        margin-top: 15px;
    }
</style>
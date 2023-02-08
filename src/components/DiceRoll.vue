<template>
    <div>
        <p><strong>Number of Dices:</strong> 
        <select v-model="numDices"> 
            <option v-for="(n, index) in 10" :value="n" :key="index">{{ n }}</option>
        </select>
        |
        <strong>Number of Faces:</strong>
        <select>
            <option>6</option>
            <option>10</option>
            <option>12</option>
            <option>20</option>
        </select>
        |
        <button @click="rollDices">Roll Dices</button>
        |
        <strong>Result:</strong> {{ result }}</p>
    </div>
    <br>
    <br>
</template>

<script>
    export default {
        data() {
            return {
                numDices: 1,
                numFaces: 6,
                result: 0
            };
        },
        methods: {
            rollDices() {
                this.result = [];
                for (let i = 0; i < this.numDices; i++) {
                    this.result.push(Math.floor(Math.random() * this.numFaces) + 1);
                }
            }
        }
    };
</script>
    
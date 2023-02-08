<template>
    <h1>Abandon all hope, ye who enter here</h1>
    <p>... to succeed at your dice rolls ! </p>
    <p>Welcome to this combat sheet to keep track of everyone's turn and stats</p>
    <form @submit.prevent="addFighter">
        <input v-model="initiative" placeholder="Fighter initiative">
        <input v-model="newFighter" placeholder="Fighter Name">
        <input v-model="maxHealth" placeholder="Fighter Max Health">    
        <button>Add Fighter</button> <br>
    </form>
    <ul>
        <li v-for="fighter in sortedFighters" :key="fighter.id">
            <input type="checkbox" v-model="fighter.played">
            <span :class="{ played: fighter.played}"><strong>Initiative</strong>: {{fighter.initiative}} | <strong>Name</strong>: {{fighter.name}} | <strong>Health</strong>: <input type="number" v-model="fighter.currentHealth" @input="updateHealth(index,$event.target.value)"> / {{fighter.maxHealth}} HP</span>
            
            <button @click="removeFighter(fighter)">X</button>

            <DiceRoll />
        </li>
    </ul>

</template>

<style>

.played{
    text-decoration: line-through;
}

</style>

<script>
let id = 0

import DiceRoll from './DiceRoll.vue';

export default{
    components: {
        DiceRoll
    },
    name: 'PresentationCombat',
    data(){
        return {
            fighters: [
                {
                    id: id++,
                    name: 'Player 1',
                    maxHealth: 50,
                    currentHealth: 50,
                    initiative: 5,
                    played: true
                },
                {
                    id: id++,
                    name: 'Monster 1',
                    maxHealth: 25,
                    currentHealth: 18,
                    initiative: 1,
                    played: false
                }
            ]
        }
    },
    methods: {
        onInput(e){
            this.name = e.target.value
        },
        addFighter(){
            this.fighters.push({
                id: id++,
                name: this.newFighter,
                maxHealth: this.maxHealth,
                currentHealth: this.maxHealth,
                initiative: this.initiative,
                played: false
            })
            this.newFighter = ''
        },
        removeFighter(fighter){
            this.fighters = this.fighters.filter((f) => f !== fighter)
        },
        updateHealth(index, value) {
        this.fighters[index].health = value
        },
        sortInitiative() {
            this.fighters.sort((a,b) => {
                return b.priority - a.priority
            })
        }
    },
    computed: {
        sortedFighters() {
            return [...this.fighters].sort((a, b) => b.initiative - a.initiative)
        }
    }
}

</script>
<template>
    <h1 v-if="!pokemon">Espere por favor...</h1>
    <div v-else>
        <h1>¿Quién es este Pokemón 🤔?</h1>
        <PokemonPicture
            :pokemonId="pokemon.id" 
            :showPokemon="showPokemon" 
        />
        <PokemonOptions
            :pokemons="pokemonArr" 
            @selection-pokemon="checkAnswer($event)"
        />
        <template v-if="showAnswer">
            <h2  :class="{ ok : correct , no : !correct }">{{ message }}</h2>
            <button 
                class="btn-new"
                @click="newGame">
                Siguiente pokemon
            </button>
        </template>
    </div>
</template>

<script>

import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'

import getPokemonOptions from '@/helpers/getPokemonOptions'

export default {
    components:{
        PokemonPicture,
        PokemonOptions
    },
    data(){
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: '',
            correct: false
        }
    },
    methods: {
        async mixPokemonArray(){
            this.pokemonArr = await getPokemonOptions()

            const rndInt = Math.floor( Math.random() * 4 )
            this.pokemon = this.pokemonArr[ rndInt ]

        },
        //obtenido de PokemonsOptions Page
        checkAnswer( selectedId ){
            this.showPokemon = true
            this.showAnswer = true

            if( selectedId === this.pokemon.id){
                this.message = `Correcto, es ${ this.pokemon.name } ✅`
                this.correct = true
            }else{
                this.message = `Ops..., era ${ this.pokemon.name } ❌`
                this.correct = false
            }
        },
        newGame(){
            this.pokemonArr = []
            this.showPokemon = false
            this.showAnswer = false
            this.pokemon = null
            this.mixPokemonArray()
        }
    },
    mounted(){
        this.mixPokemonArray()
    }
};
</script>

<style scoped>
.btn-new{
    border: none;
    background: #4eff89;
    height: 50px;
    border-radius: 10px;
    padding: 10px;
}
.btn-new:hover{
    border: black solid 1px;
    background: #4eff89;
}

.ok{
    color: #41de3b
}

.no{
    color: rgb(184, 28, 28);
}

</style>
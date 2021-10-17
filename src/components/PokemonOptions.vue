<template>
    <div class="options-container">
        <ul>
            <li v-for="pokemon in pokemons" 
                :key="pokemon.id"
                @click="$emit( 'selectionPokemon', pokemon.id )">
                {{ pokemon.name }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props:{
        pokemons: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
/* Pokemon Options */
ul {
    list-style-type: none;
}
li {
    padding-top: 5px;
    background-color: white;
    border-radius: 5px;
    cursor: pointer;
    margin-bottom: 10px;
    width: 250px;
    height: 30px;
}

li:hover {
    background-color: rgba(48, 158, 21, 0.411);
}

.options-container {
    display: flex;
    justify-content: center;
}
</style>
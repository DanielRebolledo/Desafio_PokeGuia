<template>
  <div class="App">
    <main>
      <section class="header">
          <img src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/i/87044f58-c765-43c5-bc51-8613e3ac7ab1/ddew4m7-c69a2c41-518f-48ca-ba35-8ab1895464e0.png" alt="" class="logo">
      </section>

      <section class="pokemon-foto">
        <img :src="pokemonFrontDefault" alt="">
      </section>
      
      <section class="search">
        <h4>PokeGuia</h4>
        <form class="input-search" @submit.prevent="findPokemon">
          <p>Nombre:</p>
          <input type="text" placeholder="Buscar" v-model="pokemonName" required/>
          <button type="submit" class="buscar-btn">Buscar</button>
        </form>
      </section>

      <section class="Habilidades">
        <h4>Habilidades</h4>
        <ul v-if="pokemon" class="lista">
          <li v-for="(ability, $index) of pokemonAbilities"
          :key="$index">
            {{ ability }}
          </li>
        </ul>
      </section>

      <section class="movements">
        <h4>Movimientos</h4>
        <ul v-if="pokemon" class="lista">
          <li 
            v-for="(move, $index) of pokemonMoves" 
            :key="$index">
            {{ move }}
          </li>
        </ul>
      </section>

    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: () => ({
    pokemon: {},
    pokemonName: '',

    Created(){
    
    }
  }),
  computed: {
    pokemonMoves(){
      return this.pokemon && this.pokemon.moves && this.pokemon.moves.map((move) => move.move.name)
    },
    pokemonAbilities(){
      return this.pokemon && this.pokemon.abilities && this.pokemon.abilities.map((ability) => ability.ability.name)
    },
    pokemonFrontDefault(){
      return this.pokemon?.sprites?.front_default ?? ''
    },
  },
  methods: {
      async findPokemon(){
        const pokemon = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemonName}`)
        .then((response) => response.json())
        this.pokemon = pokemon
        
      }
  }


}
</script>

<style>
  body{
    font-family: Arial, Helvetica, sans-serif;
    width: 100%;
    height: 100vh;
    margin: 0;
    padding: 0;
    background-color: #ffda27;
  }
  main{ 
    max-width: 400px; 
    margin: 100px auto; 
    background-color: #fff;
    border-radius: 25px;
    text-align: center;
    padding-bottom: 15px;
    box-shadow: -2px 5px 27px -1px #CAAC1F;
  }
  .pokemon-foto{ 
      text-align: center;
  }
  .pokemon-foto > img{ 
      width: 200px;
  }
  .header{
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .logo{
    width: 80%;
  }
  .search{ 
    text-align: center;
  }
  .buscar-btn{ 
    display: block;
    border-radius: 5px;
    padding: 10px 30px;
    color: #fff;
    background-color: #316ab1;
    border: none;
    margin:  20px auto;
    transition: all ease-in 0.2s;
  }
  .buscar-btn:hover{ 
    background-color: #ffda27;
    font-size: 15px;
  }
  .lista{ 
    text-align: left;
    list-style: decimal;
  }
  
</style>

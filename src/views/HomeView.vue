<template>
  <NavBar/>
  <MusicSquares 
    artist1="coldplay"
    artist2="dayglow"
    artist3="daft_punk"
    artist4="the_strokes"
    artist5="twenty_one_pilots"
    artist6="arctic_monkeys"
  />
  <MusicSquares 
    artist1="ariana_grande"
    artist2="harry_styles"
    artist3="camila_cabello"
    artist4="calle_13"
    artist5="dua_lipa"
    artist6="bts"
  />
  <MusicSquares 
    artist1="black_pink"
    artist2="twice"
    artist3="lana_del_rey"
    artist4="AJR"
    artist5="shawn_mendes"
    artist6="britney_spears"
  />
  
</template>

<script>
import NavBar from '../components/NavBar.vue'
import MusicSquares from '../components/MusicSquares.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    MusicSquares
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}
body {
 background-color:#EAEBEB; 
}
</style>

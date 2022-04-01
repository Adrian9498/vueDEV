<template>
    <div id="NavBarT" class="navigation">
        <nav class="navbar">
        <div class="navbar-container container">
            <input type="checkbox" name="" id="">
            <div class="hamburger-lines">
                <span class="line line1"></span>
                <span class="line line2"></span>
                <span class="line line3"></span>
            </div>
            <ul class="menu-items">
                <li><router-link to="/">Home</router-link></li>
            </ul>
            <h1 class="logo">MusicBox</h1>
        </div>
    </nav>
    </div>
</template>

<script>
    export default{
        name: 'NavBar',
        data(){
            return{
                subtitulo: 'Soy el subtitulo de mi componente'
            }
        }
    }
</script>

<style scoped>
    @import '../assets/css/navbar.css';
</style>
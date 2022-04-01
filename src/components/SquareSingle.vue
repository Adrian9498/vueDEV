<template>
    <transition name="fade" appear>
        <div class="square" :style="cssProps">
            <p class = "nombre">{{artist}}</p>
            <br>
            <p class = "nombre">{{style}}</p>
            <br>
            <router-link class="Rlink" :to="{ name: 'about', params: {artist:this.artist, reqUrl: this.reqUrl } }">Mas informacion</router-link>
        </div>  
    </transition>
    
</template>

<script>
    export default{
        name: 'SquareSingle',
        props: {
            img: String,
            reqUrl: String,
            artist: String,
            style: String
        },
        computed:{
            cssProps(){
                return{
                    '--bg-image': this.img
                }
            }
        }
    }
</script>

<style scoped>
    .square{
        height: 25vh;
        width: 25vh;
        margin-left: 3vw;
        background-color: #FFDDC4;
        background-image: var(--bg-image);
        background-size: contain;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-shadow: 5px 5px 5px black;
    }

    .nombre{
        font-size: 1vw;
        opacity: 1;
        z-index: -1;

    }

    .Rlink{
        color: #BF92B4;
        font-size: 1.2vw;
        z-index: -1;
        text-decoration: none;
    }
    .square:hover{
        background-image: none;
        z-index: 2;
    }

    
</style>
<template>
    
        <div class="square" :style="cssProps">
            <p class = "nombre">{{artist}}</p>
            <br>
            <p class = "nombre">{{style}}</p>
            <br>
            <router-link class="Rlink" :to="{ name: 'about', params: {artist:this.artist, reqUrl: this.reqUrl } }">Mas informacion</router-link>
        </div>  
   
    
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
        background-color: #591C0E;
        background-image: var(--bg-image);
        background-size: cover;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-shadow: 5px 5px 5px black;
        transition: background-color 0.5s ease-in;
        
    }

    .nombre{
        font-size: 1vw;
        opacity: 1;
        z-index: -1;
        color: #F2E5D5;
        font-weight: bold;
    }

    .Rlink{
        color: #591C0E;
        font-size: 1.2vw;
        z-index: -1;
        text-decoration: none;
        
    }
    .square:hover{
        background-image: none;
        background-color: #BF9A78;
        z-index: 2;
        
    }
    

    @media (max-width: 1200px) {
        .square {
            margin-top: 2vh;
        }
        .nombre{
            font-size: 2.5vh;
            opacity: 1;
            z-index: -1;
            
        }

        .Rlink{
            
            font-size: 2vh;
            z-index: -1;
            text-decoration: none;
        }
    }

    @media (max-width: 600px) {
        .square {
            margin-top: 2vh;
        }
    }

    
</style>
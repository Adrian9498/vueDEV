<template>
    <div class="MusicSquares">
        <SquareSingle :img="imgThumb[0]" :artist="artists[0]" :reqUrl= "reqUrl[0]" :style="style[0]"/>
        <SquareSingle :img="imgThumb[1]" :artist="artists[1]" :reqUrl= "reqUrl[1]" :style="style[1]"/>
        <SquareSingle :img="imgThumb[2]" :artist="artists[2]" :reqUrl= "reqUrl[2]" :style="style[2]"/>
        <SquareSingle :img="imgThumb[3]" :artist="artists[3]" :reqUrl= "reqUrl[3]" :style="style[3]"/>
        <SquareSingle :img="imgThumb[4]" :artist="artists[4]" :reqUrl= "reqUrl[4]" :style="style[4]"/>
        <SquareSingle :img="imgThumb[5]" :artist="artists[5]" :reqUrl= "reqUrl[5]" :style="style[5]"/>
    </div>
</template>

<script>
    
    import SquareSingle from './SquareSingle.vue'
    import axios from 'axios'
    export default{
        name: 'MusicSquares',
        props:{
            artist1: String,
            artist2: String,
            artist3: String,
            artist4: String,
            artist5: String,
            artist6: String
        },
        data (){
            return{
                imgThumb: [],
                reqUrl: [],
                artists: [],
                style:[]
            }
        },
        methods: {
            getImages: function (url){
                axios
                .get("https://www.theaudiodb.com/api/v1/json/2/search.php?s="+url)
                .then((response)=>{
                    
                    this.imgThumb.push('url('+response.data.artists[0].strArtistThumb+')');
                    this.artists.push(response.data.artists[0].strArtist);
                    this.style.push(response.data.artists[0].strStyle)
                    this.reqUrl.push(url);
                    
                })
                .catch((error)=>{
                    console.log(error.message)
                })
            }

        },
        created(){
            this.getImages(this.artist1);
            this.getImages(this.artist2);
            this.getImages(this.artist3);
            this.getImages(this.artist4);
            this.getImages(this.artist5);
            this.getImages(this.artist6);

        },
        components: {
            SquareSingle
        }
    }
</script>

<style scoped>
    .MusicSquares{
        display: flex;
        margin-top:3vh;
        margin-left: 2vw;
    }

    @media (max-width: 600px) {
        .MusicSquares {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
    }

    @media (max-width: 1200px) {
        .MusicSquares {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            align-items: center;
        }
    }
</style>
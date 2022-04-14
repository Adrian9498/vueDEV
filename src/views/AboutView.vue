<template>
  <NavBar />
  <div class="about">
    <div class="gralinfo">
      <p>{{ artist }}</p>
      <br />
      <img :src="this.img" class="img-artist" />
      <br />
      <p>Style: {{ this.style }}</p>
      <br />
      <p>Year: {{ this.anio }}</p>
      <br />
      <p>Mood: {{ this.mood }}</p>
      <br />
      <p>ID: {{ this.artistid }}</p>
    </div>
    <div class="extrainfo">
      <div class="album" v-for="album in albums" :key="album.strAlbum">
        <!--<p>{{ album.strAlbum }}</p>
        <p>{{ artist }}</p>
        <p>{{ album.intYearReleased }}</p>-->
        <img :src="album.strAlbumThumb" class="img-album" />
        <p>{{ album.strAlbum }}</p>
        <p>{{ album.intYearReleased }}</p>
        
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from "../components/NavBar.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    NavBar,
  },
  props: {
    artist: String,
    reqUrl: String,
  },
  data() {
    return {
      bio: "",
      img: "",
      style: "",
      anio: "",
      mood: "",
      artistid: "",
      albums: [],
    };
  },
  methods: {
    getImages: function (url) {
      axios
        .get("https://www.theaudiodb.com/api/v1/json/2/search.php?s=" + url)
        .then((response) => {
          this.bio = response.data.artists[0].strBiographyEN;
          this.img = response.data.artists[0].strArtistThumb;
          this.style = response.data.artists[0].strStyle;
          this.anio = response.data.artists[0].intFormedYear;
          this.mood = response.data.artists[0].strMood;
          this.artistid = response.data.artists[0].idArtist;
          axios
            .get(
              "https://theaudiodb.com/api/v1/json/2/album.php?i=" +
                this.artistid
            )
            .then((response) => {
              this.albums = response.data.album;
            })
            .catch((error) => {
              console.log(error.message);
            });
        })
        .catch((error) => {
          console.log(error.message);
        });
    },
  },
  created() {
    this.getImages(this.reqUrl);
  },
};
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
  background-color: #eaebeb;
}

.about {
  height: 92vh;
  width: 100%;
  display: flex;
  background-color: #f2e5d5;
}
.gralinfo {
  height: 100%;
  width: 30%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 3vh;
  color: #282828;
  border: 5px solid #bf9a78;
  transition: border 0.5s ease-in;
  margin-right: 2px;
}

.gralinfo:hover {
  border: 5px solid greenyellow;
}

.extrainfo {
  height: 100%;
  width: 80vw;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 20px;
  overflow: auto;
  border: 5px solid #bf9a78;
  transition: border 0.5s ease-in;
}

.extrainfo:hover {
  border: 5px solid greenyellow;
}

.img-artist {
  height: 20vh;
  width: 20vh;
  border-radius: 10px;
}

.img-album {
  margin: 2vh;
  height: 30vh;
  width: 30vh;
}

.album {
  display: flex;
  flex-direction: column;
  align-items: center;
}


@media (max-width: 1000px) {
  .about {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .gralinfo {
    margin-top: 10px;
    height: 50vh;
    width: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-size: 2vh;
    color: #282828;
  }
  .extrainfo {
    height: 50%;
    width: 95%;
    margin-top: 10px;
    display: flex;
    flex-direction: row;
    margin-bottom: 10px;
    
  }
}
</style>

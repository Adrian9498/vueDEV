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
          <p>{{ album.strAlbum }}</p>
          <p>{{ artist }}</p>
          <p>{{ album.intYearReleased }}</p>
          <img :src="album.strAlbumThumb" class="img-artist" />
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
      albums: []
    };
  },
  methods: {
    getImages:  function (url) {
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
            .get("https://theaudiodb.com/api/v1/json/2/album.php?i=" + this.artistid)
            .then((response) => {
              this.albums = response.data.album
              
            })
            .catch((error) => {
              console.log(error.message);
            });
        })
        .catch((error) => {
          console.log(error.message);
        });
    }
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
  height: 90vh;
  width: 100vw;
  display: flex;
}
.gralinfo {
  height: 90vh;
  width: 20vw;
  background-color: #bf92b4;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 3vh;
  color: #eaebeb;
  border: 1px solid #fff;
}

.extrainfo {
  height: 90vh;
  width: 80vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #eecda3; 
  background: -webkit-linear-gradient(
    to left,
    #eecda3,
    #ef629f
  );
  background: linear-gradient(to left, #eecda3, #ef629f);
  border: 1px solid #fff;
  padding: 20px;
  overflow: auto;
}

.img-artist {
  height: 30%;
  width: 60%;
  border-radius: 100px;
}

.album {
  display:flex;
  flex-direction: row;
  height: 100%;
  width: 100%;
  align-items: self-start;
  justify-content: space-between;
}

.album img {

  height: 70px;
  width: 70px;
}
</style>

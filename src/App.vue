<template>
  <div id="app">
    <!--<div id="nav">
       <img class="logo" alt="Vue logo" src="assets/logo.png" />
      <router-link to="/">Home</router-link> |
      <router-link to="/portofolio">Portofolio</router-link> |
      <router-link to="/service">Service</router-link> |
      <router-link to="/about">Aboffut</router-link>
    </div>
    <router-view /> -->
    <div class="my-all">
      <header>
        <h1>My Music Apps</h1>
        <counter></counter>
      </header> 
      
      <!-- the App content-->
      <main>
        <!-- START PLAY LIST -->
        <section class="playList container">
          <div class="row">
            <div class="clo-6">
              <h3>Play list</h3>
            <ol>
              <li class="list" v-for="song in songs" :key="song.src" @click="play(song)" :class="song.src == current.src ? 'Song Playing' : 'song'">  
              <a>{{song.title}} - {{song.artist}}</a>
              </li>
            </ol> 
            <input type="file" placeholder="Add a song" value="add" >
            </div>

             <!--Artist details-->
            <div class="col-6">
                <h4 class="song-title">{{current.title}}- <span>{{current.artist}}</span></h4>
            </div>
            <!--END ARTIST DETAILS-->
          </div>
        </section>
      <!-- eND PLAY LIST-->
      <!--Artist details-->
        <section class="artist-detail">
          <h3 class="song-title">{{current.title}}- <span>{{current.artist}}</span></h3>
        </section>
      <!--END ARTIST DETAILS-->
      <div class="song-time"><h2>{{ duration }}</h2>
        {{displaySeconds}}
        {{tim}}
      </div>
      <!-- start Control-->
        <section class="control">
          <a class="control-btn prev" @click="prev"><img src="./assets/icons/prev.png"></a>
          <a class="control-btn play" v-if="!isPlaying" @click="play"><img src="./assets/icons/play.png"></a>
          <a class="control-btn pause" v-else @click="pause"><img src="./assets/icons/pause.png"></a>
          <a class="control-btn next" @click="next"><img src="./assets/icons/next.png"></a>
        </section>
        
        <!-- END CONTROL-->
      </main>
    </div>
    <john
    :year="2020"
    :month="8"
    :date="23"
    :hour="20"
    :minute="20"
    :second="20"
    :millisecond="20"/>
   </div>
</template>
<script>
import john from "./components/john.vue";
import counter from "./components/counter.vue"
export default {
  name : 'app',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      displaySeconds:0,
      duration: 0,
      tim: 0,
      songs: [
        {
          title : 'Silence',
          artist: 'Pompi',
          src: require('./assets/silence.mp3')
        },
        {
          title : 'Second Song',
          artist : 'Jay',
          src: require('./assets/Packaging.mp3')
        },
        {
          title : 'Musician',
          artist : 'Jay',
          src: require('./assets/Refuge.mp3')
        },
        {
          title : 'Her love',
          artist : 'Jay',
          src: require('./assets/her.mp3')
        },
         {
          title : 'the lover',
          artist: 'John',
          src: require('./assets/love.mp3')
        }
      ],
      player: new Audio()
    }
  },
  components: {
    john,
    counter
  },
  computed: {
    _seconds: () => 1000,
    _minutes(){
    return this._seconds * 60
    },
    _hours(){
      return this._minutes *60
    }
  },
  methods: {  
    showRemaining(){
            
          }, 
    play (song) {
      
     
     // const minutes = Math.floor((count % this._hours) / this._minutes);
     // const second = Math.floor((this.duration % this._minutes) / this._seconds);
       // this.duration = minutes < 10 ? "0" + minutes : minutes;

      if(typeof song.src !="undefined"){
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener('ended', function(){
         this.index++;
        if(this.index > this.songs.length - 1){
          this.index = 0
        }
        this.current = this.songs[this.index];
        this.play(this.current)
      }.bind(this)),
      this.isPlaying = true,

      setTimeout(function() {
        this.duration = 1;
      },3000);
      
      /*  const timer = setInterval(() =>{
          const now = new Date();
          const total = now.getSeconds();
          now.setSeconds(40);
          // const temp = now.getSeconds();
          //let time = total - temp;
          if(total < 60){
            for(var i = 0; i < 60; i++){
              var real = i;
            }
          }
          let value = real;

            if(this.isPlaying == true){
              if(total < 0){
                clearInterval(timer);
                  return;
              }
            } else{
            clearInterval(timer)
            }
          this.tim = value;
          this.duration = total; */
          //this.displaySeconds = temp 
        //   })      
    },
    pause () {
      this.player.pause();
      this.isPlaying = false
    },
    prev () {
      this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    },
    next () {
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    
  }
}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.my-all{
  background: #240303;
  width: 75%;
  margin: auto;
  padding-bottom: 50px;
  border-radius: 50px;
  color: #fff;
  header{
  background-color: none;
  }
  //contol buttons
  .control{
    border-radius: 0 0px 50px 50px;
    .control-btn{
      background-color: transparent;
      color: #fff;
      margin: 5px;
      padding: 15px 10px 15px 10px;
        
    }
    img{
      width: 1.5rem;
    }
    .next{
     
    }
    .prev{
     
    }
    .pause{
     
    }
    .play{
     
    }
  }
  // END contol buttons
}

a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
}

.playList{
  background-color: rgb(56, 15, 18);
  display: block;
  width: 90%;
  margin: auto;
  text-align: left;
  h3{
    padding: 5px;
    font-size: 28px;
    background-color: #1c1c1c;
  }
  .list{
  display: block;
  }
}
.artist-detail{
  background: rgb(97, 4, 4);
  width: 30%;
}
.song-time{
  background: rgb(88, 9, 22);
  margin-bottom: 15px;
}
</style>

<template>
    <div id="app">
        <header class="header">
            <h4>Muzzika</h4>
        </header>
        <main>
            <section class="player">
                <h2 class="song-title">{{ current.title }} - <span> {{ current.artist }}</span>
                </h2>
                <div class="controls">
                    <!-- these buttons will display on the main page, and they are the main buttons to control the songs. -->
                    <button class="prev" @click="prev">Prev</button>
                    <button class="play" v-if="!isPlayying" @click="play">Play</button>
                    <button class="pause" v-else @click="pause">Pause</button>
                    <button class="next" @click="next">Next</button>
                </div>
            </section>
        <!-- this section is for the buttons next and prev -->
        <section class="playlist">
            <h3>Trading Yestarday Playlist</h3>
            <!-- create a v-for to loop through all the buttons from the amount of songs i have -->
            <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing'
            :'song'">
            {{song.title}} - {{song.artist}}

            </button>

        </section>
        </main>    
    
  
    </div>
</template>

<script>
export default {
    name: 'app',
    data() {
        return {
            current: {},
            index: 0,
            isPlayying: false,
            songs: [
                 {
                   title: 'Whats up',
                   artist: '4 Non Blondes',
                   src: require('./assets/4-nonblondes-whatsup.mp3')
                 },
                 {
                   title: 'Ana Ayesh',
                   artist: 'Amro Diab',
                   src: require('./assets/amrodiab-anaayesh.mp3')
                 },
                 {
                   title: 'Rise',
                   artist: 'Ashes Remain',
                   src: require('./assets/ashesremain-rise.mp3')
                 },
                 {
                   title: '99',
                   artist: 'Barns Courtney',
                   src: require('./assets/barnscourtney-99.mp3')
                 },
                 {
                   title: 'Came Here to Forget',
                   artist: 'Blake Shelton',
                   src: require('./assets/blakeshelton-camehere-to-forget.mp3')
                 },
                 {
                   title: 'No Body But You',
                   artist: 'Blake Shelton',
                   src: require('./assets/blakeshelton-nobodybutyou.mp3')
                 },
                 {
                   title: "Pin the Grenade",
                   artist: 'Blink',
                   src: require('./assets/blink-182-pin-the-grenade.mp3')
                 },
                 {
                   title: 'Heaven',
                   artist: 'Bryan Adams',
                   src: require('./assets/bryan-adams-heaven.mp3')
                 },
                 {
                   title: 'Believe',
                   artist: 'Cher',
                   src: require('./assets/cher-believe.mp3')
                 },
                 {
                   title: 'Beautiful People',
                   artist: 'Ed Sheeran',
                   src: require('./assets/ed-sheeran-beautiful-people-feat.khalid.mp3')
                 },
                 {
                   title: 'God Only Knows',
                   artist: 'King & Country',
                   src: require('./assets/for-king&country-burn-the-ships.mp3')
                 },
                 {
                   title: 'Hurricane',
                   artist: 'Galantis & John Newman',
                   src: require('./assets/galantis&john-newman-hurricane.mp3')
                 },
                 {
                   title: 'Welcome To The Jungle',
                   artist: "Guns N Roses",
                   src: require('./assets/gunsnroses-welcometothe-jungle.mp3')
                 },
                 {
                   title: 'I will Be There',
                   artist: 'Jess Glynne',
                   src: require('./assets/jess-glynne-Illbethere.mp3')
                 },
                 {
                   title: 'Memories',
                   artist: 'Maroon 5',
                   src: require('./assets/maroon5-memories.mp3')
                 },
                 {
                   title: 'In The Air',
                   artist: 'Morgan Page',
                   src: require('./assets/morgan-page-sultan-ned-shep-intheair.mp3')
                 },
                 {
                   title: 'Roses',
                   artist: 'Imanbek Remix',
                   src: require('./assets/rosesImanbek.mp3')
                 },
                 {
                   title: 'Hard To Forget',
                   artist: 'Sam Hunt',
                   src: require('./assets/sam-hunt-hard-to-forget.mp3')
                 },
            ],

            player: new Audio()
        }
    },
    methods: {
        play(song) {
            if(typeof song.src !="undefined") {
            this.current =song;
            this.player.src = this.current.src;
        }
        this.player.play();
        this.isPlayying = true;
        // this.player.play();

        // // the function below is when the song ends, it auto goes to the next song.
        // this.player.addEventListener('ended', function (){
        //     this.index++;
        //      if(this.index > this.songs.length - 1){
        //         this.index = 0;
        //     }
        //     this.current = this.songs[this.index];
        //     this.play(this.current);
        // }.bind(this));
        // this.isPlayying = true;
    // },
    },
        pause(){
            this.player.pause();
            this.isPlayying = false;
        },
        next(){ 
            this.index++;
            // if we are at the last song, this will move it back to the start of the list
            if(this.index > this.songs.length-1){
                this.index=1;
            }
            this.current = this.songs[this.index];
            this.play(this.current);
        },
        prev(){
            this.index--;
            if(this.index <0 ){
                // this will move it to the end of the list
                this.index = this.songs.lengh -1;
            }
            this.current = this.songs[this.index];
          this.play(this.current);

        }

    },
    created() {
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
      this.player.play();
    }

}
</script>

<style scoped>
    *{
      margin: 0;
      padding:0;
    }
    *{
        margin: 0;
        padding-bottom: 20px;
        font-family: sans-serif;
        box-sizing: border-box;
    }

    .header{
        display:flex;
        padding: 15px;
        justify-content: center;
        font-size: 50px;
        background-color: rgb(248, 203, 3);
        color: #0f0f0f;
        -webkit-font-smoothing: antialiased;
    }
    main{
        width: 100%;
        max-width: 786px;
        margin: auto;
        padding: 25px;
    }
    .song-title{
        color: black;
        font-size: 32px;
        font-weight: 700;
        text-transform: uppercase;
        text-align: center;
    }
    .song-title span{
        color: rgb(17, 116, 202);
        font-weight: 400;
        font-style: italic;
    }
    .controls {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 30px 15px;
    }
    button{
        appearance: none;
        background: none;
        border: none;
        outline:none;
        cursor: pointer;
    }
    .play{
        font-size: 20px;
        font-weight: 700;
        padding: 12px 25px;
        margin: 0px 15px;
        border-radius: 5px;
        color:white;
        background-color: rgb(221, 76, 100);
    }
    button:hover{
        opacity: 0.8;
    }
    .next, .prev{
        font-size: 16px;
        font-weight: 700;
        padding: 10px 20px;
        margin: 0px 15px;
        border-radius: 6px;
        color:white;
        background-color: rgb(248, 159, 174);
    }
    .pause{
        font-size: 16px;
        font-weight: 700;
        padding: 10px 20px;
        margin: 0px 15px;
        border-radius: 6px;
        color:white;
        background-color: rgb(10, 0, 2);


    }
    h3{
        background-color: rgb(248, 203, 3);
        padding: 10px;
        border-radius: 20px;
       

    }
    .playlist{
        padding: 0px 30px;
        
    }
    .playlist h3 {
        color: black;
        font-size: 28px;
        font-weight: 400;
        margin-bottom: 30px;
        text-align: center;
    }
    .playlist .song {
        display: block;
        width: 100%;
        padding: 15px;
        font-size: 20px;
        font-weight: 700;
        cursor: pointer;
    }
     .playlist .song:hover {
         color: #ff5858;
     }

    
    .playlist .song.playing {
        color: white;
        background-image: linear-gradient(to right, #cc9a2e, #ff5858);
        border-radius: 20px;
    }
</style>



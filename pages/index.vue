<template>
  <div>
    <div id="navbar" style="padding-left: 0;">
        <div>
            <h1 class="fredoka_one">kimoty.net</h1>
            <p class="fredoka_one navbar">
                <a href="#box1" uk-scroll>TOP</a><br>
                <a href="#box2" uk-scroll>ABOUT</a><br>
                <a href="#box3" uk-scroll>SKILLS</a><br>
                <a href="#box4" uk-scroll>CREATED</a>
            </p>
        </div>
    </div>
    <div id="contents">
        <div id="box1" class="backGround">
            <div class="bgImg img01" v-bind:style="{'background-image': 'url('+ selfintro.img1.url +')'}"></div>
            <div class="bgImg img02" v-bind:style="{'background-image': 'url('+ selfintro.img2.url +')', 'animation-delay': '4s'}"></div>
            <div class="bgImg img03" v-bind:style="{'background-image': 'url('+ selfintro.img3.url +')', 'animation-delay': '8s'}"></div>
            <div class="bgImg img04" v-bind:style="{'background-image': 'url('+ selfintro.img4.url +')', 'animation-delay': '12s'}"></div>
            <div class="innner1" style="padding: 10% 0;">
            </div>
        </div>
        <div id="box2">
            <div class="innner">
                <div class="padding" uk-scrollspy="target: > h2; cls: uk-animation-slide-left-medium; delay: 100">
                    <h2 class="quicksand">About</h2>
                    <div uk-scrollspy="target: > div; cls: uk-animation-fade; delay: 300">
                        <div class="kiwi_maru uk-card uk-card-default uk-card-body">
                            <h3><i class="fas fa-user"></i> 自己紹介</h3>
                            <span class="text" v-html="selfintro.text"></span>
                            <p>
                                <i class="fab fa-twitter-square"></i> <a id="twitter" v-bind:href='"https://twitter.com/" + selfintro.twitter'>Twitter</a> |
                                <i class="fab fa-github-square"></i> <a id="github" v-bind:href='"https://github.com/" + selfintro.github'>Github</a>
                                <!-- <i class="fas fa-envelope-square"></i> admin<i class="fas fa-at"></i>example.com -->
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div id="box3">
            <div class="innner" >
                <div class="padding" uk-scrollspy="target: > h2; cls: uk-animation-slide-left-medium; delay: 100">
                    <h2 class="quicksand">Skills</h2>
                    <div class="kiwi_maru uk-child-width-1-2@m uk-child-width-1-2@s uk-grid-small uk-grid-match" uk-scrollspy="target: > div; cls: uk-animation-fade; delay: 150" uk-grid>
                        <div>
                            <div class="uk-card-small uk-card-default uk-card-body">
                                <h3 class="uk-card-title"><i class="fas fa-code"></i> プログラミング</h3>
                                <span v-html="selfintro.pg"></span>
                            </div>
                        </div>
                        <div>
                            <div class="uk-card-small uk-card-default uk-card-body" uk-lightbox>
                                <h3 class="uk-card-title"><i class="fas fa-music"></i> 音楽</h3>
                                <span v-html="selfintro.mus"></span>
                            </div>
                        </div>
                    </div>
                </div> 
            </div>
        </div>
        <div id="box4">
          <div class="innner">
          <div class="padding" uk-scrollspy="target: > h2; cls: uk-animation-slide-left-medium; delay: 100">
              <h2 class="quicksand">Created</h2>
              <div uk-scrollspy="target: > div; cls: uk-animation-fade; delay: 300">
                  <div class="kiwi_maru uk-card uk-card-default uk-card-body">
                      <h3><i class="fas fa-hammer"></i> 作ったもの</h3>
                      <ul>
                          <li v-for="content in created" :key="content.id">
                              <a v-bind:href='content.url'>{{ content.title }}</a>
                          </li>
                      </ul>
                  </div>
              </div>
          </div>
    </div>
        </div>
        <div id="box5" class="uk-light" style="text-align: right;">
            <small>{{ selfintro.copyright }}</small>
        </div>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  async asyncData() {
    const res = await Promise.all([
      axios.get(
        'https://kimoto.microcms.io/api/v1/selfintro',
        { headers: { 'X-MICROCMS-API-KEY': 'd2c5a21920d14a8a9eedf5cd3d2e285127b0' }}
      ),
      axios.get(
        'https://kimoto.microcms.io/api/v1/created',
        { headers: { 'X-MICROCMS-API-KEY': 'd2c5a21920d14a8a9eedf5cd3d2e285127b0' }}
      )
    ])
    return {
      selfintro: res[0].data,
      created: res[1].data.contents
    }
  }
}
</script>
<style>
@media screen and (max-width: 480px) { 
    /* 画面サイズが480pxまで */
    .innner {
        width:  100%;
    }

    /*
    .navbar{
        display: none;
    }
    */
    #navbar {
    position: absolute;
    z-index: 100;
    width: 20%;
    font-size: 1.5em;
    line-height: 1.7em;
    margin: 4%;
    }
}
@media screen and (min-width: 481px) {
    /* 画面サイズが481pxから */
    .innner {
        width:  75%;
    }
    #navbar {
    position: fixed;
    z-index: 100;
    width: 20%;
    font-size: 1.5em;
    line-height: 1.7em;
    margin: 4%;
    }
}
body {
    margin: 0%;
}
#navbar a {
    color: #333;
}
#contents {
    height: auto;
}
#box1 {
    text-align: center;
    height: 100vh;
    width: 100%;

    /*
    background-color: #D95555;
    */
}
#box2 {
    width: 100%;
    background-color: #F28444;
}
#box3 {
    width: 100%;
    background-color: #F2A341;
}
#box4 {
    width: 100%;
    background-color: #03A6A6;
}
#box5 {
    width: 100%;
    background-color: #592E3E;
}
.innner1 {
    height: 100vh;
}
.innner {
    margin-right: 0;
    margin-left: auto;
}
.padding {
    padding: 2em 1em;
}
.fredoka_one {
    font-family: 'Fredoka One', cursive;
}
.quicksand {
    font-family: 'Quicksand', sans-serif;
}
.kiwi_maru {
    font-family: 'Kiwi Maru', serif;
} 
.text {
    line-height: 1.8em;
}

/* https://webparts.cman.jp/box/bgfade/ */
.backGround {
    position: relative;
    margin: auto;
    overflow: hidden;
}
.backGround .bgImg {
    position: absolute;
    z-index: -10;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    opacity: 0;
    animation: bgAnime 16s infinite; /* 4画像 × 各4s = 16s */
    background-size:  cover;
    background-repeat:  no-repeat;
    background-position:center center;
}

/*
.backGround .img01 {
    background-image: url(./image/back01.jpeg);
}
.backGround .img02 {
    background-image: url(./image/back02.jpeg);
    animation-delay: 4s;
}
.backGround .img03 {
    background-image: url(./image/back03.jpeg);
    animation-delay: 8s;
}
.backGround .img04 {
    background-image: url(./image/back04.jpeg);
    animation-delay: 12s;
}
*/
@keyframes bgAnime {
    0% { opacity: 0; }
    6% { opacity: 1; }
    25% { opacity: 1; }
    31% { opacity: 0; }
    100% { opacity: 0; }
}

/* ityped */
.ityped-cursor {
    font-size: 1em;
    opacity: 1;
    -webkit-animation: blink 0.3s infinite;
    -moz-animation: blink 0.3s infinite;
    animation: blink 0.3s infinite;
    animation-direction: alternate;
}
@keyframes blink {
    100% {
        opacity: 0;
    }
}
@-webkit-keyframes blink {
    100% {
        opacity: 0;
    }
}
@-moz-keyframes blink {
    100% {
        opacity: 0;
    }
}
</style>
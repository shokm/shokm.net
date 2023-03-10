<template>
  <div>
    <div id="navbar">
      <h1 class="fredoka_one">
        {{ selfintro.title }}
      </h1>
      <p class="fredoka_one navbar">
        <a href="#box1">TOP</a><br>
        <a href="#box2">ABOUT</a><br>
        <a href="#box3">SKILLS</a><br>
        <a href="#box4">CREATED</a>
      </p>
    </div>
    <div id="contents">
      <div id="box1" class="backGround">
        <div
          class="bgImg img01"
          :style="{ 'background-image': 'url(' + selfintro.img01.url + ')' }"
        />
        <div
          class="bgImg img02"
          :style="{
            'background-image': 'url(' + selfintro.img02.url + ')',
            'animation-delay': '4s'
          }"
        />
        <div
          class="bgImg img03"
          :style="{
            'background-image': 'url(' + selfintro.img03.url + ')',
            'animation-delay': '8s'
          }"
        />
        <div
          class="bgImg img04"
          :style="{
            'background-image': 'url(' + selfintro.img04.url + ')',
            'animation-delay': '12s'
          }"
        />
        <div class="innnerTop" />
      </div>
      <div id="box2">
        <div class="innner">
          <div class="padding">
            <h2 class="quicksand">
              About
            </h2>
            <div class="box kiwi_maru">
              <h3><i class="fas fa-user" /> 自己紹介</h3>
              <span class="text" v-html="selfintro.text" />
              <p>
                <i class="fab fa-twitter-square" />
                <a
                  id="twitter"
                  :href="'https://twitter.com/' + selfintro.twitter"
                >Twitter</a>
                | <i class="fab fa-github-square" />
                <a
                  id="github"
                  :href="'https://github.com/' + selfintro.github"
                >Github</a>
                <!-- <i class="fas fa-envelope-square"></i> admin<i class="fas fa-at"></i>example.com -->
              </p>
            </div>
          </div>
        </div>
      </div>
      <div id="box3">
        <div class="innner">
          <div class="padding">
            <h2 class="quicksand">
              Skills
            </h2>
            <div class="flex kiwi_maru">
              <div class="box2">
                <h3><i class="fas fa-code" /> プログラミング</h3>
                <span v-html="selfintro.pg" />
              </div>
              <div class="box3">
                <h3><i class="fas fa-music" /> 音楽</h3>
                <span v-html="selfintro.mus" />
              </div>
            </div>
          </div>
        </div>
      </div>
      <div id="box4">
        <div class="innner">
          <div class="padding">
            <h2 class="quicksand">
              Created
            </h2>
            <div class="box kiwi_maru">
              <h3><i class="fas fa-hammer" /> 作ったもの</h3>
              <ul>
                <li v-for="content in created" :key="content.id">
                  <a :href="content.url">{{ content.title }}</a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <div id="box5" class="footer quicksand">
        <small>{{ selfintro.copyright }}</small>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  async asyncData () {
    const res = await Promise.all([
      axios.get('https://kimoto.microcms.io/api/v1/selfintro', {
        headers: { 'X-MICROCMS-API-KEY': process.env.MICROCMS_API_KEY }
      }),
      axios.get('https://kimoto.microcms.io/api/v1/created?limit=1000', {
        headers: { 'X-MICROCMS-API-KEY': process.env.MICROCMS_API_KEY }
      })
    ])
    return {
      selfintro: res[0].data,
      created: res[1].data.contents
    }
  },
  head () {
    return {
      title: this.selfintro.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.selfintro.description
        }
      ]
    }
  }
}
</script>

<style>
@media screen and (max-width: 500px) {
  /* 画面サイズが500pxまで */
  .innner {
    width: 100%;
  }

  .navbar {
    /* display: none; */
  }

  #navbar {
    position: absolute;
    z-index: 100;
    font-size: 1.3em;
    line-height: 2em;
  }

  h1 {
    font-weight: normal;
    color: #333;
    font-size: 1.9em;
    margin-left: 5%;
  }

  #navbar a {
    color: #333;
    font-size: 1.1em;
    margin-left: 5%;
  }
}

@media screen and (min-width: 501px) {
  /* 画面サイズが501pxから */
  .innner {
    width: 75vw;
  }

  #navbar {
    position: fixed;
    z-index: 100;
    width: 20%;
    font-size: 1.4em;
    line-height: 1.7em;
  }

  h1 {
    font-weight: normal;
    color: #333;
    font-size: 1.9em;
    margin-top: 20%;
    margin-left: 20%;
  }

  #navbar a {
    color: #333;
    font-size: 1.1em;
    margin-left: 20%;
  }
}

html {
  scroll-behavior: smooth;
}

body {
  margin: 0%;
}

a {
  text-decoration: none;
  color: #1482a0;
}

p {
  color: #666;
}

h2 {
  font-weight: lighter;
  margin-top: 0;
  margin-bottom: 0.3em;
  color: #333;
  font-size: 2em;
}

h3 {
  font-weight: normal;
  margin-top: 0.7em;
  margin-bottom: 0.3em;
  color: #333;
  font-size: 1.5em;
}

li {
  color: #666;
}

/* https://www.nxworld.net/css-hover-underline-animation-examples-and-sass-mixin.html */

/* その1 */
.innner a {
  position: relative;
  display: inline-block;
  text-decoration: none;
}

.innner a::after {
  position: absolute;
  bottom: 0.2em;
  left: 0;
  content: '';
  width: 100%;
  height: 1px;
  background: #1482a0;
  opacity: 0;
  visibility: hidden;
  transition: 0.3s;
}

.innner a:hover::after {
  bottom: 0.2em;
  opacity: 1;
  visibility: visible;
}

/* その2 */
#navbar a {
  position: relative;
  display: inline-block;
  text-decoration: none;
}

#navbar a::after {
  position: absolute;
  bottom: 0.2em;
  left: 0;
  content: '';
  width: 100%;
  height: 2px;
  background: #333;
  transform: scale(0, 1);
  transform-origin: center top;
  transition: transform 0.3s;
}

#navbar a:hover::after {
  transform: scale(1, 1);
}

/* ここまで */
#contents {
  height: auto;
}

#box1 {
  text-align: center;
  height: 100vh;
  width: 100%;

  /* background-color: #D95555; */
}

#box2 {
  width: 100%;
  background-color: #f28444;
}

#box3 {
  width: 100%;
  background-color: #f2a341;
}

#box4 {
  width: 100%;
  background-color: #03a6a6;
}

#box5 {
  width: 100%;
  background-color: #592e3e;
}

.box,
.box2,
.box3 {
  border-radius: 10px;
  box-shadow: 0 10px 25px 0 rgba(0, 0, 0, 0.1);
}

@media screen and (max-width: 900px) {
  /* 画面サイズが900pxまで */
  .box {
    border-radius: 10px;
    background-color: #fff;
    padding: 0.6em 1.5em;
  }

  .flex {
    display: block;
  }

  .box2 {
    background-color: #fff;
    padding: 0.6em 1.5em;
  }

  .box3 {
    background-color: #fff;
    padding: 0.6em 1.5em;
    margin-top: 1em;
  }
}

@media screen and (min-width: 901px) {
  /* 画面サイズが901pxから */
  .box {
    border-radius: 10px;
    background-color: #fff;
    padding: 1em 2.5em;
  }

  .flex {
    display: flex;
  }

  .box2 {
    width: 100%;
    flex-grow: 1;
    background-color: #fff;
    padding: 0.6em 1.5em;
  }

  .box3 {
    width: 100%;
    flex-grow: 1;
    background-color: #fff;
    padding: 0.6em 1.5em;
    margin-left: 1em;
  }
}

.innnerTop {
  height: 100vh;
}

.innner {
  margin-right: 0;
  margin-left: auto;
}

.padding {
  padding: 2em 1em;
}

.footer {
  color: #999;
  text-align: right;
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
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
}

/*
.backGround .img01 {
    background-image: url(https://example.com/example.jpeg);
}
.backGround .img02 {
    background-image: url(https://example.com/example.jpeg);
    animation-delay: 4s;
}
.backGround .img03 {
    background-image: url(https://example.com/example.jpeg);
    animation-delay: 8s;
}
.backGround .img04 {
    background-image: url(https://example.com/example.jpeg);
    animation-delay: 12s;
}
*/
@keyframes bgAnime {
  0% {
    opacity: 0;
  }

  6% {
    opacity: 1;
  }

  25% {
    opacity: 1;
  }

  31% {
    opacity: 0;
  }

  100% {
    opacity: 0;
  }
}
</style>

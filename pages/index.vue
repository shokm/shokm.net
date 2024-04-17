<template>
  <div>
    <div id="navbar">
      <h1 class="fredoka_one">
        {{ selfintro.title }}
      </h1>
      <p class="fredoka_one navbar">
        <a href="#top">TOP</a><br>
        <a href="#about">ABOUT</a><br>
        <a href="#skills">SKILLS</a><br>
        <a href="#created">CREATED</a>
      </p>
    </div>
    <div id="contents">
      <div id="top" class="section01 backGround">
        <div class="bgImg img01" :style="{ 'background-image': 'url(' + selfintro.img01.url + ')' }" />
        <div class="bgImg img02" :style="{ 'background-image': 'url(' + selfintro.img02.url + ')', 'animation-delay': '4s' }" />
        <div class="bgImg img03" :style="{ 'background-image': 'url(' + selfintro.img03.url + ')', 'animation-delay': '8s' }" />
        <div class="bgImg img04" :style="{ 'background-image': 'url(' + selfintro.img04.url + ')', 'animation-delay': '12s' }" />
        <div class="innnerTop" />
      </div>
      <div id="about" class="section02">
        <div class="innner">
          <div class="padding">
            <h2 class="quicksand">
              About
            </h2>
            <div class="box01 kiwi_maru">
              <h3><i class="fas fa-user" /> 自己紹介</h3>
              <span class="text" v-html="selfintro.text" />
              <p>
                <span v-if="selfintro.twitter">
                  <i class="fa-brands fa-square-x-twitter" />
                  <a id="twitter" :href="'https://twitter.com/' + selfintro.twitter">X (Twitter)</a>
                </span>
                <span v-if="selfintro.github">
                  <span v-if="selfintro.twitter">|</span>
                  <i class="fa-brands fa-github-square" />
                  <a v-if="selfintro.github" id="github" :href="'https://github.com/' + selfintro.github">Github</a>
                </span>
                <span v-if="selfintro.email.user || selfintro.email.domain">
                  <span v-if="selfintro.twitter || selfintro.github">|</span>
                  <i class="fas fa-envelope-square" /> {{ selfintro.email.user
                  }}<i class="fas fa-at" />{{ selfintro.email.domain }}
                </span>
              </p>
            </div>
          </div>
        </div>
      </div>
      <div id="skills" class="section03">
        <div class="innner">
          <div class="padding">
            <h2 class="quicksand">
              Skills
            </h2>
            <div class="flex kiwi_maru">
              <div class="box02">
                <h3><i class="fas fa-code" /> プログラミング</h3>
                <span v-html="selfintro.pg" />
              </div>
              <div class="box03">
                <h3><i class="fas fa-music" /> 音楽</h3>
                <span v-html="selfintro.mus" />
              </div>
            </div>
          </div>
        </div>
      </div>
      <div id="created" class="section04">
        <div class="innner">
          <div class="padding">
            <h2 class="quicksand">
              Created
            </h2>
            <div class="box01 kiwi_maru">
              <h3><i class="fas fa-hammer" /> 制作物</h3>
              <ul>
                <li v-for="content in created" :key="content.id">
                  <a :href="content.url">{{ content.title }}</a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <div id="footer" class="section05 footer quicksand">
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
      axios.get(process.env.MICROCMS_API_BASE_URL + '/api/v1/selfintro', {
        headers: { 'X-MICROCMS-API-KEY': process.env.MICROCMS_API_KEY }
      }),
      axios.get(
        process.env.MICROCMS_API_BASE_URL + '/api/v1/created?limit=1000',
        {
          headers: { 'X-MICROCMS-API-KEY': process.env.MICROCMS_API_KEY }
        }
      )
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
        { hid: 'og:type', property: 'og:type', content: 'website' },
        {
          hid: 'description',
          name: 'description',
          content: this.selfintro.description
        },
        {
          hid: 'og:title',
          property: 'og:title',
          content: this.selfintro.title
        },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.selfintro.description
        },
        { hid: 'twitter:card', name: 'twitter:card', content: 'summary_large_image' },
        { hid: 'og:image', property: 'og:image', content: this.selfintro.ogp.url }
      ]
    }
  }
}
</script>

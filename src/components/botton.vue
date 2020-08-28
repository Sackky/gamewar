<template>
  <div>
    <div class="row">
      <div class="col-sm">
        <p style="font-size: 150%">{{aplayer.name}}</p>
        <p>
          <img v-bind:style="{width: aplayer.hp + 'px'}" :src="hp1" alt height="20px" />
        </p>
        <p style="font-size: 150%">{{thp}}{{aplayer.hp}}</p>
        <p>
          <img style="width:80%" :src="aplayer.image" />
        </p>
      </div>
      <div class="col-sm">
        <div class="row">
          <div class="col">
            <button class="btn btn-light" @click="reset()">NewGame</button>
          </div>
          <div class="col">
            <button v-bind:disabled="end" class="btn btn-light" @click="start()">Start</button>
          </div>
          <div class="col">
            <button v-bind:disabled="end" class="btn btn-light" @click="attack()">Attack</button>
          </div>
          <div class="col-4">
            <button v-bind:disabled="end" class="btn btn-light" @click="special()">SpecialAttack</button>
          </div>

          <br />
          <img src="https://media.giphy.com/media/jQyfzg4EwDzkiP26RG/giphy.gif" width="100%" />
        </div>
        <div class="row">
          <div class="col-sm"></div>
          <div class="col-sm">
            <div id="score">
              <div v-if="amonster.hp <= 0"><img src="https://media.giphy.com/media/SsaGzaI7QEaft8s3HK/giphy.gif" width="100%" /></div>
              <div v-else-if="aplayer.hp <= 0"><img src="https://media.giphy.com/media/l3vQXpNnRGaAVprjO/giphy.gif" width="100%" /></div>
            </div>
          </div>
          <div class="col-sm"></div>
        </div>
      </div>
      <div class="col-sm">
        <p style="font-size: 150%">{{amonster.name}}</p>
        <p>
          <img v-bind:style="{width: amonster.hp + 'px'}" :src="hp2" alt height="15px" />
        </p>
        <p style="font-size: 150%">{{thp}}{{amonster.hp}}</p>
        <p>
          <img style="width:80%" :src="amonster.image" />
        </p>
      </div>
    </div>
    <hr />
    <div class="row">
      <div class="col"></div>
      <div class="col-6">
        <div class="card bg-light">
          <div class="card-header">How to Play</div>
          <div class="card-body">
            <h6 align="left">
              <p>1.Press the Start button to randomize both characters.</p>
              <p>2.Press the Attack button to damage a light attack on each other and get hit at the same time.</p>
              <p>3.Press the Special Attack button to damage a heavy attack on the enemy and get hit at the same time.</p>
              <p>4.Press the New Game button to start a new game.</p>
            </h6>
          </div>
        </div>
      </div>d
      <div class="col"></div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      thp: "HP:",
      end: false,
      hp2:
        "https://i.ppy.sh/bca61e3c2183a86ddb4c1d75914fab845e2b128f/687474703a2f2f692e696d6775722e636f6d2f6953766c5662432e706e67",
      hp1:
        "https://i.ppy.sh/bca61e3c2183a86ddb4c1d75914fab845e2b128f/687474703a2f2f692e696d6775722e636f6d2f6953766c5662432e706e67",
      aplayer: { name: "", hp: 1, image: "", hp1: "" },
      player: [
        {
          name: "Monkey D Luffy",
          hp: 380,
          image:
            "https://www.picgifs.com/gifs/anime/monkey-d-luffy/monkey-bf7FcM.gif",
        },
        {
          name: "Protogus D Ace",
          hp: 330,
          image:
            "https://i.gifer.com/4GEy.gif",
        },
        {
          name: "Roronoa Zoro",
          hp: 330,
          image:
            "https://steamuserimages-a.akamaihd.net/ugc/279596493228739516/E3FEB47549E77E923A0C5241293E90053ADAC662/",
        },
        {
          name: "Vinsmoke Sanji",
          hp: 330,
          image:
            "https://i.gifer.com/PBD0.gif",
        },      
      ],
      amonster: { name: "", hp: 1, image: "", hp1: "" },
      monster: [
        {
          name: "Marshall D.Teach",
          hp: 500,
          image:
            "http://1.bp.blogspot.com/-GZqLUpNMVA8/UGhIgxvOLKI/AAAAAAAAFqQ/_bQyVNobbLU/s1600/Marshall+D+Teach.gif",
        },
        {
          name: "Kaido",
          hp: 120,
          image:
            "https://steamuserimages-a.akamaihd.net/ugc/200806427134469800/79F9D7D0E2D6EDE17E596FD6882B953BA1C58D77/",
        },
        {
          name: "Kuzan Aokiji",
          hp: 215,
          image:
            "https://64.media.tumblr.com/4efd65fa8854e260b9938bd9ee073167/tumblr_mz3d4eoD0V1t02ogqo1_500.gifv",
        },
        {
          name: "Sakasuki Akainu",
          hp: 325,
          image: "http://4.bp.blogspot.com/-qKsgfaixgJ8/UGkg-hYsVyI/AAAAAAAAFu4/eltmibEj5Uc/s320/Sakazuki+Akainu.gif",
        },
      ],
      pmax: "",
      mmax: "",
    };
  },
  methods: {
    randomno: function (min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },
    start: function () {
      this.aplayer = this.player[this.randomno(1, 7) - 1];
      this.amonster = this.monster[this.randomno(1, 7) - 1];
    },
    attack: function () {
      this.pmax = Math.floor(Math.random() * 10 + 4);
      this.amonster.hp = this.amonster.hp - this.pmax;
      this.mmax = Math.floor(Math.random() * 10 + 4);
      this.aplayer.hp = this.aplayer.hp - this.mmax;
      if (this.aplayer.hp <= 0) {
        this.aplayer.hp = 0;
        this.end = true;
      } else if (this.amonster.hp <= 0) {
        this.amonster.hp = 0;
        this.end = true;
      }
    },
    special: function () {
      this.pmax = Math.floor(Math.random() * 15 + 6);
      this.amonster.hp = this.amonster.hp - this.pmax;
      this.mmax = Math.floor(Math.random() * 15 + 6);
      this.aplayer.hp = this.aplayer.hp - this.mmax;
      if (this.aplayer.hp <= 0) {
        this.aplayer.hp = 0;
        this.end = true;
      } else if (this.amonster.hp <= 0) {
        this.amonster.hp = 0;
        this.end = true;
      }
    },
    reset: function () {
      window.location.reload();
    },
  },
};
</script>
<style>
#score {
  font-size: 300%;
  color: aliceblue;
}
</style>
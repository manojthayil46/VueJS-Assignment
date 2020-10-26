<template>
  <div>
    <input type="text" class="search" placeholder="Search" v-model="search" />
    <div class="container">
      <div
        class="wrapper"
        v-for="player in filteredPlayers"
        v-bind:key="player.Id"
      >
        <img v-bind:src="`/players-images/${player.Id}.jpg`" />
        <h3>{{ player.PFName }}</h3>
        <h4>{{ player.SkillDesc }}</h4>
        <h4>{{ player.Value }}</h4>
        <h4>
          {{ player.UpComingMatchesList[0].CCode }} vs
          {{ player.UpComingMatchesList[0].VsCCode }}
        </h4>
        <h4>{{ player.UpComingMatchesList[0].MDate }}</h4>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "players",
  data() {
    return {
      players: null,
      search: "",
    };
  },

  created: function() {
    axios
      .get("https://api.jsonbin.io/b/5d0c6e6a860ae0341876aac6/2")
      .then((res) => {
        console.log(res.data);
        this.players = res.data;
      });
  },

  computed: {
    filteredPlayers: function() {
      if (this.search) {
        return this.players.filter((filteredplayer) => {
          return filteredplayer.PFName.toLowerCase().includes(
            this.search.toLowerCase()
          );
        });
      } else {
        return this.players;
      }
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
}

.search {
  border: 1px solid black;
  border-radius: 5px;
  height: 30px;
  padding: 2px 23px 2px 30px;
  outline: 0;
  background-color: #f5f5f5;
}

img {
  width: 50%;
  height: 100px;
}

.container {
  width: 100%;
  height: 100%;
}

.wrapper {
  width: 200px;
  border: 1px solid black;
  padding: 20px;
  margin: 10px;
}

.wrapper:hover {
  transform: scale(1.1);
}
h3 {
  margin-bottom: 1%;
}
</style>

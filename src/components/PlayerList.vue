<template>
  <div class="container text-center">
    <div class="row" v-for="(category, index) in categorizedPlayers" :key="index">
      <h1>{{ category.title }}</h1>
      <div v-for="player in category.players" :key="player.name" class="col-md-4 mb-3">
        <div class="card">
          <img :src="player.image" class="card-img-top" alt="Player Image">
          <div class="card-body">
            <h5 class="card-title">{{ player.name }}</h5>
            <p class="card-text">Matches: {{ player.matches }}</p>
            <p class="card-text">Runs: {{ player.runs }}</p>
            <p class="card-text">50/100s: {{ player['50s'] }}/{{ player['100s'] }}</p>
            <p class="card-text">Highest Score: {{ player.highest_score }}</p>
            <p class="card-text">Team Name: {{ player.team_name }}</p>
            <p class="card-text">Best Bowling Figures: {{ player.best_bowling_figures }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['players', 'selectedTeam'],
  computed: {
    categorizedPlayers() {
      const roles = {
        2: 'Batsman',
        3: 'All-rounder',
        4: 'Bowler'
      };

      let categories = { Batsman: [], 'All-rounder': [], Bowler: [] };

      this.players.forEach(player => {
        const category = roles[player.role];
        if (category) {
          categories[category].push(player);
        }
      });

      return Object.keys(categories).map(title => ({
        title,
        players: this.filterPlayers(categories[title])
      }));
    }
  },
  methods: {
    filterPlayers(players) {
      return players.filter(player => 
        this.selectedTeam === 'ALL' || player.team_name === this.selectedTeam
      );
    }
  }
}
</script>

<style scoped>
</style>

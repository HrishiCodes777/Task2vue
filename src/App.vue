<template>
  <div id="app">
    <AppNavbar
      :selectedTeam="selectedTeam"
      :teams="teams"
      @update-selected-team="updateSelectedTeam"
    />
    <PlayerList
      :players="filteredPlayers"
      :selectedTeam="selectedTeam"
    />
  </div>
</template>

<script>
import AppNavbar from './components/AppNavbar.vue'
import PlayerList from './components/PlayerList.vue'
import playersData from './assets/players.json'

export default {
  name: 'App',
  components: {
    AppNavbar,
    PlayerList
  },
  data() {
    return {
      players: playersData.originalPlayers,
      selectedTeam: 'ALL',
      teams: [
        { name: 'All', value: 'ALL' },
        { name: 'India', value: 'IND' },
        { name: 'Pakistan', value: 'PAK' },
        { name: 'Australia', value: 'AUS' },
        { name: 'England', value: 'ENG' }
      ]
    };
  },
  computed: {
    filteredPlayers() {
      if (this.selectedTeam === 'ALL') {
        return this.players;
      }
      return this.players.filter(player => player.team_name === this.selectedTeam);
    }
  },
  methods: {
    updateSelectedTeam(newTeam) {
      this.selectedTeam = newTeam;
    }
  }
}
</script>

<style>
</style>

<template>
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Sportz Interactive</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
        aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <select name="team" id="team" :value="selectedTeam" @change="updateTeam($event)">
            <option value="ALL">ALL</option>
            <option v-for="team in teams" :key="team.value" :value="team.value">{{ team.name }}</option>
          </select>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  props: ['selectedTeam', 'teams'],
  methods: {
    updateTeam(event) {
      this.$emit('update-selected-team', event.target.value);
    }
  }
}
</script>

<style scoped>
</style>

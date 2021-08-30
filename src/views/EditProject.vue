<template>
  <div>
    <h1>Edit Project</h1>
    <form @submit.prevent="handleUpdate">
      <label>Project Title:</label>
      <input type="text" v-model="title">
      <label>Project Details</label>
      <textarea v-model="details"></textarea>
      <button>Update</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
      uri: `https://my-json-server.typicode.com/HonfeiZenge/netninja-project-planner/${this.id}`
    }
  },
  methods: {
    handleUpdate() {
      let project = {
        title: this.title,
        details: this.details
      }

      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project)
      })
        .then(response => response.status === 200 ? this.$router.push('/') : console.log(response.status))
        .catch(err => console.log(err.message))
    }
  },
  mounted() {
    fetch(this.uri)
      .then(response => response.json())
      .then(projectData => {
        this.title = projectData.title
        this.details = projectData.details
      })
      .catch(err => console.log(err.message))
  },
}
</script>

<style>
  h1 {
    text-align: center;
  }
</style>
<template>
  <div class="home">

    <FilterNav :current="current" @filterChange="current = $event" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
      </div>
    </div>
    <div v-else>
      <h3>loading to get data...</h3>
    </div>

  </div>
</template>

<script>
import SingleProject from '@/components/SingleProject.vue'
import FilterNav from '@/components/FilterNav.vue'

export default {
  name: 'Home',
  components: { SingleProject, FilterNav },
  data() {
    return {
      endpoint_url: 'https://my-json-server.typicode.com/HonfeiZenge/netninja-project-planner',
      projects: [],
      current: 'all'
    }
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id
      })
    },
    handleComplete(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })

      p.complete = !p.complete
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      else if (this.current === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      } else {
        return this.projects
      }
      
    }
  },
  mounted() {
    fetch(this.endpoint_url)
      .then(response => response.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
}
</script>

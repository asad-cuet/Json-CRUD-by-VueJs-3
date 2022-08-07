<template>
  <div class="home">
    <ul class="list-group">


   <li v-for="project in projects" :key="project.id" class="list-group-item">
      <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
   </li>

   
   </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from '@/views/SingleProject.vue'

export default {
  name: 'Home',
  data() {
    return {
      projects:[]
    }
  },
  components: {
    SingleProject
  },
  mounted()
  {
      fetch('http://localhost:3000/projects')
     .then(res => res.json())
     .then(data => this.projects = data)
     .catch(err => console.log(err.message ))
  },
  methods: {
    handleDelete(id) {
      this.projects=this.projects.filter(project=> {
       return project.id !==id;
      });
    },
    handleComplete(id) {
      let p=this.projects.find(project=> {
          return project.id === id
      });
      p.complete=!p.complete
    }
  }
}
</script>

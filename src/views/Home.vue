<template>
  <div class="home">
    <NavFilter @filterChange=" current = $event " :current="current"/>
    <ul class="list-group">

   <li v-for="project in filteredProject" :key="project.id" class="list-group-item">
      <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
   </li>

   
   </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from '@/views/SingleProject.vue';
import NavFilter from '@/views/NavFilter.vue';

export default {
  name: 'Home',
  data() {
    return {
      projects:[],
      current:'all'
    }
  },
  components: {
    SingleProject,
    NavFilter
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
  },
  computed: {
    filteredProject()
    {
      if(this.current=== 'all') {
        return this.projects;
      }
      if(this.current=== 'completed') {
        return this.projects.filter(project=> project.complete);
      }
      if(this.current=== 'ongoing') {
        return this.projects.filter(project=> !project.complete);
      }
    }

  }
}
</script>

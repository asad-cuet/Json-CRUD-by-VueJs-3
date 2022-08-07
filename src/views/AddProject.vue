<template>
  <div style="width:100%;max-width:500px;margin:auto;">
  <form @submit.prevent="handleSubmit">
  <div class="mb-3">
    <label for="exampleFormControlInput1" class="form-label">Title</label>
    <input type="text" v-model="title" class="form-control">
  </div>
  <div class="mb-3">
    <label for="exampleFormControlTextarea1" class="form-label">Details</label>
    <textarea v-model="details" class="form-control" rows="3"></textarea>
  </div>
  <button type="submit" class="btn">Add Project</button>
  </form>
  </div>
</template>

<script>
export default {
  name:'AddProject',
  data() {
    return {
      title:'',
      details:''
    }
  },
  methods: {
    handleSubmit() {
      let project= {
        title: this.title,
        details: this.details,
        complete: false
      }
      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project)
      })
      .then(()=> {
        this.$router.push('/')
      })
      .catch((err)=> console.log(err));
    }
  }

}
</script>

<style scoped>
input, textarea{
  border: 1px solid #e90074;
}
button {
  background-color: #00ce89;
  color:white;
}

</style>

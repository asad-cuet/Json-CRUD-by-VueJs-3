<template>


<div class="project" style="background-color:#172035;color:white;width:300px;margin:auto">

      <div class="pointer">
            <div @click="showDetails =!showDetails">{{project.title}}</div> 

            <div class="icons">
                  <span class="material-icons">edit</span>
                  <span @click="deleteProject" class="material-icons">delete</span>
                  <span class="material-icons">done</span>
            </div>


      </div>
      

      
      <div v-if="showDetails">
      {{project.details}}
      </div>


</div>




</template>

<script>
export default {
     name:"SingleProjet",
     props:['project'],
     data() {
      return {
            showDetails:false,
            url:'http://localhost:3000/projects/'+this.project.id
      }
     },
     methods:{
      deleteProject() {
          fetch(this.url,{ method: 'DELETE'})                 //deleted but page not updated
          .then(()=> this.$emit('delete',this.project.id))   //this is for page update  in Home.vue
          .catch(err=>console.log(err.message));
      }
     }
}
</script>

<style scoped>
.pointer {
      cursor: pointer;
      display:flex;
      justify-content: space-between;
      align-items: center;
}

.project {
      margin: 20px auto;
      background: white;
      padding: 10px 20px;
      border-radius:4px;
      box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
      border-left: 4px solid #e90074;
}

</style>
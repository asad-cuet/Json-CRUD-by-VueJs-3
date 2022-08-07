<template>


<div class="project" :class="{complete: project.complete }" style="background-color:#172035;color:white;width:300px;margin:auto">

      <div class="action">
            <div style="cursor:pointer" @click="showDetails =!showDetails">{{project.title}}</div> 

            <div class="icons">
                  <router-link :to="{ name:'EditProject',params : {id:project.id} }">
                        <span class="material-icons">edit</span>
                  </router-link>
                  <span @click="deleteProject" class="material-icons">delete</span>
                  <span @click="toggleComplete" class="material-icons tick">done</span>
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
      },
      toggleComplete() {
        fetch(this.url, { 
               method: 'PATCH',
               headers: { 'Content-Type' : 'application/json' },
               body :JSON.stringify({
                  complete: !this.project.complete
                  })
               })    //updated in db
        .then(()=> {
            this.$emit('complete',this.project.id)   //for updating in Home.vue
        })         
        .catch((err)=> console.log(err.message));
      }
     }
}
</script>

<style scoped>
.action {
      display:flex;
      justify-content: space-between;
      align-items: center;
}

.icons span {
      cursor: pointer;
}
.project {
      margin: 20px auto;
      background: white;
      padding: 10px 20px;
      border-radius:4px;
      box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
      border-left: 4px solid #e90074;
}
.project.complete {
      border-left: 4px solid #00ce89;
}
.project.complete .tick {
      color:#00ce89;
}

</style>
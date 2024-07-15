<template>
<div class="home">
 <h1>Home</h1>
<div v-for="project in projects" :key="project.id">
<SingleProject :project="project" @delete="delteteProject"/>
</div>
</div>

<<router-view>
</router-view>

</template>
 

<script>
import SingleProject from '../components/SingleProject'

export default{
  name:'Home',
  components:{
    SingleProject,
  },
  data(){
    return{
      projects :[]
    }
  },
  methods:{
    delteteProject(id){
      this.projects=this.projects.filter(project=>{
        return project.id ==! id;
      })
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response) => {
      return response.json()
    })
    .then((data) => {
      this.projects =data
    })
    .catch(() => {

    })
  }
}

</script>


<style>

</style>
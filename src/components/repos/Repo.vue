<template>
        <div v-for="repo in repos" :key="repo.nazwa">
            <h2>{{repo.nazwa}}</h2>
            <p>{{repo.content}}</p>
            <p>{{repo.type}}</p>
        </div>
</template>

<script>
export default {
    data(){
        return{
            repos:[
        {
          nazwa:'repo1',
          content:'content',
          type:'main'
        },
        {
          nazwa:'repo2',
          content:'content',
          type:'master'
        }
      ]
        }
    }
}
</script>

<style lang="scss" scoped>
div{
   display: flex;
   flex-direction: column; 
   margin:0;
   position: relative;
   margin: 20px;
   width: 555px;
   height:130px;
   & h2,&p{
       margin:0;
   } 
}
</style>

<template>
        <div>
            <img :src="repo.photo" alt="zdjęcie">
            <h2>{{repo.name}}</h2>
            <p>{{repo.description}}</p>
            <p>{{repo.branch}}</p>
        </div>
</template>

<script>
export default {
  props:['repo','key','repos'],
    data(){
        return{ 
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
   & h2,& p{
       margin:0;
   } 
   & img{
     width:60px;
     height:60px;
     border-radius: 50%;
     object-fit: cover;
   }
}
</style>

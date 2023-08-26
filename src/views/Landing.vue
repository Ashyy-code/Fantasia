<template>
  
  <div class="ft-wrapper">
    <div v-for="(p,index) in this.$store.state.fantasiaData" :key="index" class="p-stats">
        <span t>{{ p.char }}</span>
        <img :src="p.img" />
        <div class="row"><span g>Race Changes: </span><span r>{{ p.race_changes }}</span></div>
        <div class="row"><span g>Sex Changes: </span><span r>{{ p.sex_changes }}</span></div>
        <div class="row"><span g>Name Changes: </span><span r>{{ p.name_changes }}</span></div>
    </div>  
  </div>

</template>

<script>
import axios from 'axios';
export default {
  mounted(){
    this.loadFantasiaData();
  },
  methods:{
    async loadFantasiaData(){
      await axios.post("https://ashypls.com/endpoints/apis/Fantasia.aspx",{
        contentType:'application/json'
      }).then(
        response =>{
          this.$store.state.fantasiaData = response.data;
        }
      )
    }
  }
}
</script>

<style lang="scss" scoped>
.ft-wrapper{
  width:100vw;
  height:100vh;
  background:url('../assets/bg.png');
  background-size: cover;
  overflow:hidden;
  display:flex;
  flex-direction: row;
  align-items: center;
  flex-wrap: wrap;
  justify-content: center;
  gap:4rem;
  .p-stats{
    padding:1rem;
    color:white;
    display:flex;
    flex-direction: column;
    gap:1rem;
    justify-content: center;
    align-items: center;
    background:#000000c5;
    border-radius: .5rem;

    img{
      width:200px;
      aspect-ratio: 1;
      object-fit: cover;
      border-radius: 50%;
    }

    .row{
      
      display:flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
      gap:1rem;
      width:100%;
      
    }

    span{
      color:white;
      font-size:2rem;
      text-shadow: 2px 3px 6px #000000;

      &[g]{
        flex-grow:1;
      }

      &[t]{
        text-align: center;
        font-size:3rem;
      }

      &[r]{
        color:rgb(175, 237, 30);
        font-size:3rem;
      }

    }

  }
}
</style>
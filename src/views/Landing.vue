<template>
  <div class="ft-wrapper">
    <div
      v-for="(p, index) in this.$store.state.fantasiaData"
      :key="index"
      :class="
        'p-stats animate__animated animate__backInLeft animate__faster animate__delay-' +
        index +
        's'
      "
    >
      <div v-if="p.crowned" class="crown"><img src="../assets/crown.png" alt="" /></div>
      <span t>{{ p.char }}</span>
      <img :src="p.img" />
      <div class="row">
        <span g>Race Changes: </span
        ><span :style="getCountBg(p.race_changes)" r>{{ p.race_changes }}</span>
      </div>
      <div class="row">
        <span g>Sex Changes: </span
        ><span :style="getCountBg(p.sex_changes)" r>{{ p.sex_changes }}</span>
      </div>
      <div class="row">
        <span g>Name Changes: </span
        ><span :style="getCountBg(p.name_changes)" r>{{ p.name_changes }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  mounted() {
    this.loadFantasiaData();
  },
  methods: {
    async loadFantasiaData() {
      await axios
        .post("https://ashypls.com/endpoints/apis/Fantasia.aspx", {
          contentType: "application/json",
        })
        .then((response) => {
          this.$store.state.fantasiaData = response.data;
        });
    },
    getCountBg(count) {
      switch (count) {
        case 0:
          return "background:#ffffff08";
          break;
        case 1:
          return "background:#29a987";
          break;
        case 2:
          return "background:#169b15";
          break;
        case 3:
          return "background:#a4b521";
          break;
        case 4:
          return "background:#b57421";
          break;
        case 5:
          return "background:#b54b21";
          break;
        case 6:
          return "background:#b53721";
          break;
        default:
          return "background:#a32020";
          break;
      }
    }
  },
};
</script>

<style lang="scss" scoped>
body {
  background: url("../assets/bg.png");
  background-size: cover;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
.ft-wrapper {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background: none;
  background: url("../assets/bg.png");
  background-size: cover;
  overflow-y: auto;

  display: flex;
  flex-direction: row;
  align-items: center;
  flex-wrap: wrap;
  justify-content: center;
  gap: 4rem;

  .p-stats {
    padding: 1rem;
    color: white;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    justify-content: center;
    align-items: center;
    background: #000000c5;
    border-radius: 0.5rem;
    width: 300px;
    user-select: none;
    position: relative;

    .crown {
      position: absolute;
      width: 82px;
      height: 62px;
      top:-38px;
      right:-30px;
      user-select: none;

      img {
        width: 82px;
        height: 62px;
        aspect-ratio: unset;
        object-fit: none;
        border-radius: 0;
      }
    }

    img {
      width: 200px;
      aspect-ratio: 1;
      object-fit: cover;
      border-radius: 50%;
      user-select: none;
    }

    .row {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
      gap: 1rem;
      width: 100%;
    }

    span {
      color: white;
      font-size: 2rem;
      text-shadow: 2px 3px 6px #000000;

      &[g] {
        flex-grow: 1;
      }

      &[t] {
        text-align: center;
        font-size: 3rem;
      }

      &[r] {
        color: white;
        font-size: 1.5rem;
        aspect-ratio: 1;
        width: 18%;
        text-align: center;
        display: grid;
        place-items: center;
        border-radius: 50%;
      }
    }
  }
}
</style>
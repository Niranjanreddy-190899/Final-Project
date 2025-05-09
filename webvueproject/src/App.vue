<template>
  <MyHeader WebsiteName="Mobile Device Purchase Guide" authorName="By Niranjan Reddy" />

  <MobileBox v-if="Array.isArray(Mobiles)" :Mobiles="Mobiles" />

</template>

<script>
import MyHeader from './components/MyHeader.vue';
import MobileBox from './components/MobileBox.vue';

export default {
  name: 'App',
  components: {
    MyHeader,
    MobileBox
  },
  data() {
    return {
      Mobiles: []
    };
  },
  methods: {
    async fetchmobile() {
      try {
        const res = await fetch("https://webfinalproject-v1b6.onrender.com/api");
        const data = await res.json();
        console.log(data);
        this.Mobiles = data[0].Mobiles;
      } catch (error) {
        console.error("Error fetching mobile data:", error);
      }
    }
  },
  created() {
    this.fetchmobile();
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Montserrat', sans-serif;
}

.container {
  max-width: 400px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 0.3em solid black;
  padding: 30px;
  border-radius: 5px;
}

div {
  margin-bottom: 0.5em;
  text-align: center;
}
</style>

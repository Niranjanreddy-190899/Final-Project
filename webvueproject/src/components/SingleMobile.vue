<template>
  <div :style="{ backgroundColor: parseFloat(phone?.Ratings) > 4.5 ? '#fef08a' : '#bfdbfe' }">
    <h2>Phone Name: {{ phone.MobileName }}</h2>
    <h2>Year of Release: {{ phone.YearOfRelease }}</h2>
    <h2>Ratings: {{ phone.Ratings }}</h2>
    <h2>Cost: {{ phone.Cost }}</h2>

    <h3>Configurations:</h3>
    <ul v-if="phone.Configurations">
      <li>Display: {{ phone.Configurations.Display }}</li>
      <li>Processor: {{ phone.Configurations.Processor }}</li>
      <li>RAM: {{ phone.Configurations.RAM }}</li>
      <li>Storage: {{ phone.Configurations.Storage }}</li>
      <li>Camera: {{ phone.Configurations.Camera }}</li>
      <li>Battery: {{ phone.Configurations.Battery }}</li>
      <li>Operating System: {{ phone.Configurations['Operating System'] }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'SingleMobile',
  props: {
    phone: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
div {
  background-color: #ffffff;
  color: #333333;
  padding: 1.5em;
  text-align: center;
  width: 100%;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  border: 1px solid #e5e7eb;
  height: 100%; 
  display: grid;  
  grid-template-rows: auto 1fr auto; 
}


h2,
h3 {
  color: #3b82f6;
  margin: 0.5em 0;
}

li {
  text-align: left;
  margin-left: 1em;
}
</style>

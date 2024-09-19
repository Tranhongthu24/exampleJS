<template>
  <div class="all">
    <!-- <FetchingData />
    <Data/> -->
    <!-- <TreeView/> -->
     <FlightBooker/>
  </div>
</template>

<script setup>
import FetchingData from "./components/FetchingData.vue";
import Data from "./components/Data.vue";
import TreeView from "./components/TreeView.vue";
import FlightBooker from "./components/FlightBooker.vue";
</script>
<style scoped>
.all{
  margin: 50px;
}
</style>

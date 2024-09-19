<script setup>
import { ref, computed } from "vue";
const props = defineProps({
    gridData: Array,
    filterKey:String
})
const show = ref(false)
const handleChange = () => {
  show.value = !show.value;
  props.gridData.sort((a, b) => {
    if (a.power ===  typeof String) return show.value ? -1 : 1;
    if (b.power === typeof String) return show.value ? 1 : -1;

    return show.value ? a.power - b.power : b.power - a.power;
  });
};

const filterData = computed(() => {
  return props.gridData.filter((item) => {
    return item.name.toLowerCase().includes(props.filterKey.toLowerCase())
  })
})
</script>

<template>
  <input placeholder="search" v-model="searchName"/>
  <ul v-for="item in filterData">
    <li>{{ item.name }} - {{ item.power }}</li>
  </ul>
  <button @click="handleChange">click</button>
</template>
<style scoped>
input {
  border: 1px solid;
}
button {
  background-color: aqua;
  width: 40px;
  height: 30px;
  border-radius: 6px;
  text-align: center;
}
</style>

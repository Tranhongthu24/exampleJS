<script setup>
import { ref, computed } from "vue";

const props = defineProps({
  model: Object,
});

const isFolder = computed(() => {
  return props.model?.children?.length > 0;
});

const isOpen = ref(false);
const openTree = () => {
  isOpen.value = !isOpen.value;
};
const addChildren = ()=>{
    props.model.children.push({name:"new stuff"})
}

const addParent =()=>{
    if (!isFolder.value) {
        props.model.children = []
        isOpen.value = true
        addChildren()
    }
}

</script>

<template>
  <li>
    <div
      v-if="model"
      :class="{ bold: isFolder }"
      @click="openTree"
      @dblclick="addParent"
    >
      {{ model.name }}
      <span v-if="isFolder">[{{ isOpen ? "-" : "+" }}]</span>
    </div>
    <ul v-show="isOpen" v-if="isFolder">
      <TreeItem v-for="model in model.children" :model="model"/>
      <li @click="addChildren">+</li>
    </ul>
  </li>
</template>

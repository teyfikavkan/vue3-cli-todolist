<template>
  <HeaderTitleComponent />
  <AddTaskComponent />
</template>

<script>
import HeaderTitleComponent from "@/components/HeaderTitleComponent/HeaderTitleComponent.vue";
import AddTaskComponent from "@/components/AddTaskComponent/AddTaskComponent.vue";

export default {
  components: {
    HeaderTitleComponent: HeaderTitleComponent,
    AddTaskComponent: AddTaskComponent,
  }
};
</script>

<style>
</style>
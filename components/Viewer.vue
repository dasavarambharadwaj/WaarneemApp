<template>
  <div class="flex flex-col">
    <w-filter
      v-model="sliderValue"
      class="w-10"
      :min="0"
      :max="1000"
      :step="10"
    ></w-filter>
    <w-shifts></w-shifts>
  </div>
</template>
<script>
import WFilter from "./Filter.vue";
import WShifts from "./Shifts.vue";
export default {
  name: "WViewer",
  props: {},
  components: {
    WFilter,
    WShifts,
  },
  data() {
    return {
      sliderValue: 0,
    };
  },
};
</script>

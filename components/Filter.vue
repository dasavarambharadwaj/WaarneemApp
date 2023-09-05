<template>
  <div class="flex flex-col">
    <w-layout class="w-96">
      <template v-slot:header>Filter</template>
      <Form :label-width="120" label-position="left">
        <FormItem label="Filter on price">
          <Slider
            v-model="sliderValue"
            @on-input="inputChanged"
            :min="min"
            :max="max"
            :step="step"
          ></Slider>
        </FormItem>
      </Form>
    </w-layout>
  </div>
</template>
<script>
import WLayout from "./Layout.vue";

export default {
  name: "WFilter",
  components: { WLayout },
  props: {
    value: {
      type: Number,
      default: 0,
    },
    min: {
      type: Number,
      default: 0,
    },
    max: {
      type: Number,
      default: 10,
    },
    step: {
      type: Number,
      defualt: 10,
    },
  },
  data() {
    return {
      sliderValue: 0,
    };
  },
  created() {
    this.sliderValue = this.value;
  },
  methods: {
    inputChanged(value) {
      this.$emit("input", this.value);
    },
  },
};
</script>

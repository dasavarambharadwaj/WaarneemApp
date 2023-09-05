<template>
  <div class="flex flex-col">
    <w-layout class="w-full">
      <template v-slot:header>Shifts</template>
      <template v-slot:action
        ><Button
          size="large"
          type="primary"
          class="font-bold"
          @click="showEditor = true"
          >Add Shift</Button
        >
      </template>
      <div class="flex flex-col gap-3">
        <Card v-for="card in [1, 2, 3]" :key="card">
          <template v-slot:title>
            <div class="flex h-auto justify-between">
              <div class="flex-col flex">
                <h3 class="text-2xl font-bold text-start h-auto">Title</h3>
                <p class="text-base">Description</p>
              </div>
              <Button
                size="large"
                icon="md-create"
                type="primary"
                shape="circle"
              ></Button>
            </div>
          </template>
          <template>
            <h3 class="text-2xl font-bold text-start">Dates</h3>
            <div class="pt-3 flex flex-col gap-3 text-start">
              <div
                v-for="item in [1, 2, 3, 4, 5]"
                :key="item"
                class="flex gap-2 bg-gray-700 p-3 text-white rounded"
              >
                <div class="w-1/5">12 dec 2020</div>
                <div class="w-1/5">09:00</div>
                <div class="w-1/5">17:00</div>
                <div
                  class="w-1/5 text-ellipsis whitespace-nowrap overflow-hidden"
                  title="consultation"
                >
                  Consultation
                </div>
                <div class="w-1/5 text-end">$70</div>
              </div>
            </div>
          </template>
        </Card>
      </div>
    </w-layout>
    <Drawer
      title="Create"
      v-model="showEditor"
      width="720"
      :mask-closable="false"
    >
      <w-editor v-model="selectedShift"></w-editor>
    </Drawer>
  </div>
</template>
<script>
import WLayout from "./Layout.vue";
import WEditor from "./Editor.vue";

export default {
  name: "WShifts",
  components: { WLayout, WEditor },
  props: {
    shifts: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      sliderValue: 0,
      showEditor: false,
      selectedShift: {},
    };
  },
  created() {
    this.sliderValue = this.value;
  },
  methods: {
    inputChanged(value) {
      this.$emit("input", value);
    },
  },
};
</script>

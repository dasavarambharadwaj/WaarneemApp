<template>
  <div class="flex flex-col items-start">
    <div class="flex justify-between w-full">
      <div>
        <h2 class="text-2xl font-bold">
          <slot name="header"></slot>
        </h2>
        <div class="h-1 bg-pink-700 w-4/5 rounded"></div>
      </div>

      <slot name="action"></slot>
    </div>
    <div class="w-full pl-3 pt-3">
      <slot name="default"></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: "WLayout",
  data() {
    return {};
  },
};
</script>

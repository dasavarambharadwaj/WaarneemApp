<template>
  <div class="m-auto min-h-screen flex-col p-4 flex text-center">
    <h1 class="text-3xl font-bold">Waarneem App</h1>
    <Card>
      <w-viewer></w-viewer>
    </Card>
  </div>
</template>

<script>
import WViewer from "@/components/Viewer.vue";
export default {
  name: "IndexPage",
  components: {
    WViewer,
  },
};
</script>

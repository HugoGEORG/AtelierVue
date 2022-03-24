<template>
  <div class="about">
    <h1>This is an about page</h1>
    <Map />
  </div>
</template>
<script>
import Map from "@/components/map.vue";

export default {
  name: "Home",
  components: {
    Map,
  },
};
</script>
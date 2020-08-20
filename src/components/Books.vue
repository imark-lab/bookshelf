<template>
  <div class="books card">
    <img :src="img" alt="" class="card-img-top" />
    <div class="card-body">
      <h5 class="card-title">{{ title }}</h5>
      <p class="card-text">{{ subtitle }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ShowBooks",
  props: ["img", "title", "subtitle"],
};
</script>

<style scoped lang="scss">
.books {
  width: 18rem;
}
</style>

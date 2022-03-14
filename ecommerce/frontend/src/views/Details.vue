<template>
  <div class="details">
    <div>
      <span style="color: black; font-size: 30px;"><b>Listado de productos</b></span>
      <template>
        <div>
          <section class="wrapper">
            <h2>{{ item.name }}</h2>
          </section>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: 'details',
  data() {
    return {
      detail: this.$store.getters.products(this.$route.params.item.id)
    }
  }
};
</script>
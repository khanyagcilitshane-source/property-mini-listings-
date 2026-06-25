<template>

  <header class="header">
    <h1>Homes & Beyond</h1>
    <p>{{ count }} Properties Available</p>
    <p>{{ favourites }}Saved Properties</p>
  </header>

</template>

<script>
export default {
  props: ["count", "favourites"]
  }
</script>


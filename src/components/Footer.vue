<template>
  <footer>
    <p>
      © 2021 Nintendo. Games are property of their respective owners. Nintendo
      of America Inc. Headquarters are in Redmond, Washington
    </p>
    <img src="../assets/logo-nintendo.png" alt="" class="logo-nintendo" />
  </footer>
</template>

<script>
export default {};
</script>

<style scoped>
footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 1px solid lightgrey;
  padding: 0.7em 3em;
}
footer p {
  font-size: 0.7em;
  padding-right: 1em;
}
footer img {
  max-width: 100px;
}
</style>

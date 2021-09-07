<template>
  <div class="p-2 box-border flex flex-col bg-green-100 h-screen">
    <h1 class="text-2xl">Transition Test</h1>
    <div class="bg-white p-4 my-2" @click="$router.push('/demo/transition/right')">TO RIGHT</div>
    <NuxtLink to="/demo/transition/left"><div class="bg-white p-4 my-2">TO LEFT</div></NuxtLink>
  </div>
</template>

<script>
export default {
  transition(to, from) {
    if (to.path=="/demo/transition/right") return "to-right";
    if (from!=undefined && from.path=="/demo/transition/right") return "to-left";
    if (to.path=="/demo/transition/left") return "to-left";
    if (from!=undefined && from.path=="/demo/transition/left") return "to-right";
    


    return "fade";
  },


}
</script>

<style scoped>

</style>
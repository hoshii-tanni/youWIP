<template>
  <Nuxt />
</template>

<script>
export default {

}
</script>

<style>
/* router transition */
.fade-enter-active, .fade-leave-active {
  transition: opacity .3s; 
}
.fade-enter, .fade-leave-to
/* .fade-leave-active below version 2.1.8 */ 
{
  opacity: 0;
}

/* -> 右方向へ遷移 -> */
.to-right-leave-active {
  transition: transform .15s;
  transform: translateX(0);
}
.to-right-leave-to {
  transform: translateX(-100%);
}
.to-right-enter-active {
  transition: transform .15s, opacity .15s;
}
.to-right-enter {
  /*transform: scale(80%);*/
  opacity: 0;
}

/* <- 左方向へ遷移 <- */
.to-left-leave-active {
  transition: opacity .15s;
}
.to-left-leave-to {
  opacity: 0;
}
.to-left-enter-active {
  transition: transform .15s; 
  transform: translateX(0);  
}
.to-left-enter {
  transform: translateX(-100%);
}


</style>
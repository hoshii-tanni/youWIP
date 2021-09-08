<template>
  <div class="">
    <div class="header w-full h-14">
      <i class="bi bi-chevron-left text-2xl"></i>
      <div class="text-xl">保存</div>
    </div>
    <div class="content px-3 mt-16 mb-96 box-border flex flex-col">
      <div><input type="text" /></div>
      <div><input type="text" /></div>
      <ul>
        <li><input type="text" /></li>
      </ul>
      <div><i class="bi bi-plus-circle"></i></div>
      <div><textarea name="" id="" cols="30" rows="10"></textarea></div>
      <ul><li><input type="checkbox" /><input type="text" /></li></ul>
      <div><i class="bi bi-plus-circle"></i></div>


    </div>
    
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.mt-18 { margin-top: 4.5rem; }



.header {
  position: fixed;
  top: 0; left: 0;

  padding: 0 .75rem;
  box-sizing: border-box;

  display: flex;
  justify-content: space-between;
  align-items: center;
}


input[type="text"], textarea {
  border: solid 1px #888;
}


</style>
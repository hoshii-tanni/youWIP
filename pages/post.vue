<template>
  <div class="flex flex-col items-center">

    <div class="header">
      <i class="bi bi-plus-circle text-2xl"></i>
      <div class="text-2xl">youWIP</div>
      <i class="bi bi-clock-fill text-2xl"></i>
    </div>

    <div class="content max-w-lg w-full px-3 mt-16 mb-96 box-border flex flex-col">
      <ul>
        <li class="task p-2 pb-1">
          <div class="flex justify-between items-end">
            <div class="text-xl font-bold">タイトル</div>
            <i class="bi bi-pencil-fill bg-pink text-white flex justify-center items-center rounded w-8 h-8"></i>
          </div>
          <div class="text-gray-500 my-1">
            #ハッシュタグ
          </div>

          <AccordionList>
            <div class="text-gray-500 mb-1">
              概要...
            </div>
            <ul>
              <li>ToDo..</li>
            </ul>
          </AccordionList>
        </li>
      </ul>
    </div>

  </div>
</template>

<script>
export default {
}
</script>

<style lang="scss">
.bg-pink { background-color: #da0063; }
.header {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 3.5rem;
  padding: 0 .75rem;
  border-bottom: solid 1px #aaa;
  border-radius: .5rem;
  box-sizing: border-box;
  z-index: 10;
  /*backdrop-filter: blur(5px);*/
  background-color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.content {
  li.task {
    border: solid 1px #aaa;
    border-radius: .5rem;
  }
}
</style>
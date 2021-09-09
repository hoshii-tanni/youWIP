<template>
  <div class="flex flex-col items-center">

    <div class="header">
      <img @click="$router.push('/post')" class="img" src="/plus_green_01.png" width="40" />
      <img class="img" src="/colored.png" />
      <img class="img" src="/timeline.png" width="40" />
    </div>

    <div class="content max-w-lg w-full px-3 mt-16 mb-96 box-border flex flex-col">
      <ul>
        <li v-for="(n,i) in tasks.length" :key="i" class="task flex flex-col my-2">
          <div v-if="tasks[i].image!=''" class="image" :style="'background-image: url(' + tasks[i].image + ');'"></div>
          <div class="mx-2 mt-2 flex justify-between items-end">
            <div class="text-xl font-bold">{{tasks[i].title}}</div>
            <img class="img" src="/edit.png" width="40" />
          </div>
          <div class="mx-2 my-1 text-gray-500">
            <ul class="flex">
              <li v-for="(n,j) in tasks[i].tags.length" :key="j" class="flex flex-col mr-2">
                #{{tasks[i].tags[j]}}
              </li>
            </ul>
            
          </div>

          <AccordionList>
            <div class="mx-2 text-gray-500">
              {{tasks[i].description}}
            </div>
            <ul class="mx-2">
              <li v-for="(n,j) in tasks[i].todo.length" :key="j" class="flex items-center my-2">
                <input class="text-xl pr-2" v-model="tasks[i].todo[j].checked" type="checkbox" disabled/>
                <div class="w-100">{{tasks[i].todo[j].title}}</div>
              </li>
            </ul>
          </AccordionList>
        </li>
      </ul>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],

    }
  },

  created() {
    this.tasks.push({
      title: "グミを作りたい", // タイトル
      image: "/img/45_result_Cycles_960.png",　// 画像パス
      deadline: "", // 締め切り
      description: "これはBlenderで作ったグミ", // 概要
      tags: ["料理", "お菓子"], // タグ
      todo: [{
        checked: false,
        title: "作り方を調べる",
        deadline: "",
      }], // ToDo
    })
  }

}
</script>

<style lang="scss">
.h−273 { height: 273px; }
.bg-pink { background-color: #da0063; }


input, select, textarea {
  -webkit-appearance: none;
  appearance: none;
}

input[type="checkbox"]::before {
  font-family: bootstrap-icons !important;
  content: "\f584";
  color: #99C9C5;

  display: flex;
  justify-content: center;
}

input[type="checkbox"]:checked::before {
  font-family: bootstrap-icons !important;
  content: "\f26c";
  color: #99C9C5;
}



.header {
  position: fixed;
  top: 0; left: 0;

  width: 100%; height: 3.5rem;
  padding: 0 .75rem;
  border-bottom: solid 1px #aaa;
  border-radius: 0 0 .5rem .5rem;
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

    background-color: #fff;
    overflow: hidden;

    .image {
      width: 100%; height: 273px;
      background-size: cover;
      
    }
  }

}
</style>
<template>
  <div class="flex flex-col items-center">

    <div class="header w-full h-14 z-10">
      <i class="bi bi-chevron-left text-2xl"></i>
      <div @click="display()">タスクの編集</div>
      <div class="px-4 py-1 bg-pink text-white rounded">保存</div>
    </div>

    <div class="content max-w-lg w-full px-3 mt-16 mb-96 box-border flex flex-col">
      <div class="py-3">
        <input class="w-full px-2 py-1 border-white rounded text-lg font-bold" v-model="title" type="text" placeholder="タイトル"/>
      </div>

      <div class="py-3 flex items-center">
        <i class="bi bi-calendar-check text-2xl pr-1"></i>
        <Datetime
          v-model="deadline"
          :label="'締め切り'"
        ></Datetime>
      </div>

      <ul class="py-3">
        <li v-for="(n,i) in tags.length" :key="i" class="flex items-center my-2">
          <i class="bi bi-hash text-2xl pr-1"></i>
          <input class="px-2 py-1 rounded" v-model="tags[i]" type="text" placeholder=""/>
          <i @click="removeTag(i)" class="bi bi-trash-fill text-xl pl-2 text-gray-400"></i>
        </li>
        <li @click="addTag()" class="my-1 text-gray-400">
          <i class="bi bi-plus-circle pl-3 pr-1"></i>
          タグを追加する
        </li>
      </ul>


      <div class="py-3">
        <textarea rows="5" class="w-full p-2 rounded" placeholder="概要"></textarea>
      </div>

      <ul class="py-3">
        <li v-for="(n,i) in todo.length" :key="i" class="flex items-center my-2">
          <input class="text-xl pr-2" v-model="todo[i].checked" type="checkbox"/>
          <input class="w-full px-2 py-1 rounded" v-model="todo[i].title" type="text" placeholder="ToDo..."/>
          <i @click="removeTodo(i)" class="bi bi-trash-fill text-xl pl-2 text-gray-400"></i>
        </li>
        <li @click="addTodo()" class="my-1 text-gray-400">
          <i class="bi bi-plus-circle pl-3 pr-1"></i>
          ToDoを追加する
        </li>
      </ul>



    </div>
    
  </div>
</template>

<script>
import Vue from 'vue'
import Datetime from 'vue-ctk-date-time-picker';
import 'vue-ctk-date-time-picker/dist/vue-ctk-date-time-picker.css';

Vue.component('VueCtkDateTimePicker', Datetime);

export default {
  components: {
    Datetime
  },

  data() {
    return {
      title: "", // タイトル
      deadline: "", // 締め切り
      tags: [], // タグ
      todo: [],


    }
  },

  created() {
    this.addTag();
    this.addTodo();
  },

  methods: {
    display(){ // デバッグ用メソッド
      alert(this.tags)
      console.log(this)
    },

    // タグの追加
    addTag() {
      this.tags.push("");
    },

    // タグを消す。配列のindexを指定する
    removeTag(idx) {
      this.tags.splice(idx, 1);
    },

    // ToDoの追加
    addTodo(){
      this.todo.push({
        checked: false,
        title: "",
        deadline: "",
      })
    },

    // ToDoを消す。配列のindexを指定する
    removeTodo(idx) {
      this.todo.splice(idx, 1);
    },


  }

}
</script>

<style lang="scss" scoped>
.mt-18 { margin-top: 4.5rem; }
.bg-pink { background-color: #da0063; }


/* Date-ctk-picker */
label.field-label { display: none }


.header {
  position: fixed;
  top: 0; left: 0;

  padding: 0 .75rem;
  box-sizing: border-box;

  backdrop-filter: blur(5px);

  display: flex;
  justify-content: space-between;
  align-items: center;
}

input[type="text"], textarea {
  border: solid 1px #888;
}

input, select, textarea {
  -webkit-appearance: none;
  appearance: none;
}

input[type="checkbox"]::before {
  font-family: bootstrap-icons !important;
  content: "\f584";
}

input[type="checkbox"]:checked::before {
  font-family: bootstrap-icons !important;
  content: "\f26c";
}


</style>
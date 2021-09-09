<template>
  <div class="flex flex-col items-center">

    <div class="header w-full h-20 z-10">
      <!-- <i class="bi bi-chevron-left green text-2xl"></i> -->
      <img class="img py-2" src="/back_01.png" width="40" />
      <div class="px-4 py-2 bg-pink text-white rounded">保存</div>
    </div>

    <div class="content max-w-lg w-full px-3 mt-20 mb-96 box-border flex flex-col">
      <div class="py-4">
        <input class="w-full px-2 py-4 border-white rounded text-lg" type="text" placeholder="タイトル"/>
      </div>

      <div class="py-3 flex items-center">
        <!-- <i class="bi bi-calendar-check text-2xl pr-1"></i> -->
        <img class="img pr-1" src="/calendar_green_01.png" width="40" />
        <Datetime
          v-model="deadline"
          :color="'#99C9C5'"
          :button-color="'#99C9C5'"
          :label="'締め切り'"
        ></Datetime>
      </div>

      <ul class="py-3">
        <li v-for="(n,i) in tags.length" :key="i" class="flex items-center my-2">
          <!-- <i class="bi bi-hash text-2xl pr-1"></i> -->
          <img class="img pr-1 w-10" src="/hashtag_green_01.png" />
          <input class="px-2 py-1 rounded" v-model="tags[i]" type="text" placeholder=""/>
          <!-- <i class="bi bi-trash-fill text-xl pl-2 text-gray-400"></i> -->
          <img class="img pl-1 w-10" src="/trash_green_01.png" />
        </li>
        <li @click="addTag()" class="my-1 text-gray-400">
          <i class="bi bi-plus-circle pl-3 pr-1"></i>
          タグを追加する
        </li>
      </ul>
 

      <div class="py-2">
        <textarea rows="5" class="w-full p-2 rounded" v-model="description" placeholder="概要"></textarea>
      </div>

      <ul class="py-2">
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
      description: "", // 概要
      tags: [], // タグ
      todo: [], // ToDo
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

    // 保存
    submit () {
      let dbTasks = this.$fire.firestore.collection('tasks')
      dbTasks
        .add({
          title: this.title,
          tags: this.tags,
          description: this.description,
          deadline: this.deadline,
          todo: this.todo,
        })
        .then(ref => {
          console.log('Add ID: ', ref.id)
        })
    },


  }

}
</script>

<style lang="scss" scoped>
.mt-18 { margin-top: 4.5rem; }
.bg-pink { background-color: #F45B69; }
.pink {color: #F45B69;}
.green {color: #3E9E9C}


/* Date-ctk-picker */
label.field-label { display: none }

::v-deep {
  .field-input {
    border: solid 4px #99C9C5;
    background-color: #F4F3EE;
  }
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

input[type="text"], textarea {
  border: solid 4px #99C9C5;
}

input, select, textarea {
  -webkit-appearance: none;
  appearance: none;
  background-color: #F4F3EE;
}

input[type="checkbox"]::before {
  font-family: bootstrap-icons !important;
  content: "\f584";
  color: #99C9C5;
}

input[type="checkbox"]:checked::before {
  font-family: bootstrap-icons !important;
  content: "\f26c";
  color: #99C9C5;
}

::v-deep {
  .field-input {
    border: solid 4px #99C9C5;
  }
}


</style>
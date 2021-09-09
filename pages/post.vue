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
          :label="'締め切り'"
        ></Datetime>
      </div>

      <ul class="py-3">
        <li class="flex items-center">
          <!-- <i class="bi bi-hash text-2xl pr-1"></i> -->
          <img class="img pr-1" src="/hashtag_green_01.png" width="40" />
          <input class="px-3 py-1 rounded" type="text" placeholder=""/>
          <!-- <i class="bi bi-trash-fill text-xl pl-2 text-gray-400"></i> -->
          <img class="img pl-1" src="/trash_green_01.png" width="40" />
        </li>
      </ul>
      <div class="pb-4 text-gray-400 flex">
        <!-- <i class="bi bi-plus-circle pl-3 pr-1"></i> -->
        <img class="img pr-1" src="/plus_green_01.png" width="30" /> タグを追加する
      </div>

      <div class="py-2">
        <textarea rows="5" class="w-full p-2 rounded" placeholder="概要"></textarea>
      </div>

      <ul class="py-2">
        <li class="flex items-center">
          <input class="text-xl pr-2" type="checkbox"/>
          <input class="w-full px-2 py-1 rounded" type="text" placeholder="ToDo..."/>
        </li>
      </ul>
      <div class="pb-4 text-gray-400 flex">
        <!-- <i class="bi bi-plus-circle pl-3 pr-1"></i> -->
        <img class="img pr-1" src="/plus_green_01.png" width="30" />ToDoを追加する
      </div>


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
      deadline: ''
    }
  },

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

  padding: 0 .75rem;
  box-sizing: border-box;

  backdrop-filter: blur(5px);

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


</style>
<template>
  <div class="">
    <div class="header w-full h-14">
      <i class="bi bi-chevron-left text-2xl"></i>
      <div class="text-xl">保存</div>
    </div>
    <div class="content px-3 mt-16 mb-96 box-border flex flex-col">
      <div><input type="text" placeholder="タイトル" v-model="task.title"/></div>
      <div>
         <Datetime
          v-model="task.deadline"
          :minute-interval="5"
          :format="'YYYY-MM-DD HH:mm'"
          :overlay="true"
        ></Datetime>
      </div>
      <ul>
        <li><input type="text" placeholder="タグ" v-model="task.tag"/></li>
      </ul>
      <div><i class="bi bi-plus-circle"></i></div>
      <div><textarea name="" id="" cols="30" rows="10" placeholder="詳細" v-model="task.description"></textarea></div>
      <ul><li><input type="checkbox" /><input type="text" v-model="task.todo"/></li></ul>
      <div><i class="bi bi-plus-circle"></i></div>


    </div>
    
  </div>
</template>

<script>
import Datetime from 'vue-ctk-date-time-picker';
import '@/node_modules/vue-ctk-date-time-picker/dist/vue-ctk-date-time-picker.css';
export default {
  components: {
    Datetime
  },
 data () {
   return {
     task: {
       title: "",
       tag: "",
       descripition: "",
       deadline:""
     },
   }
 },
 methods: {
   submit () {
     let dbTasks = this.$fire.firestore.collection('tasks')
     dbTasks
       .add({
         title: this.task.title,
         tag:this.task.tag,
         description: this.task.description,
         deadline: this.task.deadline
       })
       .then(ref => {
         console.log('Add ID: ', ref.id)
       })
   },
 },
 
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
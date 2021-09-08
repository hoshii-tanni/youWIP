<template>
 <div class="page">
   <label>
     <span>
       タイトル
     </span>
     <input
       type="text"
       v-model="task.title"
     >
   </label>
   <label>
     <span>
       詳細
     </span>
     <input
       type="text"
       v-model="task.description"
     >
   </label>
   <label>
     <span>
       締め切り
     </span>
     <input
       type="date"
       v-model="task.deadline"
     >
   </label>
   <button
     type="button"
     @click="submit"
   >
     Submit
   </button>
 </div>
</template>

<script>
//import firebase from 'firebase'

export default {
 data () {
   return {
     task: {
       title: "",
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
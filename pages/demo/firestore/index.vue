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
   <button
     type="button"
     @click="getData"
   >
     getData
   </button>

   <button
     type="button"
     @click="getAllTodos"
   >
     getAllTodos
   </button>

   <div id="task.title" />
   <div id="task.description" />
   <div id="task.date" />
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
   getData () {
     let docTasks = this.$fire.firestore.collection('tasks').doc('sb541NagO4wZGLUqh1uz')
     docTasks
         .get()
         .then(function(doc) {
           document.getElementById("task.title").innerHTML = (doc.data().title)
           document.getElementById("task.description").innerHTML = (doc.data().description)
           document.getElementById("task.date").innerHTML = (doc.data().deadline)
         })
   },

    getAllTodos(){
      const db=this.$fire.firestore;
      db.collection("tasks").get().then(snapShot => {
        console.log(snapShot);
        //snapShot.forEach(doc =>{
        //  console.log(`id:${doc.id},title: ${doc.data().title}`);
        //})
      })
    },
 },
 
}
</script>
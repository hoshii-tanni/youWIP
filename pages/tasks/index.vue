<template>
  <div class="flex flex-col items-center">

    <div class="header">
      <img @click="$router.push('/tasks/new')" class="img" src="/plus_green_01.png" width="40" />
      <img class="img" src="/colored.png" />
      <img class="img" src="/timeline.png" width="40" />
    </div>

    <div class="content max-w-lg w-full px-3 mt-16 mb-96 box-border flex flex-col">
      <ul>
        <li v-for="(n,i) in tasks.length" :key="i" class="task flex flex-col my-2">
          <div v-if="tasks[i].image!=''" class="image" :style="'background-image: url(' + tasks[i].image + ');'"></div>
          <div class="mx-2 mt-2 flex justify-between items-end">
            <div class="text-xl font-bold">{{tasks[i].title}}</div>
            <img @click="clickEdit(tasks[i].post_id)" class="img" src="/edit.png" width="40" />
          </div>
          <div class="mx-2 my-1 pink underline">
            <ul class="flex">
              <li v-for="(n,j) in tasks[i].tags.length" :key="j" @click="clickTag(tasks[i].tags[j])" class="flex flex-col mr-2">
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
  transition(to, from) {
    if (to.path=="/tasks/new") return "to-right";
    if (from!=undefined && from.path=="/tasks/new") return "to-left";
    if (to.path=="/tasks/*") return "to-right";
    if (from!=undefined && from.path=="/tasks/*") return "to-left";
    
    return "fade";
  },

  data() {
    return {
      usr_id: "",
      tasks: [],

    }
  },

  created() {
    // cookieの取得とusr_idの設定
    let usr_id = this.$cookies.get("usr_id");
    if(usr_id==null) { usr_id = this.makeRandomUsrId(12); }

    this.usr_id = usr_id;
    this.$cookies.set("usr_id", usr_id, { path:"/", maxAge: 60 * 60 * 24 * 90 });

    // usr_id の一致するタスクを取得
    this.tasks = this.getTaskFromUsrId(this.usr_id);


    // テスト用task
    /*
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
    */
  },

  methods:{
    // 文字列の長さを引数に取り、ランダムな英数字列を返す
    makeRandomUsrId(length) {
      let c = "ABCDEFGHIJKLMNOPQRSTUVWXWZabcdefghijklmnopqrstuvwxyz0123456789";
      let cl = c.length;
      let result = "";
      for (var i = 0; i < length; i++) {
        result += c[Math.floor(Math.random() * cl)];
      }

      return result;
    },

    // タグクリック時に遷移する
    clickTag(tag) {
      this.$router.push("/tasks/" + tag);
    },

    // 編集画面に遷移する
    clickEdit(post_id) {
      this.$router.push({ path: '/tasks/update', query: {post_id: post_id} });
    },

    // タグからタスクを探す
    getTaskFromTag(tag){
      const db = this.$fire.firestore;
      let result = [];

      db.collection("tasks").where("tags","array-contains",tag).get().then(snapShot => {
        snapShot.forEach(doc =>{
          result.push(doc.data().todo);
        })
      })
    },

    // ユーザidからタスクを探す
    getTaskFromUsrId(usr_id){
      const db = this.$fire.firestore;
      let result = [];

      db.collection("tasks").where("usr_id","==",usr_id).get().then(snapShot => {
        snapShot.forEach(doc =>{
          let array = doc.data();
          array["post_id"] = doc.id;
          result.push(array);
        })
      })

      return result;
    },

    


  }

}
</script>

<style lang="scss">
.h−273 { height: 273px; }
.bg-pink { background-color: #F45B69; }
.pink {color: #F45B69;}


input, select, textarea {
  -webkit-appearance: none;
  appearance: none;
}

input[type='checkbox'] {
  appearance: none;
  outline: none;

  display: block;
  position: relative;
  text-align: center;
  cursor: pointer;

  width: 28px;
  height: 28px;
  margin-right: 10px;
}

input[type="checkbox"]::before {
  display: block;
  position: absolute;
  content: "";

  width: 28px;
  height: 28px;
  border: solid 3px #99C9C5;

  display: flex;
  justify-content: center;
}


input[type="checkbox"]::after {
  display: block;
  content: "";
  background-image: url(/check.png);
  background-size: contain;
  position: absolute;
  width: 40px;
  height: 40px;
  top: -3px;
  left: -5px;

  background-repeat: no-repeat;
  opacity: 0;
}

input[type="checkbox"]:checked:after {
    opacity: 1;
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
<!-- 以下 HTML ／ template直下はタグを1つしか置けない -->
<template>
  <div class="a p-2 box-border">
    <h1 class="bg-gray-300">Hello World</h1> <!-- デフォルトのh1スタイルが無効に -->
    <div @click="test()">val: {{ val }} (変数の呼び出し)</div>
    <div class="b p-4 my-2 font-bold" @click="$router.push('/demo/transition')">GO TO demo/transition</div>
    <div class="bg-green-100 p-4 my-2 font-bold" @click="$router.push('/demo/add_firestore')">GO TO demo/add_firestore</div>
  </div>
</template>


<!-- 以下 JavaScript -->
<script>
export default {
  layout: "default",

  // この中に、このクラス共通の変数を定義する(グローバル変数的な)。
  data() {
    return {
      null: null,
      val: 123,
      str: "文字列",
    }
  },

  // ここに利用する自作コンポーネントを定義する
  components: {

  },
  

  // DOM(上のHTML)構築 '前' に処理を行う
  // あまり使わないかも
  created() {

  },


  // DOM(上のHTML)構築 '直後' に処理を行う
  // 上のHTMLにアクセスする場合に利用
  mounted() {
    // this.$fire 〜 firebaseへアクセスできる
    // this.test()
  },


  // 関数(メソッド)を定義
  // mounted や methods で呼び出す際には、'this' が必要
  methods: {
    test() {
      alert("Hello World")
      this.log("Hello")
    },
    

    log(string) {
      let x = "World";

      console.log(this.str) // グローバル変数読み込み
      console.log(string) // 関数の引数の読み込み
      console.log(x) // ローカル変数の読み込み
    },
  },






}
</script>


<!-- 以下 CSS -->
<style lang="scss" scoped>
.a {
  .b {
    background-color: #888;
  }
}
</style>
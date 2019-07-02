
<template lang="pug">
  div(id="app")
    h1
      | ECHO SERVER
    input( name = "text" type="text" v-model="text" placeholder="文章を入力してください")
    button(v-on:click="submit")
      | 送信する
    p
      | 結果 : {{ this.result }}
    p
      | (C) Kota FUKUI
</template>
<script>

import axios from 'axios';

export default {
  name: 'app',
  data () {
    return {
      text: '',
      result: ''
    }
  },
  methods: {
    submit: function () {
      let params = new URLSearchParams();
      axios.post('http://18.222.190.215/api/', {
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        text: this.text
        })
        .then(response => {
          this.result = response.data["results"]
          console.log('送信したテキスト: ' + response.data.text);
        }).catch(error => {
          console.log(error);
        });
    }
  }
}

</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

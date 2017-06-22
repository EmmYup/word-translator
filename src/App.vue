<template>
  <div class="text-center" id="app">
    <h1>Word Translator</h1>
    <h5>Powered by Vue.js</h5>
    <TranslateForm @formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'

export default {
  name: 'app'
  ,components: {
    TranslateForm
    ,TranslateOutput
  }
  ,data: function() {
    return {
      translatedText: ''
    }
  }
  ,methods: {
    translateText: function(text,lenguage) {
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170622T123950Z.5e2797cf83fac5cc.7b198cbd7f02ee502a04c492cdb631722e55c58c&lang=' + lenguage + '&text=' + text)
      .then((response) => {
        this.translatedText = response.body.text[0];
      });
    }
  }
}
</script>

<style>
body{
  background: #fefefe;
}
</style>

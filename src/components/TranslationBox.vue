<template>
  <div class="translation-box-wrapper">
    {{ translated_text }}
  </div>
</template>

<script>
//Need this for axios to work in Internet Explorer, also needed to npm install @babel/polyfill
import "@babel/polyfill";

import axios from 'axios'

export default {
  name: 'TranslationBox',
  props: ["language", "text"],
  data () {
    return {
      translated_text: ''
    }
  },
  watch: {
    text(){
      /*
        Whenever the text is changed from the parent, translate the text
      */
      this.translateText();
    },
    language(){
      /*
        Whenever the language is changed from the parent, translate the text
      */
      this.translateText();
    }
  },
  methods: {
    translateText(){
      /*
        Make sure the text is not blank
      */
      if(this.text != ""){
        /*
          Let the user know we are translating the text
        */
        this.translated_text = "Translating..."

        /*
          Use Google Translate API to translate the text in the specified language
        */
        let this_vm = this;
        axios.get("https://translate.googleapis.com/translate_a/single?client=gtx&sl=en&tl=" + this.language + "&dt=t&q=" + this.text)
          .then(response => {
            /*
              Update the translated text with the data from Gogole Translate
            */
            this_vm.translated_text = response.data[0][0][0];
          })
          .catch(e => {
            console.log(e);
          })
      } else {
        /*
          If the text is blank, then make sure that the translation text is blank
        */
        this.translated_text = "";
      }
    }
  }
}
</script>

<style scoped>
  .translation-box-wrapper {
    min-height: 160px;
    padding: 20px;
    background-color: #F2F2F2;
    overflow: auto;
    border-bottom-right-radius: 5px;
  }
</style>

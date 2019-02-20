<template>
  <div id="app">
    <h3>Translation Tool</h3>
    <div class="header">
      <div>English</div>
      <div>
        <span>Translate to:</span>
        <select @change="languageChange($event)">
          <!--
            TODO:
            Bring in a list of languages plus their two digit code to populate this list
           -->
          <option value="fr">French</option>
          <option value="de">German</option>
          <option value="it">Italian</option>
          <option value="es">Spanish</option>
        </select>
      </div>
    </div>
    <div class="translations-wrapper">
      <div class="translate-boxes">
        <EnglishInput />
      </div>
      <div class="translate-boxes">
        <TranslationBox :language="language" :text="text" />
      </div>
    </div>
  </div>
</template>

<script>
import EnglishInput from './components/EnglishInput'
import TranslationBox from './components/TranslationBox'

export default {
  name: 'App',
  data () {
    return {
      language: 'fr',
      text: ''
    }
  },
  methods: {
    languageChange(event){
      /*
        Whenever the language is changed from the drop down selection,
        update the language
      */
      this.language = event.target.value;
    },
    updateText(new_text){
      /*
        Update the English text.
        This will come from the EnglishInput component
      */
      this.text = new_text
    }
  },
  components: {
    EnglishInput, TranslationBox
  }
}
</script>

<style>
  @media screen and (max-width: 600px) {
    #app {
      width: 100%;
      margin: 0;
    }

    .translations-wrapper {
      flex-direction: column;
    }

    .translate-boxes {
      width: 100%;
    }

    .header {
      font-size: 0.8em;
    }
  }

  @media screen and (min-width: 600px) {
    #app {
      width: 80%;
      margin: auto;
    }

    .translations-wrapper {
      flex-direction: row;
    }

    .translate-boxes {
      width: 50%;
    }

    .header {
      font-size: 1em;
    }
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    min-width: 300px;
  }

  .header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    border: 1px solid lightgray;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }

  .translations-wrapper {
    display: flex;
    border: 1px solid lightgray;
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
  }

  select {
    padding: 10px;
    border: none;
    border-radius: 4px;
    background-color: #f1f1f1;
  }
</style>

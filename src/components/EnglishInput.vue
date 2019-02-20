<template>
  <div class="english-box-wrapper">
    <textarea v-model="text" v-on:keyup="updateEnglishText()" placeholder="Type here to begin translating" ></textarea>
    <div v-show="text.length > 0" class="clear-text" @click="cleartext()"> X </div>
  </div>
</template>

<script>


export default {
  name: 'EnglishInput',
  data () {
    return {
      inputTimeout: null,
      text: ''
    }
  },
  methods: {
    updateEnglishText(){
      /*
        Whenever the user types something,
        send it to the parent
      */

      let this_vm = this;

      /*
        Have a timeout feature so that we don't translate every letter that is typed,
        but only when the user is finished typing.

        Clear the timeout if it has already been set.
        This will prevent the previous task from executing
        if it has been less than 500ms
      */
      clearTimeout(this.inputTimeout);

      /*
        Make a new timeout set to go off in 500ms
      */
      this.inputTimeout = setTimeout(() => {
          console.log('Input Value:', this_vm.text);
          /*
            Send the text to the parent method updateText()
          */
          this_vm.$parent.updateText(this_vm.text)
      }, 500);
    },
    cleartext(){
      /*
        Empty the text
      */
      this.text = '';

      /*
        Send the blank text to the parent so that the translation box will empty as well
      */
      this.$parent.updateText(this.text)
    }
  }
}
</script>

<style scoped>
  .english-box-wrapper {
    padding: 20px;
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
  textarea {
    width: 90%;
    min-height: 120px;
    border: none;
    outline: none;
    resize: none;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    font-size: 1em;
  }
  .clear-text {
    text-align: center;
    width: 20px;
    height: 20px;
  }
  .clear-text:hover {
    cursor: pointer;
  }
</style>

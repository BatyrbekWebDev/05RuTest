<template>
  <div class="flex flex-wrap">
    <button @click="undo" class="button">
        <i class="fa fa-rotate-left"></i>
    </button>
    <button @click="redo" class="button">
        <i class="fa fa-rotate-right"></i>
    </button>
    <button @click="applyBold" class="button">
        <i class="fa fa-bold"></i>
    </button>
    <button @click="applyItalic" class="button">
        <i class="fa fa-italic"></i>
    </button>
    <button @click="applyHeading" class="button">
        <i class="fa fa-header" aria-hidden="true"></i>
    </button>
    <button class="button" @click="copy">Скопировать HTML</button>
  </div>
  <div>
    <div
    
      @input="onInput"
      v-html="innerValue"
      contenteditable="true"
      ref="myInput"
      class="wysiwyg-output outline-none border-2 p-4 rounded-lg border-gray-300 focus:border-green-300"
    />
  </div>

</template> 

<script>
export default {
  name: 'WysiwygEditor',

  props: ['value'],
  data() {
    return {
      innerValue: this.value || '<p><br></p>',
    };
  },

  mounted() {
    document.execCommand('defaultParagraphSeparator', false, 'p');
  },

  methods: {
    
    onInput(event) {
      this.$emit('input', event.target.innerHTML);
    },
    applyBold() {
      document.execCommand('bold');
    },
    applyItalic() {
      document.execCommand('italic');
    },
    applyHeading() {
      document.execCommand('formatBlock', false, '<h1>');
    },
    applyUl() {
      document.execCommand('insertUnorderedList');
    },
    applyOl() {
      document.execCommand('insertOrderedList');
    },
    undo() {
      document.execCommand('undo');
    },
    redo() {
      document.execCommand('redo');
    },
    copy() {
      this.$refs.myinput.focus();
      document.execCommand('copy');
    }
  },
};
</script>

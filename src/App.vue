<template>
  <div id="app">
    <div class="container">
      <markdown-editor id="editor" v-model="input" />
      <markdown-previewer :input="input" />
    </div>
  </div>
</template>

<script>
import MarkdownEditor from './components/MarkdownEditor.vue';
import MarkdownPreviewer from './components/MarkdownPreviewer.vue';

export default {
  name: 'app',
  components: {
    MarkdownEditor,
    MarkdownPreviewer
  },
  data () {
    return {
      input: ''
    };
  }
};
</script>

<style lang="scss">
html,
body,
#app {
  height: 100%;
  font-family: 'Helvetica Neue', Arial, sans-serif;
}

@media print {
  #editor {
    display: none;
  }
}

.container {
  height: 100%;
  display: flex;

  > * {
    flex: 1;
    height: 100%;
    vertical-align: top;
    box-sizing: border-box;
  }
}
</style>

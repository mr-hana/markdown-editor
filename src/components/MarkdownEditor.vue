<template>
  <div class="editor" @dragleave.prevent @dragover.prevent @drop.prevent="onDrop">
    <markdown-exporter :text="value" />
    <input type="file" @change="onDrop" style="display:none;">
    <textarea :value="text" @input="onUpdate"></textarea>
  </div>
</template>

<script>
const _ = require('lodash');
import MarkdownExporter from './MarkdownExporter.vue';

export default {
  props: ['value'],
  data: function () {
    return {
      text: this.value
    }
  },
  components: { MarkdownExporter },
  methods: {
    onUpdate: _.debounce(function (e) {
      this.text = e.target.value
      this.$emit('input', e.target.value)
    }, 300),
    onDrop: function (e) {
      let file = e.dataTransfer.files[0]
      let vm = this;
      let reader = new FileReader();
      reader.onload = function () {
        vm.text = reader.result
        vm.$emit('input', vm.text)
      }

      reader.readAsText(file);
    }
  }
}
</script>

<style lang="scss" scoped>
.editor {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  background-color: #f6f6f6;
  padding: 5px 5px 15px 10px;
  border-right: 1px solid #ccc;
}

textarea {
  height: 100%;
  color: #333;
  background: transparent;
  border: none;
  resize: none;
  outline: none;
  font-size: 14px;
  font-family: 'Monaco', courier, monospace;
}
</style>

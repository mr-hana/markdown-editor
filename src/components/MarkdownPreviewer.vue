<template>
  <div class="wrapper">
    <html-exporter :body="compiledMarkdown" />
    <div id="markdown-preview" v-html="compiledMarkdown"></div>
  </div>
</template>

<script>
const marked = require("marked");
import HtmlExporter from './HtmlExporter.vue';

export default {
  props: ['input'],
  components: { HtmlExporter },
  computed: {
    compiledMarkdown: function () {
      return marked(this.input, { sanitize: true });
    }
  }
};
</script>

<style>
.wrapper {
  height: 100%;
  overflow: auto;
  padding: 5px 10px 15px 5px;
}
</style>


<style lang="scss" scoped>
#markdown-preview /deep/ {
  $border-color: #666;

  max-width: 900px;
  margin: 0 auto;
  padding: 25px;
  color: black;
  h1,
  h2,
  h3,
  h4,
  h5 {
    font-weight: normal;
    border-color: $border-color;
  }
  h1 {
    font-size: 35px;
    border: none;
    margin: 30px auto;
    text-align: center;
    letter-spacing: 5px;
  }
  h2 {
    font-size: 25px;
    letter-spacing: 3px;
    margin: 50px auto 25px;
    padding-bottom: 10px;
    border-bottom: solid 2px $border-color;
  }
  h3 {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 10px;
  }
  p,
  table,
  ul,
  ol,
  dl,
  pre,
  blockquote {
    margin-left: 25px;
    ul,
    ol,
    dl {
      margin-left: 0px;
    }
  }
  table {
    border-collapse: collapse;
    border-spacing: 0;
    max-width: 800px;
    tr {
      border-top: #666;
    }
    th {
      text-align: center;
      background-color: #ccc;
      border: solid 1px $border-color;
      padding: 8px 10px;
    }

    td {
      border: solid 1px $border-color;
      padding: 5px;
    }
    tr:nth-child(2n) {
      background: #eee;
    }
  }
  .margin-clear {
    margin-left: 0;
  }
  // テキストの中央揃え
  .center {
    text-align: center;
    @extend .margin-clear;
  }
  // テキストの右寄せ
  .right {
    text-align: right;
    @extend .margin-clear;
  }
}
</style>


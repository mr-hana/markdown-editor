<template>
  <div>
    <button @click="handleDownload">
      <i class="far fa-file-code fa-lg"></i>
    </button>
  </div>
</template>

<script>
export default {
  props: ['body'],
  methods: {
    handleDownload: function () {
      var html = generateHtml(this);
      var blob = new Blob([html.outerHTML], { type: "text/plain" });
      if (window.navigator.msSaveBlob) {
        window.navigator.msSaveBlob(blob, currentDatetime());
      } else {
        var a = document.createElement("a");
        a.href = URL.createObjectURL(blob);
        a.target = '_blank';
        a.download = currentDatetime();
        a.click();
        URL.revokeObjectURL(a.href);
      }
    }
  }
}

function currentDatetime () {
  var date = new Date();
  var yyyy = date.getFullYear();
  var mm = ('0' + (date.getMonth() + 1)).slice(-2);
  var dd = ('0' + date.getDate()).slice(-2);
  var hh = ('0' + date.getHours()).slice(-2);
  var mi = ('0' + date.getMinutes()).slice(-2);
  var ss = ('0' + date.getSeconds()).slice(-2);
  return yyyy + mm + dd + hh + mi + ss + '.html';
}

function generateHtml (vueObj) {
  let html = document.createElement('html');
  let head = document.createElement('head');
  html.appendChild(head);
  let styles = document.getElementsByTagName('style');
  Array.prototype.forEach.call(styles, function (item) {
    let css = item.innerHTML || item.innerText;
    if (0 < css.indexOf('markdown-preview')) {
      let style = document.createElement('style')
      style.type = item.type;
      style.innerHTML = css;
      head.appendChild(style);
    }
  });

  let body = document.createElement('body');
  html.appendChild(body);
  let div = document.createElement('div');
  body.appendChild(div);
  div.id = 'markdown-preview';
  let dataKey = Object.keys(vueObj.$parent.$el.dataset)[0];
  div.dataset[dataKey] = '';
  div.innerHTML = vueObj.body;
  return html;
}
</script>

<style lang="scss" scoped>
div {
  padding: 5px;
}
button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  outline: none;
  padding: 0;
  :hover {
    color: #999;
  }
}
</style>


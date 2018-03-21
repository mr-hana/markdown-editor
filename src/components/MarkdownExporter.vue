<template>
  <div>
    <button @click="handleDownload">
      <i class="fas fa-cloud-download-alt fa-lg"></i>
    </button>
  </div>
</template>

<script>
export default {
  props: ['text'],
  methods: {
    handleDownload: function () {
      var blob = new Blob([this.text], { type: "text/plain" });
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
  return yyyy + mm + dd + hh + mi + ss + '.md';
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


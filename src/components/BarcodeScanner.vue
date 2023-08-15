<template>
  <div id="qr-code-full-region"></div>
</template>

<script>
  import { defineComponent } from 'vue'
  //import { App } from '../App.vue'

  export default defineComponent({
    name: 'qrcode-scanner',
    props: {
      qrbox: Number,
      fps: Number,
    },

    mounted: function () {
      var $this = this;
      var config = { fps: this.fps ? this.fps : 10 };
      if (this.qrbox) {
        config['qrbox'] = this.qrbox;
      }

      function onScanSuccess(decodedText, decodedResult) {
        $this.$root.$emit('decodedCode', decodedText, decodedResult);
      }

      var html5QrcodeScanner = new Html5QrcodeScanner(
        "qr-code-full-region", config);
      html5QrcodeScanner.render(onScanSuccess);
    }
  });


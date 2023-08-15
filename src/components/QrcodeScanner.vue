<template>
  <div id="qr-code-full-region"></div>
</template>

<script setup>
  import { toRefs,onMounted } from 'vue'
  import { Html5QrcodeScanner } from 'html5-qrcode';

  const props= defineProps({
                  qrbox: {type: [Number,Object,Function]},
                  fps: Number,
                  rememberLastUsedCamera: {type: Boolean, default: true}
                });
  const emit = defineEmits(['result']);
  function onScanSuccess(decodedText, decodedResult) {
      console.log('QrcodeScanner onScanSuccess',decodedResult,this)
      this.clear()
      emit('result', decodedText, decodedResult);
  }

  onMounted(() => {
    const { fps,qrbox,rememberLastUsedCamera } = toRefs(props)

    var config = {rememberLastUsedCamera:rememberLastUsedCamera.value}
    config['fps'] = fps.value ? fps.value : 10
    if (qrbox.value) {
        config['qrbox']=qrbox.value
    }

    var html5QrcodeScanner = new Html5QrcodeScanner("qr-code-full-region", config);
    html5QrcodeScanner.render(onScanSuccess.bind(html5QrcodeScanner));
  });

</script>
<script>
export default {
  name: 'QrcodeScanner',
}

</script>

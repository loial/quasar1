<template>
  <q-page class="flex flex-center">
    <QrcodeScanner v-if="!result"
        :qrbox="{width:400,height:200}"
        :fps="100"
        style="width: 500px;"
        @result="setResult"

    />
    <div v-if="result">
      {{result}}
      <q-btn
          label="Clear"
          @click="clearResult"
      />
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import QrcodeScanner from 'components/QrcodeScanner.vue';

export default defineComponent({
  name: 'BarcodeScanner',
  components: {
    QrcodeScanner
  },
  data: function() {return {
    header: 'Html5-qrcode using vue.js',
    result: ''
  }},
  methods: {
  mounted: function () {
  },
    setResult: function (data) {
      this.result=data
  },
    clearResult: function () {
      this.result=''
    }
  }
  })
</script>

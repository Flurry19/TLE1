<template>
    <div class="flex">
        <div class="justify-around">
            <StreamBarcodeReader
            @decode="(a, b, c) => onDecode(a, b, c)"
            @loaded="() => onLoaded()"

            ></StreamBarcodeReader>
            Input Value: {{ text || "Nothing" }}
        </div>
    </div>
  </template>

  <script>
  import { StreamBarcodeReader } from "vue-barcode-reader";
import router from "../router";

  export default {
    name: "ScannerComp",
    components: {
      StreamBarcodeReader,
    },
    data() {
      return {
        text: "",
        id: null,
      };
    },
    props: {
      msg: String,
    },
    methods: {
      onDecode(a, b, c) {
        console.log(a, b, c);
        router.push({ name: 'productpage', params: { barcode: a } })
        this.text = a;
        if (this.id) clearTimeout(this.id);
        this.id = setTimeout(() => {
          if (this.text === a) {
            this.text = "";
          }
        }, 5000);
      },
      onLoaded() {
        console.log("load");
      },
    },
  };
  </script>

  <style scoped>
  </style>

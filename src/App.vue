<template>
  <div id="app">
    <canvas width="1000" height="800" id="c"></canvas>
  </div>
</template>

<script>
import { fabric } from 'fabric'
import demoImg from './images/demo.png'

export default {
  name: 'app',
  data () {
    return {
    }
  },
  mounted () {
    const canvas = new fabric.Canvas('c')

    fabric.Image.fromURL(demoImg, (oImg) => {
      canvas.add(red)
      canvas.add(oImg)
      canvas.add(text40)

      this.saveImage(canvas.toDataURL({
        format: 'jpeg'
      }))
    })

    var red = new fabric.Rect({
      top: 100, left: 0, width: 80, height: 50, fill: 'gray'
    })

    var text40 = new fabric.Text("一\n群\n死\n宅", {
      fontSize: 40
    })
  },
  methods: {
    saveImage(yourDataURL) {
      function dataURIToBlob(dataURI, callback) {
        var binStr = atob(dataURI.split(',')[1]),
          len = binStr.length,
          arr = new Uint8Array(len)

        for (var i = 0; i < len; i++) {
          arr[i] = binStr.charCodeAt(i)
        }

        callback(new Blob([arr]))
      }

      var callback = function(blob) {
        var a = document.createElement('a')
        a.download = 'test.jpeg'
        a.innerHTML = 'download'
        a.href = URL.createObjectURL(blob);
        document.body.appendChild(a)
      }

      dataURIToBlob(yourDataURL, callback);
    }
  }
}
</script>

<style lang="css">

</style>
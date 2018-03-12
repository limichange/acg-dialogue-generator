<template>
  <div id="app">
    <canvas width="1000" height="800" id="c"></canvas>
    <button @click="addText">添加文本</button>
  </div>
</template>

<script>
import { fabric } from 'fabric'
import demoImg from './images/demo.png'
import demo2Img from './images/demo2.png'

export default {
  name: 'app',
  data () {
    return {
      canvas: {}
    }
  },
  mounted () {
    const canvas = new fabric.Canvas('c')

    this.canvas = canvas

    fabric.Image.fromURL(demo2Img, img => {
      canvas.add(img)
    })

    fabric.Image.fromURL(demoImg, (oImg) => {
      canvas.add(red)
      canvas.add(oImg)
      canvas.add(text40)
      canvas.add(text2)

      this.saveImage(canvas.toDataURL({
        format: 'jpeg'
      }))
    })

    var red = new fabric.Rect({
      top: 100, left: 0, width: 80, height: 50, fill: 'gray'
    })

    var text40 = new fabric.IText("老子天下第一👌", {
      fontFamily: 'arial black',
      fontSize: 20
    })

    var text2 = new fabric.IText("我是不信的", {
      fontFamily: 'arial black',
      fontSize: 30
    })
  },
  methods: {
    addText () {
      const text = new fabric.IText("老子天下第一👌", {
        fontFamily: 'arial black',
        fontSize: 20
      })

      this.canvas.add(text)
    },
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
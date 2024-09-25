<template>
    <div>
      <video ref="videoPlayer" controls style="width: 100%;"></video>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, onBeforeUnmount, watch } from 'vue'
  import Hls from 'hls.js'
  
  const props = defineProps({
    streamUrl: {
      type: String,
      required: true
    }
  })
  
  const videoPlayer = ref(null)
  let hls
  
  const setupHls = (url) => {
    if (Hls.isSupported()) {
      if (hls) {
        hls.destroy() 
      }
      hls = new Hls()
      hls.loadSource(url)
      hls.attachMedia(videoPlayer.value)
      hls.on(Hls.Events.MANIFEST_PARSED, function () {
        videoPlayer.value.play()
      })
    } else if (videoPlayer.value.canPlayType('application/vnd.apple.mpegurl')) {
      videoPlayer.value.src = url
      videoPlayer.value.addEventListener('loadedmetadata', () => {
        videoPlayer.value.play()
      })
    }
  }
  
  onMounted(() => {
    setupHls(props.streamUrl)
  })
  
  onBeforeUnmount(() => {
    if (hls) {
      hls.destroy()
    }
  })
  
  watch(() => props.streamUrl, (newUrl) => {
    setupHls(newUrl)
  })
  </script>
  
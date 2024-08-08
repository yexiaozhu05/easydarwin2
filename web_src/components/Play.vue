<template>
  <body>
  <video id="video"></video>
  </body>
</template>
<script>
import {} from '../externals/js/adapter.min.js'
import { WebRtcStreamer } from '../externals/js/webrtcstreamer.js'
var webRtcServer      = null;
window.onload         = function() {
  videoEle = document.getElementById("video")
  console.log(window.innerHeight)
  videoEle.style.width = window.innerWidth
  videoEle.style.height = window.innerHeight
  webRtcServer      = new WebRtcStreamer("video",location.protocol+"//"+location.hostname+":9005");
  var videoUrl="rtsp://10.4.196.91/lg001/172.20.207.50_01_20240620102719238.mp4";
  var audioUrl="";
  var options="rtptransport=tcp&timeout=60";
  webRtcServer.connect(videoUrl, audioUrl, options);
}
window.onbeforeunload = function() { webRtcServer.disconnect(); }
</script>
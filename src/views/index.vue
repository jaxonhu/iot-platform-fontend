<template>
  <div class="terminal">
    <i class="fa fa-cog"></i>
    智能设备demo
    <i class="fa fa-wrench"></i>
    <br>
    <!-- <i class="fa fa-terminal"></i>
    <code>npm start</code>
    <i class="fa fa-cog"></i>
    <i class="fa fa-wrench"></i>
    <i class="fa fa-puzzle-piece"></i>
    <i class="fa fa-gavel"></i>
    <i class="fa fa-coffee"></i>
    <br>
    <i class="fa fa-terminal"></i>
    <code>npm run build</code>
    <i class="fa fa-hourglass-start"></i>
    <i class="fa fa-hourglass-half"></i>
    <i class="fa fa-hourglass-end"></i>
    <i class="fa fa-beer"></i>
    <br>
    <i class="fa fa-magic"></i>
    两个命令玩转 <code>Vue</code>
    <i class="fa fa-hand-o-left"></i>
    <i class="fa fa-smile-o"></i>
    <i class="fa fa-hand-peace-o"></i>
    <i class="fa fa-flag-checkered"></i> -->
  </div>
</template>
<script>

// import Stomp from '../../static/plugins/stomp.min.js'
// import SockJs from '../../static/plugins/sockjs.min.js'

// import Stomp from 'stompjs'
import SockJs from 'sockjs-client'

var Stomp = require('stompjs')

export default {
  data: () => ({
    // websock: null,
    // stompClient: null
  }),
  created() {
    this.initWebSocket()
  },
  destoryed: function() {
    // this.websocketclose()
  },
  methods: {
    initWebSocket() {
      var websock = new SockJs('http://127.0.0.1:8081/websocket')
      var stompClient = Stomp.over(websock)
      stompClient.connect({}, function(frame) {
        console.log('连接成功' + frame)
        stompClient.subscribe('/app/1/queue/getResponse', response => {
          console.log(response.body)
        })
      })      
    },
    websocketclose() {
      if (this.stompClient !== null) {
        this.stompClient.disconnect()
      }
      console.log('连接关闭')
    }
  }
}
</script>


<style>
.terminal {
  padding: 30px;
  font-size: 3em;
  color: #a6e22e;
  text-align: center;
  background-color: #23241f;
}
</style>

<template>
      <div id="xterm" class="xterm" ></div>
</template>

<script>
// @ is an alias to /src
import { Terminal } from 'xterm'; 
import { FitAddon } from 'xterm-addon-fit'
import { AttachAddon } from 'xterm-addon-attach'

export default {
  name: 'Terminal',

  props: {
    socketURI: {
      type: String,
      default: 'ws://127.0.0.1:8090/ws/1'
    }
  },
  mounted() {
    this.initSocket(); 
  }, 
  beforeDestroy() {
    this.socket.onClose()
    this.term.dispose()
  },
  methods: {
    initTerm() {
      const term = new Terminal({
        fontSize: 14,
        cursorBlink: true
      });
      const attachAddon = new AttachAddon(this.socket);
      const fitAddon = new FitAddon();
      term.loadAddon(attachAddon);
      term.loadAddon(fitAddon);
      term.open(document.getElementById('xterm'));
      fitAddon.fit();
      term.focus();
      this.term = term
    },
    initSocket(){
      this.socket = new WebSocket(this.socketURI); 
      this.initTerm()
      this.onClose();
      this.onOpen();
      this.onError();
    }, 
    onOpen(){
      this.socket.onOpen = () => {
        this.initTerm();
      }
    },
    onClose(){
      this.socket.onClose = () => {
        console.log("socket close"); 
      }

    },
    onError(){
      this.socket.onError = () => {
        console.error("error");
      }
    }

  }

}
</script>

<template>
  <div ref="video-chat-container" class="embed-response embed-responsive-16by9">
    <video
      id="video"
      ref="video"
      class="embed-responsive-item"
      autoplay="autoplay"
    ></video>
  </div>
</template>

<script>
import { mapActions, mapState } from 'vuex'

export default {
  name: 'Webcam',
  data() {
    return {
      iceServers: [
        { urls: 'stun:stun.l.google.com:19302' },
        { urls: 'stun:stun1.l.google.com:19302' },
        { urls: 'stun:stun2.l.google.com:19302' },
        { urls: 'stun:stun3.l.google.com:19302' },
        { urls: 'stun:stun4.l.google.com:19302' },
      ],
    }
  },
  computed: {
    ...mapState(['user', 'warzone']),
  },
  watch: {
    warzone(value) {
      this.text = value
    },
  },
  mounted() {
    if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
      navigator.mediaDevices.getUserMedia({ video: true }).then((stream) => {
        this.$refs.video.srcObject = stream
        this.$refs.video.play()
        // this.setVideo(this.$refs.video)
      })
    }
  },
  methods: {
    ...mapActions(['setVideo']),
  },
}
</script>

<template>
  <div>
    <video controls class="video">
      <source src="http://localhost:3000/api/video?video=test.mp4" type="video/mp4">
      <p>Votre navigateur ne supporte pas la vidéo HTML5. Voici à la place <a href="rabbit320.mp4">un lien vers la vidéo</a>.</p>
    </video>
  </div>
</template>

<script>
import VideoPlayer from '@/components/Home/video.vue';

export default {
  name: 'VideoExample',
  components: {
    VideoPlayer
  },
  data() {
    return {
      videoOptions: {
        autoplay: true,
        controls: true,
        sources: [
          {
            src:
              './test.mp4',
              type: 'video/mp4'
          }
        ]
      }
    };
  }
};
</script>

<style>

.video {
  width: 100%;
  height: 100%;
}
</style>
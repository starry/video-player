<template>
  <div class="video-player">
    <video
      ref="video"
      class="vjs-custom video-js"
      controls
      x-webkit-airplay="true"
      webkit-playsinline="true"
      x5-playsinline="true"
      :x5-video-player-type="type"
      playsinline="true">
    </video>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

import videojs from 'video.js';
import 'video.js/dist/video-js.min.css';
@Component
export default class HelloWorld extends Vue {

    /** 视频地址 */
    @Prop()
    public src!: string;

    /** 视频封面 */
    @Prop()
    public poster!: string;

    /** android video 是否 x5 */
    @Prop()
    public type!: string;

    /** vidoe */
    public player!: videojs.Player;

    /** video配置选项 */
    public options?: videojs.PlayerOptions;

    /** 默认事件 */
    public events: string[] = [
    'pause',
    'waiting',
    'playing',
    'ended',
    'error',
    'fullscreenchange',
    ];

    public mounted() {
        this.player = videojs(this.$refs.video, this.options, () => {
          for (const event of this.events) {
            this.player.on(event, () => {
              this.$emit(event, this.player);
            });
          }
        });
    }

    public created() {
        this.options = {
            src: this.src,
            poster: this.poster,
            language: 'en',
            fluid: true,
            preload: 'auto',
            width: document.documentElement ? document.documentElement.clientWidth : 375,
            sources: [
              {
                type: 'video/mp4',
                src: this.src,
              },
            ],
            controlBar: {},
        };
    }
}
</script>

<style>
.video-js .vjs-menu-button-inline.vjs-slider-active,
.video-js .vjs-menu-button-inline:focus,
.video-js .vjs-menu-button-inline:hover,
.video-js.vjs-no-flex .vjs-menu-button-inline {
  width: 10em;
}

.video-js .vjs-controls-disabled .vjs-big-play-button {
  display: none !important;
}

.video-js .vjs-control {
  width: 3em;
}

.video-js .vjs-menu-button-inline:before {
  width: 1.5em;
}

.vjs-menu-button-inline .vjs-menu {
  left: 3em;
}

.vjs-paused.vjs-has-started.video-js .vjs-big-play-button,
.video-js.vjs-ended .vjs-big-play-button,
.video-js.vjs-paused .vjs-big-play-button {
  display: block;
}

.video-js .vjs-load-progress div,
.vjs-seeking .vjs-big-play-button,
.vjs-waiting .vjs-big-play-button {
  display: none !important;
}

.video-js .vjs-mouse-display:after,
.video-js .vjs-play-progress:after {
  padding: 0 0.4em 0.3em;
}

.video-js.vjs-ended .vjs-loading-spinner {
  display: none;
}

.video-js.vjs-ended .vjs-big-play-button {
  display: block !important;
}

video-js.vjs-ended .vjs-big-play-button,
.video-js.vjs-paused .vjs-big-play-button,
.vjs-paused.vjs-has-started.video-js .vjs-big-play-button {
  display: block;
}

.video-js .vjs-big-play-button {
  top: 50%;
  left: 50%;
  margin-left: -1.5em;
  margin-top: -1em;
}

.video-js .vjs-big-play-button {
  background-color: rgba(0, 0, 0, 0.4);
  border: none;
  font-size: 3em;
  border-radius: 50%;
  height: 2em !important;
  line-height: 2em !important;
  margin-top: -1em !important;
}

.video-js:hover .vjs-big-play-button,
.video-js .vjs-big-play-button:focus,
.video-js .vjs-big-play-button:active {
  background-color: rgba(0, 0, 0, 0.4);
}

.video-js .vjs-loading-spinner {
  border-color: rgba(255, 255, 255, 0.7);
}

.video-js .vjs-control-bar2 {
  background-color: transparent;
}

.video-js .vjs-control-bar {
  background-color: linear-gradient(
    rgba(0, 0, 0, 0),
    rgba(0, 0, 0, 0.7)
  ) !important;
  color: #ffffff;
  font-size: 14px;
  transition: opacity 0.4s ease-in-out, transform 0.4s ease-in-out;
}

.video-js .vjs-play-progress,
.video-js .vjs-volume-level {
  background-color: #2483d5;
}

.video-js .vjs-big-play-button {
  height: 2em !important;
  width: 2em !important;
  line-height: 2em !important;
  margin-top: -1em !important;
  margin-left: -1em;
  border-width: 3px;
}

.video-js .vjs-icon-play:before,
.video-js .vjs-big-play-button:before {
  font-size: 50px;
}

.video-js .vjs-progress-holder {
  font-size: 1.7em;
  border-radius: 10px;
}

.video-js .vjs-progress-holder .vjs-play-progress,
.video-js .vjs-progress-holder .vjs-load-progress,
.video-js .vjs-progress-holder .vjs-load-progress div,
.video-js .vjs-slider,
.vjs-volume-level {
  border-radius: 10px;
}

.video-js .vjs-load-progress {
  background: rgba(255, 255, 255, 0.5);
}
</style>

<template>
  <div id="app">
    <SmipleVuePlayer
      :src="src"
      :poster="poster">
    </SmipleVuePlayer>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import SmipleVuePlayer from './components/smipleVuePlayer.vue';

@Component({
  components: {
    SmipleVuePlayer,
  },
})
export default class App extends Vue {

  public src: string = '//1251741799.vod2.myqcloud.com/9b0fbfcdvodgzp1251741799/1811f39c7447398156428815489/XheTZszonSIA.mp4';

  public poster: string = '//y.gtimg.cn/music/photo_new/T002R300x300M000002oqIsq2cHiv6.jpg';
}
</script>

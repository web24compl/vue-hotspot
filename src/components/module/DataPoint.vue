<template>
  <div class="ui__vue_hotspot_hotspot"
    :style="`top: ${positionTop}; left: ${positionLeft}; background-color: ${hotspotColor};`"
    :class="isActive || interactivity === 'none' ? 'active' : ''"
    @mouseenter="interactivity === 'hover' ? isActive=true : null"
    @mouseleave="interactivity === 'hover' ? isActive=false : null"
    @click="interactivity === 'click' ? toggleActive() : null">
    <!-- message box -->
    <div :style="`color:${textColor}`">
      <div
        class="ui__vue_hotspot_title"
        :style="`
          background: ${messageBoxColor};
          opacity: ${opacity}
          height:${config.editable ? '40px' : '20px'}
          `"

      >
        {{ hotspot['Title'] }}
        <div v-if="config.editable" style="display:flex;width:100%;justify-content: flex-start;">
          <a @click="handleDelete" role="button">Usuń</a>
          <a @click="handleEdit" role="button">Edytuj</a>
        </div>
      </div>
      <div
        class="ui__vue_hotspot_message"
        :style="`
          background: ${messageBoxColor};
          opacity: ${opacity}`"
      >
        {{ hotspot['Message'] }}
      </div>
    </div>
  </div>
</template>

<script>
import { throttle } from '../utils/common.js'
import {
  createComponent,
  ref,
  reactive,
  toRefs,
  onMounted,
  onUnmounted,
  computed,
  watch
} from '@vue/composition-api'

export default createComponent({
  props: {
    hotspot: Object,
    config: Object,
    imageLoaded: Boolean,
    vueHotspotBackgroundImage: HTMLImageElement,
    vueHotspot: HTMLDivElement
  },
  setup (props, { emit }) {
    const isActive = ref(false)
    const conf = reactive({
      positionTop: 0,
      positionLeft: 0,
      hotspotColor: computed(() => props.config && props.config.hotspotColor),
      interactivity: computed(() => props.config && props.config.interactivity),
      textColor: computed(() => props.config && props.config.textColor),
      messageBoxColor: computed(() => props.config && props.config.messageBoxColor),
      opacity: computed(() => props.config && props.config.opacity),
      isMain: computed(() => props.hotspot && props.hotspot.isMain)
    })

    watch(() => props.imageLoaded, (loaded, prev) => {
      if (loaded) {
        getHotspotStyle()
      }
    })

    onMounted(() => {
      window.addEventListener('resize', throttle(getHotspotStyle, 50))
    })

    onUnmounted(() => {
      window.removeEventListener('resize', throttle(getHotspotStyle, 50))
    })

    function getHotspotStyle () {
      conf.positionTop = `${((props.hotspot.y * props.vueHotspotBackgroundImage.clientHeight / 100) + (props.vueHotspotBackgroundImage.offsetTop - props.vueHotspot.clientTop))}px;`
      conf.positionLeft = `${(props.hotspot.x * props.vueHotspotBackgroundImage.clientWidth / 100) + (props.vueHotspotBackgroundImage.offsetLeft - props.vueHotspot.clientLeft)}px;`
    }

    function toggleActive () {
      isActive.value = !isActive.value
    }

    function handleEdit () {
      emit('edit')
    }

    function handleDelete () {
      emit('delete')
    }

    return {
      // data
      isActive,
      ...toRefs(conf),
      handleEdit,
      handleDelete,
      // methods
      getHotspotStyle,
      toggleActive
    }
  }
})
</script>

<style scoped>
/* CSS class for hotspot data points */
.ui__vue_hotspot_hotspot {
  height: 20px;
  width: 20px;
  position: absolute;
  border-radius: 50%;
  cursor: pointer;
  z-index: 200;
  margin-left: -10px;
  margin-top: -10px;
}
.ui__vue_hotspot_hotspot > div {
  position:absolute;
  width: 140px;
  height: 120px;
  top:-30px;
  margin: -104px -60px;
  border-radius: 4px;
  overflow: hidden;
  font-size: 10px;
  display: none;
}
.ui__vue_hotspot_hotspot.active > div {
  display: block; /* Required */
}
/*.ui__vue_hotspot_hotspot.active > div:before {*/
/*  border: solid transparent;*/
/*  content: ' ';*/
/*  height: 0;*/
/*  left: 0;*/
/*  position: absolute;*/
/*  width: 0;*/
/*  border-width: 10px;*/
/*  border-left-color: rgba(255, 255, 255, 0.4);*/
/*  transform: rotate(90deg);*/
/*  top: -10px;*/
/*}*/
.ui__vue_hotspot_hotspot > div > .ui__vue_hotspot_title {
  /*height: 40px;*/
  line-height: 20px;
  font-weight: bold;
  padding: 4px 10px;
  transition: opacity 0.2s ease-in;
}
.ui__vue_hotspot_hotspot > div > .ui__vue_hotspot_message {
  margin-top: 2px;
  padding: 10px 10px;
  height: 120px;
  overflow-y: auto;
  transition: opacity 0.2s ease-in;
}
</style>

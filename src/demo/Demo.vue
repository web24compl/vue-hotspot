<template>
  <main>
    <img style="max-width: 80%" alt="Vue logo" src="./assets/logo.png"/>
    <h1><a href="https://github.com/jamesxwang/vue-hotspot">Vue-Hotspot</a></h1>
    <p class="desc">Hotspot component for Vue.js.</p>

    <section v-for="(item, i) in hotspots" :key="i">
      <div class="container">
        <!-- Title -->
        <div class="text mb-sm">
          <span class="bold">Example {{ i + 1 }}</span>
        </div>
        <!-- Main -->
        <v-hotspot
          :init-options="item"
          save-buton-text="Bagno"
          @save-data="saveData"
          @after-delete="afterDelete"/>
        <div class="text">
          Editable: {{ item.editable }} | interactivity: {{ item.interactivity }} | hotspotCurves: {{
            item.hotspotCurves
          }}
        </div>
        <!-- Button -->
        <toggle
          :label="'Change Editable'"
          :hotspot-config="item"
          @change-editable="changeEditable"/>
      </div>
    </section>

    <footer>
      <!-- eslint-disable-next-line -->
      <a href="//github.com/jamesxwang">@James Wang</a>|<a
      href="//github.com/jamesxwang/vue-hotspot/blob/master/LICENSE">MIT License</a>|<a
      href="//github.com/jamesxwang/vue-hotspot">View on GitHub</a>
    </footer>
  </main>
</template>

<script>
import VueHotspot from '../components/VueHotspot.vue'
import Toggle from './components/Toggle.vue'

export default {
  components: {
    'v-hotspot': VueHotspot,
    toggle: Toggle
  },
  data () {
    return {
      hotspots: [
        {
          image: 'http://youimg1.c-ctrip.com/target/tg/154/775/815/aea886e20493478a9c2f628d86e34cfc.jpg',
          editable: true,
          interactivity: 'click',
          hotspotCurves: false
        },
        {
          image: 'http://youimg1.c-ctrip.com/target/100ghk1433p0arl5c3A3B.jpg',
          editable: false,
          interactivity: 'click',
          hotspotCurves: false
        },
        {
          image: 'http://5b0988e595225.cdn.sohucs.com/images/20171109/920c1cdc5d294a0eb2e17f2b9e731542.jpeg',
          editable: false,
          interactivity: 'hover',
          hotspotCurves: false,
          data: [
            { Message: 'A prepopulated hotspot with custom color', Title: 'Vue Hotspot 1', x: 33.3973, y: 58.3333 },
            {
              Message: 'Another prepopulated hotspot with custom color',
              Title: 'Vue Hotspot 2',
              x: 53.3973,
              y: 78.3333
            },
            {
              Message: 'Another prepopulated hotspot with custom color',
              Title: 'Vue Hotspot 3',
              x: 73.3973,
              y: 28.3333
            }
          ],
          hotspotColor: '#85ce61',
          messageBoxColor: '#409eff',
          textColor: '#333'
        },
        {
          image: 'http://pic.rmb.bdstatic.com/a2aa78b5e58cefb983dc2b9ea0ff9910.jpeg',
          editable: false,
          interactivity: 'none',
          hotspotCurves: false,
          data: [
            {
              Message: 'A prepopulated hotspot with interactivity: none',
              Title: 'Vue Hotspot 1',
              x: 33.3973,
              y: 68.3333
            },
            {
              Message: 'Another prepopulated hotspot with interactivity: none',
              Title: 'Vue Hotspot 2',
              x: 73.3973,
              y: 38.3333
            }
          ]
        },
        {
          image: 'https://www.tripsavvy.com/thmb/6oWvLMhqeWAq6YKDREH6S7LMLcE=/950x0/filters:no_upscale():max_bytes(150000):strip_icc():format(webp)/cityscape-of-melbourne-city-of-australia-during-the-sunset--873409300-8db98cef20b44200abfb339188d801f7.jpg',
          editable: true,
          overlayText: '🚀 Customize your own overlay text! 😄',
          hotspotCurves: false
        },
        {
          image: 'https://bluevinta.web24.info.pl/build/assets/map-99cd365e.svg',
          editable: false,
          interactivity: 'hover',
          hotspotCurves: true,
          data: [
            {
              'id': 1,
              'Title': 'Ameryka P\u00f3\u0142nocna',
              'Message': null,
              'x': 10.493441599001,
              'y': 24.211711711712,
              'isMain': 0
            }, {
              'id': 2,
              'Title': 'USA',
              'Message': null,
              'x': 17.801374141162,
              'y': 39.189189189189,
              'isMain': 0
            }, {
              'id': 3,
              'Title': 'Ameryka Po\u0142udniowa',
              'Message': null,
              'x': 28.669581511555,
              'y': 65.765765765766,
              'isMain': 0
            }, {
              'id': 4,
              'Title': 'Afryka',
              'Message': null,
              'x': 51.655215490319,
              'y': 55.18018018018,
              'isMain': 0
            }, {
              'id': 5,
              'Title': 'Australia',
              'Message': null,
              'x': 84.1973766396,
              'y': 78.040540540541,
              'isMain': 0
            }, {
              'id': 6,
              'Title': 'Nowa Zelandia',
              'Message': null,
              'x': 94.628357276702,
              'y': 90.427927927928,
              'isMain': 0
            }, {
              'id': 7,
              'Title': 'Filipiny',
              'Message': null,
              'x': 80.886945658963,
              'y': 56.869369369369,
              'isMain': 0
            }, {
              'id': 8,
              'Title': 'Europa',
              'Message': null,
              'x': 50.156152404747,
              'y': 32.995495495495,
              'isMain': 1
            }, {
              'id': 9,
              'Title': 'Ukraina',
              'Message': null,
              'x': 56.33978763273,
              'y': 33.558558558559,
              'isMain': 0
            }, { 'id': 10, 'Title': 'Azja', 'Message': null, 'x': 77.638975640225, 'y': 37.162162162162, 'isMain': 0 }
          ],
          hotspotColor: '#85ce61',
          messageBoxColor: '#409eff',
          textColor: '#333'
        }
      ]
    }
  },
  methods: {
    changeEditable (conf) {
      if (!conf) return
      conf.editable = !conf.editable
    },
    saveData (data) {
      // A list of hotspots
      console.log(data)
    },
    afterDelete () {
      // Do something after delete
      console.log('Do something after delete ...')
    }
  }
}
</script>

<style lang="less">
@small: 1em;
@medium: 2em;
@gray: #666666;

.no-margin {
  margin: 0
}

.mt-sm {
  margin-top: @small
}

.mb-sm {
  margin-bottom: @small
}

.ml-sm {
  margin-left: @small
}

.mr-sm {
  margin-right: @small
}

.mt-m {
  margin-top: @medium
}

.mb-m {
  margin-bottom: @medium
}

.ml-m {
  margin-left: @medium
}

.mr-m {
  margin-right: @medium
}

.no-padding {
  padding: 0
}

.pt-sm {
  padding-top: @small
}

.pb-sm {
  padding-bottom: @small
}

.pl-sm {
  padding-left: @small
}

.pr-sm {
  padding-right: @small
}

.pt-m {
  padding-top: @medium
}

.pb-m {
  padding-bottom: @medium
}

.pl-m {
  padding-left: @medium
}

.pr-m {
  padding-right: @medium
}

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  padding: 3em 0 0;
  font-family: "Source Sans Pro", "Helvetica Neue", Arial, sans-serif;
  color: @gray;
  text-align: center;
}

a {
  color: inherit;
  text-decoration: none;
}

h1 {
  margin-bottom: 1em;
  font-family: Dosis, "Source Sans Pro", "Helvetica Neue", Arial, sans-serif;
}

h1,
h2 {
  color: #2c3e50;
  font-weight: 300;
}

h2 {
  margin-top: 2em;
  padding-top: 1em;
  font-size: 1.2em;
}

button {
  margin-left: 1em;
  vertical-align: middle;
}

.desc {
  margin-bottom: 3em;
  color: #7f8c8d;
}

.container {
  display: inline-block;
  position: relative;
  margin: 2em auto;
  border: 1px solid rgba(0, 0, 0, .1);
  border-radius: 8px;
  box-shadow: 0 0 45px rgba(0, 0, 0, .2);
  padding: 1.5em 2em;
  // min-width: calc(40vw + 4em);
  width: 50vw;

  .text {
    &.mb-sm {
      margin-bottom: 1em;
    }

    font-size: 1.2em;

    .bold {
      font-weight: bold;
    }

    .left {
      float: left;
    }
  }
}

footer {
  margin: 5em 0 3em;
  font-size: 0.5em;
  vertical-align: middle;

  a {
    display: inline-block;
    margin: 0 5px;
    padding: 3px 0 6px;
    color: #7f8c8d;
    font-size: 2em;
    text-decoration: none;
  }

  a:hover {
    padding-bottom: 3px;
    border-bottom: 3px solid #42b983;
  }
}

@media screen {
  @media (max-width: 980px) {
    section {
      border-top: 1px solid @gray;

      .container {
        width: 100vw;
        margin: @small auto;
        padding: 0;
        border: none;
        border-radius: 0;
        box-shadow: none;
      }
    }
  }
}
</style>

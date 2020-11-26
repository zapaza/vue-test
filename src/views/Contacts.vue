<template>
  <main class="contacts" id="app">
    <div class="wrapper">
      <h1>Мое место обитания</h1>

      <yandex-map
      zoom="16"
      style="width: 100%; max-width: 100%; height: 400px"
      :coords="coords"
    >
      <ymap-marker
        v-for="(billboard, index) in surfaces"
        marker-type="placemark"
        :balloon-template="mapBalloon(billboard, index)"
        :coords="billboard.coords.split(',')"
        :marker-id="index"
        :icon="{ content: billboard.id }"
        :key="index"
      ></ymap-marker>
    </yandex-map>

    </div>
  </main>
</template>
<style lang="scss">

.contacts {
  background-color: $black;
  padding: 64px 0;
  flex: 1 1 auto;
}



.skils {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;

  li {
    padding: 24px;
    font-size: 24px;
    line-height: 32px;
  }
}
</style>
<script>
import { yandexMap, ymapMarker } from 'vue-yandex-maps'



export default {

  name: 'Contacts',
  components: {
  yandexMap, ymapMarker
  },
  data() {
    return {
      coords: [57.82043725132573, 28.274578277441115],
      options: {
        layout: "default#image",
        imageSize: [30, 40],
        contentOffset: [0, 0]
      },
      selectedSurfaces: this.$selectedSurfaces,
      layout:
        "<div>{{ properties.balloonContentHeader }}</div><div>{{ properties.balloonContentBody }}</div><div>{{ properties.balloonContentFooter }}</div>",
      surfaces: [
        {
          id: "М",
          city: "Псков",
          address: 'ул. Михайловская д. 1',
          coords: "57.82043725132573, 28.274578277441115"
        },
      ]
    };
  },
  methods: {
    makeSurfaceSelected: function(surface_id) {
      this.surfaces.forEach(surface => {
        if (surface.surface_id === surface_id) {
          surface.selected = true;
        }
      });
    },
    mapBalloon: function(billboard) {
      return `
      <p><strong>Город:</strong>: ${billboard.city}</p>
      <p><strong>Адрес:</strong>: ${billboard.address}</p>
      </div>
      `;
    }
  }

}
</script>

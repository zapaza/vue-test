<template>
  <main class="contacts" id="app">
    <div class="wrapper">
      <h1>Мое место обитания</h1>

      <yandex-map
      zoom="4"
      style="width: 100%; max-width: 100%; height: 98vh;"
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

<script>
import { yandexMap, ymapMarker } from 'vue-yandex-maps'



export default {
  
  name: 'Contacts',
  components: {
  yandexMap, ymapMarker
  },
  data() {
    return {
      coords: [55.099943, 50.706567],
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
          id: "1",
          city: "Moscow",
          type: "Mediawall",
          address: 'ТРЦ "Океания", пр. Кутузовский, 57',
          coords: "55.727790, 37.475986"
        },
        {
          id: "2",
          city: "Moscow",
          type: "Mediawall",
          address: 'ТРЦ "Хорошо!", Хорошёвское шоссе, 27',
          coords: "55.777138, 37.523430"
        },
        {
          id: "3",
          city: "Moscow",
          type: "Mediawall",
          address: "Варшавское шоссе, д. 118, корп. 1",
          coords: "55.631768, 37.618022"
        },
        {
          id: "4",
          city: "Moscow",
          type: "Mediawall",
          address: "Ленинский проспект, д. 158 ",
          coords: "55.651186, 37.483095"
        },
        {
          id: "5",
          city: "Moscow",
          type: "Mediawall",
          address: 'Волоколамское ш., 3, стр. 1, ТЦ "Карамель"',
          coords: "55.819095, 37.338341"
        },
        {
          id: "6",
          city: "Saint Petersburg ",
          type: "Mediawall",
          address: 'пл. Конституции, 3, БЦ "Leader Tower"',
          coords: "59.850483, 30.305507"
        },
      ]
    };
  },
  mounted() {
    console.log(this.$selectedSurfaces);
  },
  watch: {
    selectedSurfaces() {
      this.makeSurfaceSelected(
        this.selectedSurfaces[this.selectedSurfaces.length - 1].SURFACEID
      );
    }
  },
  methods: {
    selectedBillboard(billboard) {
      let data = {
        SURFACEID: billboard.surface_id,
        NETWORKID: billboard.networkid
      };
      return data;
    },
    makeSurfaceSelected: function(surface_id) {
      this.surfaces.forEach(surface => {
        if (surface.surface_id === surface_id) {
          surface.selected = true;
        }
      });
    },
    mapBalloon: function(billboard) {
      return `
      <div><h1>${billboard.id}</h1>
      <p><strong>City</strong>: ${billboard.city}</p>
      <p><strong>Type</strong>: ${billboard.type}</p>
      <p><strong>Side</strong>: ${billboard.side}</p>
      <p><strong>Address</strong>: ${billboard.address}</p>
      </div>
      `;
    }
  }
  
}
</script>
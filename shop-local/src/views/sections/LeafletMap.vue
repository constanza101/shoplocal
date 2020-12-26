<template>
  <base-section class="py-6" id="leaflet-map" style="max-height: calc(100vh - 150px); overflow: auto">
  <v-row class="px-8">
    <v-col cols="12" md="6" lg="8">
          <!-- <div>
        <span v-if="loading">Loading...</span>
        <label for="checkbox">GeoJSON Visibility</label>
        <input id="checkbox" v-model="show" type="checkbox" />
        <label for="checkboxTooltip">Enable tooltip</label>
        <input id="checkboxTooltip" v-model="enableTooltip" type="checkbox" />
        <input v-model="fillColor" type="color" /> {{ marker }} {{center}}
        <br />
      </div> -->
      <l-map  :zoom="zoom" :center="center" style="height: calc( 100vh - 220px); width: 100%; z-index">
        <l-tile-layer :url="url" :attribution="attribution" />
        <l-geo-json
          v-if="show"
          :geojson="geojson"
          :options="options"
          :options-style="styleFunction"
        />

        
        <l-marker
        v-if="creatingNewshop"
          :draggable="true"
          :lat-lng="marker"
          @update:lat-lng="updatePosition"
        />

      <div v-if="shops.length > 0 ">
          <l-marker
            v-for="(shop, index) in filteredShops"
            :lat-lng="shop.position"
            :key="index"
            :draggable="true"
            :title="shop.name"
            @click="editMarker(shop)"
            :search="search"
          >
            <l-icon>
              <div class="background-icon">
                <v-icon>{{shop.icon}}</v-icon>
                
              </div>
            </l-icon>
            <l-popup >
              <v-row>
              <v-col class=" d-flex justify-center pt-1"  cols="12" style="font-size:18px;"> <b>{{shop.name}}</b> </v-col>
              </v-row>
              <p v-if="shop.address">{{shop.address}}</p>
              <v-col class="pa-0 d-flex justify-center">
                <v-btn @click="openLink(shop.website)" icon v-if="shop.website"> <v-icon small>mdi-web</v-icon> </v-btn>
                <v-btn @click="openLink(shop.instagram)" icon v-if="shop.instagram"> <v-icon small>mdi-instagram</v-icon> </v-btn>
                <v-btn @click="openLink(shop.facebook)" icon v-if="shop.facebook"> <v-icon small>mdi-facebook</v-icon> </v-btn>
              </v-col>
            
            </l-popup>
          </l-marker>
        </div>

      </l-map>

    </v-col>
    <v-col cols="12" md="6" lg="4" >
      <b>Filtro</b>

    <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Busca un rubro o nombre de tienda"
        hide-details
        outlined
        
      ></v-text-field>

      <v-data-table
        class="pt-3"
        height="calc(100vh - 350px)"
        :headers="headers"
        :items="shops"
        :search="search"
      ></v-data-table>
    </v-col>
  </v-row>
  <v-row class="px-12">
    <v-col class="px-12">

    </v-col>
  </v-row>




    
  </base-section>
</template>

<script>
import { latLng } from "leaflet";
import {
  LMap,
  LTileLayer,
  // LImageOverlay,
  LMarker,
  LPopup,
  LIcon,
  // LTooltip,
  // LControl,
  LGeoJson
} from "vue2-leaflet";


export default {
  name: "LeafletMap",
  components: {
    LMap,
    LTileLayer,
    LGeoJson,
    LMarker,
    // LImageOverlay,
    LPopup,
    LIcon,
    // LTooltip,
    // LControl,
  },
  data() {
    return {
      search:"",
      value:null,
      filterTags: [],
      creatingNewshop: false,
      loading: false,
      show: true,
      enableTooltip: true,
      zoom: 14,
      center: [41.279313, 1.974593],
      geojson: null,
      fillColor: "#e4ce7f",
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      marker: latLng(41.279313, 1.974593),
    };
  },
  computed: {


    headers(){
      let headers = [
        {
            text: 'nombre',
            align: 'start',
            filterable: true,
            value: 'name',
            width: 200 
        },
        {
            text: 'tags',
            align: 'start',
            filterable: true,
            value: 'tags',
            width: 20 
        },
      ]
      return headers

    },
    shops(){
      let shops =  [
        {id: 1, name: "Mercería B.E.A", icon: "mdi-shoe-heel", position: latLng(41.2788893,1.9764628,21), instagram: "https://www.instagram.com/merceriabea/", website:"https://www.merceriabea.com/", tags: ["mercería", "costurera", "compostura", "lana", "mascarillas", "arreglos"]},
        {id: 2, name: "Intez Inmuebles", instagram: "https://www.instagram.com/intezinmuebles/",  icon:"mdi-office-building", website:"https://www.intez.es/", facebook:"https://www.facebook.com/intezinmuebles", position: latLng(41.2687707,1.9885141,21), tags: [" inmuebles", " compra", " venta", " inmobiliaria", " apartamentos", " alquiler"]},
        {id: 3, name: "Gominoles", icon: "mdi-muffin", instagram:"https://www.instagram.com/gominoles.castelldefels/", facebook:"https://www.facebook.com/gominoles.castelldefels/", position: latLng(41.2826808,1.9797894,21),  tags: [" gominoles", " dulces", " golosinas", " cumpleaños", " niños"]},
        {id: 4, name: "La casa de la iaia", icon: "mdi-baby-face-outline", instagram:"https://www.instagram.com/lacasadelaiaiacastelldefels/", facebook:"https://www.facebook.com/ludotecacastelldefels/", position: latLng(41.2836123,1.9811225,21),  tags: [" ludoteca", " guardería", " fiestas infantiles", " cumpleaños", " niños"]},
        {id: 5, name: "Naturbella", icon: "mdi-face-woman-outline", instagram:"https://www.instagram.com/naturbellacastelldefels/", facebook:"https://www.facebook.com/naturbellacastelldefels/", position: latLng(41.2831536,1.9809661,21), website:"https://centre-estetica-naturbella-castelldefels.negocio.site/", tags: [" estética", " centro de estética", " peluquería", " manicura", " esmalte", " semipermanente"]},
        {id: 6, name: "Delma Nails", icon: "mdi-face-woman-outline", instagram:"https://www.instagram.com/delmaelisa_nails/",  position: latLng(41.266846,1.981148,21), website:"https://delma-nails.negocio.site/", tags: [" estética", " centro de estética", " manicura", " esmalte", " semipermanente"]},
        ]
      return shops
    },
    filteredShops() {
           return this.shops.filter(item => {
                return item.name.toLowerCase().includes(this.search.toLowerCase()) 
                || item.tags.join('').toLowerCase().includes(this.search.toLowerCase()) 
            });
        },
    tags(){
      let foundTags = []
      this.shops.map(shop => { foundTags = [...new Set([...foundTags,...shop.tags])] })
      return foundTags
    },
    options() {
      return {
        onEachFeature: this.onEachFeatureFunction,
      };
    },
    styleFunction() {
      const fillColor = this.fillColor; // important! need touch fillColor in computed for re-calculate when change fillColor
      return () => {
        return {
          weight: 2,
          color: "#ECEFF1",
          opacity: 1,
          fillColor: fillColor,
          fillOpacity: 1,
        };
      };
    },
    onEachFeatureFunction() {
      if (!this.enableTooltip) {
        return () => {};
      }
      return (feature, layer) => {
        layer.bindTooltip(
          "<div>code:" +
            feature.properties.code +
            "</div><div>nom: " +
            feature.properties.nom +
            "</div>",
          { permanent: false, sticky: true }
        );
      };
    },
  },
  methods: {
    clearfilterTags(){
      this.filterTags = []
    },
    openLink(item){
        window.open(item, '_blank');
    },
    updatePosition(position) {
      this.marker = position;
    },
    editMarker(shop){
      console.log(shop)
    }
  },
  async created() {
    this.loading = true;
    const response = await fetch(
      "https://rawgit.com/gregoiredavid/france-geojson/master/regions/pays-de-la-loire/communes-pays-de-la-loire.geojson"
    );
    const data = await response.json();
    this.geojson = data;
    this.loading = false;
  },
};
</script>
<style scoped lang="css">
  .background-icon {
  margin-top: -27px;
  margin-left: -10px;
  width: 35px;
  height: 35px;
  background-color: white;
  border-radius: 50%;
  padding: 5px;
  box-shadow: 1px 1px 5px grey;
}
a {
  color: black 
}
>>> .leaflet-popup{
  margin-bottom: 40px;
}
>>> .leaflet-top {
    z-index: 400;
}
>>> .leaflet-bottom{
    z-index: 400;

}
</style>

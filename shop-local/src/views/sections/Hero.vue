<template>
  <section id="hero" style="max-height: calc(100vh - 150px); overflow: hidden">
    <v-img
      :min-height="minHeight"
      src="https://upload.wikimedia.org/wikipedia/commons/5/5e/Castell_de_Fels%2C_Esgl%C3%A9sia_de_Santa_Maria_i_Torre_de_guaita_%28Castelldefels%29_-_1.jpg"
      class="white--text"
      gradient="to right, rgba(5, 11, 31, .8), rgba(5, 11, 31, .8)"
    >
      <v-container class="fill-height px-4 py-12 " >
        <v-responsive
          class="d-flex align-start"
          height="100%"
          max-width="700"
          width="100%"
        >
        <v-col style="background-color: primary; width: 240px;  border-radius:150px; margin-left:80px; margin-bottom:50px" class="py-10 px-9">
          <base-img
            style="margin-left: -170px"
            :src="require('@/assets/castelldefels.png')"
            contain
            max-width="500"
            min-height="78"
            width="500"
          />
        </v-col>

          <base-heading  title="TIENDAS DE BARRIO" />

          <base-body>
            Encuentra lo que necesitas en tu barrio y apoya el comercio local.
            <br />
            Visita los perfiles de las tiendas de barrio para conocerlos mejor.
            <br />
            Compra e-cards para regalar y canjéalas en la tienda que más te
            guste.
          </base-body>

          <div
            :class="
              $vuetify.breakpoint.smAndDown
                ? 'flex-column align-start'
                : 'align-center'
            "
            class="d-flex flex-wrap"
          >
            <v-btn width="200px" light color="primary" class="mr-8 my-3" > Buscar tienda </v-btn>
            <v-btn  width="200px" text color="primary" :ripple="false" > tengo una tienda </v-btn>

          </div>
        </v-responsive>
      </v-container>
    </v-img>
  </section>
</template>

<script>
export default {
  name: "SectionHero",

  provide: {
    theme: { isDark: true },
  },

  computed: {
    minHeight() {
      const height = this.$vuetify.breakpoint.mdAndUp ? "100vh" : "50vh";
      return `calc(${height} - ${this.$vuetify.application.top}px)`;
    },
  },
};
</script>

<template>
  <base-section id="about-our-product">
    <base-section-heading
      color="grey lighten-2"
      icon="mdi-storefront-outline"
      title="Apoyamos el Comercio Local"
    />

    <v-container>
      <v-row>
        <v-col
          v-for="card in cards"
          :key="card.title"
          cols="12"
          md="4"
        >
          <base-info-card v-bind="card" />
        </v-col>
      </v-row>
    </v-container>
  </base-section>
</template>

<script>
  export default {
    name: 'SectionAboutOurProduct',

    data: () => ({
      cards: [
        {
          title: '¿Quiénes somos?',
          subtitle: '¿Por qué?',
          text: '... mejor dicho "¿quién soy?,  ya que soy una sola persona, mi nombre es Constanza y siendo hija de comerciantes, aunque en este momento no me dedico a eso, conozco en persona el trabajo y las dificultades que atraviesan los comerciantes normalmente y en sespecial en esta época tan dificl! También conozco que para los comercios tradicionales es dificil la transición a lo digital, pero que es una necesidad vital para las tiendas al día de hoy.',
          callout: '01',
        },
        {
          title: 'Cómo surgió',
          subtitle: 'Castelldefels Tiendas de Barrio',
          text: 'Con el confinamiento de la pandemia me vi oblgada a trabajar desde casa, lo que me llevó a darme cuenta de que al ir todos los días a Barcelona, hacía todas mis compras allí y no conocía las tiendas de mi ciudad Castelldefels. El día 1 de mayo de 2020, casualmente el día del trabajador, se me ocurrió abrir una cuenta de Instagram para agrupar y dar a conocer las tiendas de Castelldefels, lo cual tuvo mucha acogida, especialmente por parte de los comerciantes que  han sido los más golpeados por esta crisis.',
          callout: '02',
        },
        {
          title: 'Cómo publicar?',
          subtitle: 'Mi proyecto',
          text: 'El principal canal es Instagram, donde publicamos gratuitamente un post en el feed con la presentación y las imágenes que nos envíes. El único requisito es que estés en Castelldefels y tengas una tienda, emprendimiento o servicio. Para aparecer en nuestras historias sólo tienes que etiquetarnos y así podremos compartirlas. Búscanos como @castelldefelstiendasdebarrio en Instagram.',
          callout: '03',
        },
      ],
    }),
  }
</script>

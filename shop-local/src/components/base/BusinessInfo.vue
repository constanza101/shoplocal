<template>
  <v-theme-provider :dark="dark">
    <div>
      <base-info-card
        title="contáctanos"
        pace="6"
      >
      Si quieres ser parte de esta comunidad envía tus datos y los de tu tienda a nuestro  e-mail.
      </base-info-card>

      <base-business-contact dense />
    </div>
  </v-theme-provider>
</template>

<script>
  export default {
    name: 'BaseBusinessInfo',

    props: { dark: Boolean },

    data: () => ({
      business: [
        {
          icon: 'mdi-map-marker-outline',
          title: 'Ubicación',
          text: 'Castelldefels (08860)',
        },
        {
          icon: 'mdi-cellphone',
          title: 'Teléfono',
          text: '+34 640286830',
        },
        {
          icon: 'mdi-email',
          title: 'Email',
          text: 'constanza.diaz@gmail.com',
        },
      ],
    }),
  }
</script>

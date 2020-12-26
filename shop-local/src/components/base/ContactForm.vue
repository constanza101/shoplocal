<template>
  <div>
    <base-info-card
      :title="title"
      :subtitle="subtitle"
      space="4"
      color="primary"
    />

    <base-text-field label="Nombre o tienda" />

    <base-text-field label="Email" />

    <base-text-field label="Asunto" />

    <base-textarea
      class="mb-6"
      label="Mensaje"
    />

    <base-btn
      :color="!theme.isDark ? 'accent' : 'white'"
      href="mailto:constanza.diaz@gmail.com?subject=Castelldefels%20Tiendas%20de%20Barrio"
      outlined
      target="_blank"
    >
      Enviar
    </base-btn>
  </div>
</template>

<script>
  export default {
    name: 'BaseContactForm',

    // Injected from the Vuetify Themeable mixin
    inject: ['theme'],

    props: {
      subtitle: String,
      title: {
        type: String,
        default: 'MAIL US YOUR MESSAGE',
      },
    },
  }
</script>

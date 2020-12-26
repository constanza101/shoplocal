<template>
  <v-theme-provider :dark="dark">
    <div>
      <base-info-card
        :title="title"
        color="primary"
      >
        <slot />
      </base-info-card>

      <template style="height: 500px" v-for="({ icon, text, title: t }, i) in business">
        <base-avatar-card
          :key="i"
          :icon="icon"
          :outlined="false"
          :title="!dense ? t : undefined"
          color="transparent"
          horizontal
          space="0"
        >
          <!-- Do not use v-html for user -->
          <!-- provided values -->
          <div class="pt-3" v-html="text" />
        </base-avatar-card>

        <v-divider
          v-if="i + 1 !== business.length"
          :key="`divider-${i}`"
          class="my-0"
        />
      </template>
    </div>
  </v-theme-provider>
</template>

<script>
  export default {
    name: 'BaseBusinessContact',

    props: {
      dark: Boolean,
      dense: Boolean,
      title: String,
    },

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

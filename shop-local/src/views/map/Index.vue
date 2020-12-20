<script>
  // Extensions
  import View from '@/views/View'

  // Mixins
  import LoadSections from '@/mixins/load-sections'

  export default {
    name: 'Map',

    metaInfo: { title: 'About Us' },

    extends: View,

    mixins: [
      LoadSections([
        'leaflet-map',
        // 'hero-alt',
        // 'about-our-product',
        // 'theme-features',
        // 'affiliates',
        // 'newsletter',
        // 'pro-features',
        // 'info',
      ]),
    ],

    props: {
      id: {
        type: String,
        default: 'about',
      },
    },
  }
</script>

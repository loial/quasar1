<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          Catalog Scanner
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>

        <InternalLink
          v-for="link in internalLinks"
          :key="link.title"
          v-bind="link"
        />
        <q-item-label
          header
          v-if="essentialLinks.count"
        >
          Essential Links
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
import InternalLink from 'components/InternalLink.vue'


const pageList = [
  {
    title: 'Main',
    caption: '',
    icon: 'home',
    link: '/'
  },
  {
    title: 'Scan',
    caption: 'Scan barcodes',
    icon: 'barcode_reader',
    link: 'scan'
  }
]

const linksList = [
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink,
    InternalLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      internalLinks: pageList,
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>

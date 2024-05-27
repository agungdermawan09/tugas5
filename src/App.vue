<template>
  <q-layout view="lHh Lpr fff" class="bg-dark">
    <!-- Navbar -->
    <q-header elevated class="bg-dark text-white" height-hint="64">
      <q-toolbar class="q-px-md" style="height: 64px">
        <q-btn
          flat
          dense
          round
          @click="toggleLeftDrawer"
          aria-label="Menu"
          icon="menu"
          class="text-white"
        />
        <q-toolbar-title class="row items-center no-wrap">
          <span class="q-ml-sm">Jual Beli</span>
        </q-toolbar-title>

        <q-space />

        <q-input class="q-mr-md" dense standout="bg-grey-7" v-model="search" placeholder="Search">
          <template v-slot:prepend>
          </template>
        </q-input>

        <q-btn  @click="menu = !menu" ref="menuBtn" class="text-white">
          <q-menu v-model="menu" anchor="top right" self="top right">
            <q-list class="text-white" style="min-width: 100px">
              <q-item aria-hidden="true">
                <q-item-section class="text-uppercase text-grey-7" style="font-size: 0.7rem">Menu</q-item-section>
              </q-item>
              <q-item v-for="item in menuItems" :key="item.label" clickable v-close-popup aria-hidden="true" @click="handleMenuItemClick(item.action)">
                <q-item-section avatar>
                  <q-icon :name="item.icon" />
                </q-item-section>
                <q-item-section>{{ item.label }}</q-item-section>
              </q-item>
            </q-list>
          </q-menu>
        </q-btn>
      </q-toolbar>
    </q-header>

    <!-- Sidebar -->
    <q-drawer v-model="leftDrawerOpen" bordered class="bg-dark text-white">
      <q-scroll-area class="fit">
        <q-list padding>
          <q-item v-for="link in links1" :key="link.text" clickable class="text-white">
            <q-item-section avatar>
              <q-icon :name="link.icon" class="text-white" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ link.text }}</q-item-label>
            </q-item-section>
          </q-item>

          <q-separator class="q-my-md" />

          <q-item v-for="link in links2" :key="link.text" clickable class="text-white">
            <q-item-section avatar>
              <q-icon :name="link.icon" class="text-white" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ link.text }}</q-item-label>
            </q-item-section>
          </q-item>

          <q-separator class="q-my-md" />

          <q-item v-for="link in links3" :key="link.text" clickable class="text-white">
            <q-item-section avatar>
              <q-icon :name="link.icon" class="text-white" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ link.text }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <!-- Page Container -->
    <q-page-container class="q-pa-md">
      <!-- Carousel -->
      <q-carousel animated autoplay infinite transition-prev="fade" transition-next="fade" arrows navigation>
        <q-carousel-slide v-for="(image, index) in carouselImages" :key="index" :img-src="image">
          <div class="absolute-bottom text-white text-center bg-black bg-opacity-50 q-pa-sm">{{ imageText }}</div>
        </q-carousel-slide>
      </q-carousel>

      <!-- Product Cards -->
      <q-page class="q-pa-md">
        <q-card v-for="product in products" :key="product.name" class="q-mb-md bg-grey-10 text-white shadow-2">
          <q-img :src="product.image" ratio="4/3">
            <q-banner dense class="absolute-bottom text-white bg-primary">
              <div>{{ product.name }}</div>
              <div>{{ product.price }}</div>
            </q-banner>
          </q-img>
          <q-card-section>
            <div class="text-h6">{{ product.name }}</div>
            <div class="text-subtitle1">{{ product.price }}</div>
          </q-card-section>
          <q-card-actions align="right">
            <q-btn flat color="primary" @click="addToCart(product)">Add to Cart</q-btn>
          </q-card-actions>
        </q-card>
      </q-page>
    </q-page-container>

    <!-- Footer -->
    <q-footer class="bg-grey-9 text-white q-px-md q-pt-md q-pb-sm">
      <q-toolbar>
        <q-toolbar-title class="text-h6">Jual Beli</q-toolbar-title>
        <q-space />
        <div>© 2024 Jual Beli</div>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'JualBeliLayout',

  setup () {
    const leftDrawerOpen = ref(false)
    const search = ref('')
    const menu = ref(false)

    const products = ref([
      { name: 'Product 1', price: 'Rp 100.000', image: 'https://via.placeholder.com/150' },
      { name: 'Product 2', price: 'Rp 200.000', image: 'https://via.placeholder.com/150' },
      { name: 'Product 3', price: 'Rp 300.000', image: 'https://via.placeholder.com/150' }
    ])
    const carouselImages = ref([
      'https://via.placeholder.com/800x400',
      'https://via.placeholder.com/800x400',
      'https://via.placeholder.com/800x400'
    ])
    const imageText = 'Welcome to Jual Beli'

    const menuItems = ref([
      { label: 'Home', icon: 'home', action: 'home' },
      { label: 'Profile', icon: 'person', action: 'profile' },
      { label: 'Settings', icon: 'settings', action: 'settings' },
      { label: 'Logout', icon: 'exit_to_app', action: 'logout' }
    ])


    function toggleLeftDrawer () {
      leftDrawerOpen.value = !leftDrawerOpen.value
    }

    function addToCart (product) {
      console.log('Adding to cart:', product)
    }

    function handleMenuItemClick (action) {
      console.log(`Menu item ${action} clicked`)
      menu.value = false
      // Add your navigation logic here
    }

    return {
      leftDrawerOpen,
      search,
      products,
      carouselImages,
      imageText,
      menu,
      menuItems,
      toggleLeftDrawer,
      addToCart,
      handleMenuItemClick,
      links1: [
        {  text: 'Home' },
        {  text: 'About' },
        {  text: 'Contact' }
      ],
    }
  }
}
</script>

<style scoped>
.q-layout__section--scroll {
  background-color: #121212;
}

.q-header {
  background-color: #1e1e1e;
  color: #fff;
}

.q-drawer {
  
  background-color: #1e1e1e;
}

.q-page {
  background-color: #aaa6a6;
}

.q-footer {
  background-color: #3f3c3c;
  color: #fff;
}

.q-input {
  color: #fff;
}

.q-banner {
  background-color: rgba(93, 88, 88, 0.7);
}

.q-card {
  background-color: #2c2c2c;
}

.text-white {
  color: #fff;
}
</style>

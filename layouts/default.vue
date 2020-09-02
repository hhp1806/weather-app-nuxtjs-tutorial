<template>
  <v-app>
    <v-main>
      <v-toolbar color="indigo">
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
        <v-toolbar-title>
          <n-link to="/"> Weather App </n-link>
        </v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items class="hidden-sm-and-down">
          <v-btn text>
            <n-link to="/weather-app"> Home </n-link>
          </v-btn>
        </v-toolbar-items>
      </v-toolbar>
      <transition>
        <v-main>
          <nuxt />
        </v-main>
      </transition>
    </v-main>
  </v-app>
</template>

<script>
export default {}
</script>

<style scoped>
a {
  text-decoration: none;
  color: white;
}
</style>

<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" color="#4caf50" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn
        v-if="isLogined === false"
        color="#087f23 "
        href="https://spotinowserver.shiguma.net/login"
        >Login</v-btn
      >
      <v-btn icon>
        <v-icon @click="componentKey += 1">mdi-reload</v-icon>
      </v-btn>
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt :key="componentKey" />
      </v-container>
    </v-content>
    <v-footer :fixed="fixed" app>
      <span>&copy; {{ new Date().getFullYear() + ' shiguma127' }}</span>
      <v-spacer />
      <span>
        <div>
          <a
            href="https://twitter.com/share?ref_src=twsrc%5Etfw"
            class="twitter-share-button"
            data-text="Spotinowで再生中の音楽をシェアしよう♪"
            data-url="spotinow.shiguma.net"
            data-hashtags="Spotinow"
            data-show-count="false"
            >Tweet</a
          >
          <script
            async
            src="https://platform.twitter.com/widgets.js"
            charset="utf-8"
          ></script>
        </div>
      </span>
    </v-footer>
  </v-app>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      componentKey: 0,
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'HOME',
          to: '/'
        },
        {
          icon: 'mdi-cog-outline',
          title: 'Settings',
          to: '/settings'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'SpotiNow',
      isLogined: false
    }
  },
  created() {
    axios
      .get('https://spotinowserver.shiguma.net/api/islogined', {
        withCredentials: true
      })
      .then((response) => (this.isLogined = response.data.islogined))
  }
}
</script>

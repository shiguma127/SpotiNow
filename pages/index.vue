<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <v-container>
        <v-row dense>
          <v-col v-for="(item, i) in items" :key="i" cols="12">
            <v-card :color="item.color" dark>
              <div class="d-flex flex-no-wrap justify-space-between">
                <v-avatar class="ma-3" size="125">
                  <v-img :src="item.icon"></v-img>
                </v-avatar>
                <div>
                  <v-card-text
                    class="headline"
                    v-text="item.title"
                  ></v-card-text>
                  <v-card-subtitle v-text="item.song"></v-card-subtitle>
                  <v-card-text v-text="item.artist"></v-card-text>
                </div>
                <v-avatar class="ma-3" size="125" tile>
                  <v-img :src="item.albumArt"></v-img>
                </v-avatar>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data: () => ({
    items: [
      {
        color: '#1F7087',
        icon:
          'https://pbs.twimg.com/profile_images/1161252458871644161/ckBHovuv_400x400.jpg',
        albumArt: 'https://cdn.vuetifyjs.com/images/cards/foster.jpg',
        title: '@shiguma127 is Playing',
        artist: 'Foster the People',
        song: 'hahahahaSong'
      },
      {
        color: '#952175',
        icon:
          'https://pbs.twimg.com/profile_images/1161252458871644161/ckBHovuv_400x400.jpg',
        albumArt: 'https://cdn.vuetifyjs.com/images/cards/halcyon.png',
        title: '@shiguma128 is Playing',
        artist: 'Ellie Goulding',
        song: 'lalalaSong'
      }
    ]
  })
}
</script>

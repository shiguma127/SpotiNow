<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <v-container>
        <v-row dense>
          <v-col v-for="(item, i) in items" :key="i" cols="12">
            <v-card :color="item.color" dark>
              <div class="d-flex flex-no-wrap justify-space-between">
                <v-row class="">
                  <v-col>
                    <v-layout justify-center>
                      <v-avatar class="ma-3" size="125">
                        <v-img :src="item.icon"></v-img>
                      </v-avatar>
                    </v-layout>
                    <v-layout justify-center>
                      <p v-text="item.user"></p>
                    </v-layout>
                  </v-col>
                  <v-col>
                    <v-row>
                      <v-col>
                        <v-spacer />
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-col>
                        <v-card-title
                          class="headline"
                          v-text="item.song"
                        ></v-card-title>
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-col>
                        <v-layout justify-end align-center>
                          <v-card-text v-text="item.artist"></v-card-text>
                        </v-layout>
                      </v-col>
                    </v-row>
                  </v-col>
                  <v-col>
                    <v-row>
                      <v-spacer />
                    </v-row>
                    <v-row>
                      <v-col>
                        <v-layout justify-center>
                          <v-avatar class="ma-3" size="125" tile>
                            <v-img :src="item.albumArt"></v-img>
                          </v-avatar>
                        </v-layout>
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-layout justify-center>
                        <v-btn color="#4caf50">Listen together</v-btn>
                      </v-layout>
                    </v-row>
                  </v-col>
                </v-row>
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
        user: '@shiguma127',
        artist: 'Foster the People',
        song: 'hahahahaSong'
      },
      {
        color: '#952175',
        icon:
          'https://pbs.twimg.com/profile_images/1161252458871644161/ckBHovuv_400x400.jpg',
        albumArt: 'https://cdn.vuetifyjs.com/images/cards/halcyon.png',
        user: '@shiguma128',
        artist: 'Ellie Goulding',
        song: 'lalalaSong'
      }
    ]
  })
}
</script>

<template>
  <v-layout justify-center align-center>
    <v-flex xs12 sm12 md12>
      <v-container>
        <v-layout justify-center>
          <v-progress-circular
            v-show="onLoading"
            indeterminate
            color="#4caf50"
          ></v-progress-circular>
        </v-layout>
        <v-row dense>
          <v-layout justify-end>
            <v-expand-transition>
              <v-alert
                v-if="hasError"
                v-model="hasError"
                type="error"
                dismissible
                transition="scale-transition"
              >
                <div v-text="errorMessages"></div>
              </v-alert>
            </v-expand-transition>
          </v-layout>
          <v-col v-for="(item, i) in items" :key="i" cols="12">
            <v-card :color="item.color" dark>
              <div class="d-flex flex-wrap justify-space-between">
                <v-row class="">
                  <v-col>
                    <v-layout justify-center>
                      <v-avatar class="ma-3" size="125">
                        <v-img :src="item.icon"></v-img>
                      </v-avatar>
                    </v-layout>
                    <v-layout justify-center>
                      <p
                        :class="item.textcolor + '--text'"
                        v-text="item.name"
                      ></p>
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
                          :class="item.textcolor + '--text'"
                          v-text="item.song"
                        ></v-card-title>
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-col>
                        <v-layout justify-end align-center>
                          <v-card-text
                            :class="item.textcolor + '--text'"
                            v-text="item.artist"
                          ></v-card-text>
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
                            <v-img :src="item.albumart"></v-img>
                          </v-avatar>
                        </v-layout>
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-layout justify-center>
                        <v-btn color="#4caf50" @click="sendRequest(item.userid)"
                          >Listen together</v-btn
                        >
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
import axios from 'axios'
export default {
  data: () => ({
    hasError: false,
    items: null,
    errorMessages: 'error',
    onLoading: false
  }),
  created() {
    this.getinfo()
  },
  methods: {
    getinfo() {
      this.onLoading = true
      axios
        .get('https://spotinowserver.shiguma.net/api/getuser', {
          withCredentials: true
        })
        .then((response) => (this.items = response.data.userlist))
        .then((this.onLoading = false))
    },
    sendRequest(id) {
      axios
        .post(
          'https://spotinowserver.shiguma.net/api/listentogether',
          { userid: id },
          { withCredentials: true }
        )
        .then((response) => this.alertErrorMessage(response.data.errorMessages))
    },
    alertErrorMessage(msg) {
      if (msg) {
        this.hasError = true
        this.errorMessages = msg
      }
    },
    test() {
      this.onLoading = !this.onLoading
    }
  }
}
</script>

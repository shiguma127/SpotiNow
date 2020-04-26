<template>
  <v-layout justify-center align-center>
    <v-flex xs12 sm12 md12>
      <v-container>
        <v-row dense>
          <v-col v-for="(item, i) in items" :key="i" cols="12">
            <v-card :color="'#1F7087'" dark>
              <div class="d-flex flex-no-wrap justify-space-between">
                <v-row class="">
                  <v-col cols="2">
                    <v-layout justify-center>
                      <v-avatar class="ma-3" size="125">
                        <v-img :src="item.icon"></v-img>
                      </v-avatar>
                    </v-layout>
                    <v-layout justify-center>
                      <p v-text="item.name"></p>
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
    items: null
  }),
  created() {
    axios
      .get('http://localhost:8080/api/getuser', { withCredentials: true })
      .then((response) => (this.items = response.data.userlist))
  },
  methods: {
    sendRequest(id) {
      axios.post(
        'http://localhost:8080/api/listentogether',
        { userid: id },
        { withCredentials: true }
      )
    }
  }
}
</script>

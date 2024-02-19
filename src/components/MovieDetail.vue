<template>
  <div>
    <v-dialog v-model="dialog" width="auto">
      <v-card>
        <v-card-text>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor incididunt ut labore et dolore magna aliqua.
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" block @click="closeDetail">Fermer</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
const config = require("../config.json");
import axios from "axios";

export default {
  name: "MovieDetail",
  props: {
    movieId: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      movie: {},
      photo_path: config.url.photo_path,
      dialog: true,
    };
  },
  mounted() {
    axios
      .get(`${config.url.movie_detail}${this.movieId}`, {
        headers: {
          Authorization: `bearer ${config.api_key}`,
        },
      })
      .then((response) => {
        this.movie = response.data;
        console.log(response.data);
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
    closeDetail() {
      this.$emit("close");
    },
  },
};
</script>



<!-- template qui fonctionne o k ou
    <template>
    <div>
      <v-dialog v-model="dialog" width="auto">
        <v-card>
          <v-card-text>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
            eiusmod tempor incididunt ut labore et dolore magna aliqua.
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" block @click="closeDetail">Fermer</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
  </template> -->
<template>
  <div>
    <v-dialog v-model="dialog" width="auto">
      <v-card theme="dark">
        <v-container>
          <v-row>
            <v-col>
              <div class="text-center">
                <v-card-title class="text-h2">{{ movie.title }}</v-card-title>
              </div>

              <v-img
                height="300px"
                :src="photo_path + movie.poster_path"
                alt="movie poster"
              ></v-img>

              <v-card-text class="text-h4">Date de sortie :</v-card-text>
              <div class="text-center">
                <v-card-text class="text-h5">
                  {{ movie.release_date }}
                </v-card-text>
              </div>

              <v-card-text class="text-h4">Genres :</v-card-text>
              <c-container>
                <v-row>
                  <v-col class="text-center">
                    <v-chip
                      v-for="genre in movie.genres"
                      :key="genre.id"
                      color="teal-accent-4"
                      class="mx-auto"
                    >
                      {{ genre.name }}
                    </v-chip>
                  </v-col>
                </v-row>
              </c-container>

              <v-card-text class="text-h4"> Note : </v-card-text>
              <div class="text-center">
                <v-rating
                  v-model="movie.vote_average"
                  color="amber"
                  length="10"
                  dense
                  readonly
                  class="text-center"
                ></v-rating>
              </div>

              <v-card-text class="text-h4">Production :</v-card-text>
              <div class="text-center">
                <v-avatar
                  v-for="company in movie.production_companies"
                  :key="company.id"
                  size="100"
                  class="mx-2"
                  color="teal-accent-4"
                >
                  <v-img
                    :src="photo_path + company.logo_path"
                    alt="company logo"
                    v-if="company.logo_path !== null"
                  ></v-img>
                  <v-text-field
                    v-model="company.name"
                    readonly
                    class="text-center"
                    v-else
                  ></v-text-field>
                </v-avatar>
              </div>

              <v-card-text class="text-h4">Résumé :</v-card-text>
              <v-card-text class="text-subtitle-1">
                {{ movie.overview }}
              </v-card-text>
              <v-card-actions>
                <v-btn color="primary" block @click="closeDetail">Fermer</v-btn>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-container>
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
      .get(`${config.url.movie_detail}${this.movieId}?language=fr-FR`, {
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

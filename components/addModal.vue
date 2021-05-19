<template>
  <section>
    <div class="buttons">
      <b-button
        label="Añadir"
        type="is-success"
        size="is-medium"
        @click="isCardModalActive = true"
      />
    </div>

    <b-modal v-model="isCardModalActive" :width="640" scroll="keep">
      <div class="card">
        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <b-field label="Nombre">
                <b-input v-model="nombre"></b-input>
              </b-field>

              <b-field label="Genero">
                <b-select v-model="genre" placeholder="Elige un Genero">
                  <option>Shounen</option>
                  <option>Seinen</option>
                  <option>Deportes</option>
                  <option>Romance</option>
                  <option>Psicologico</option>
                  <option>Aventura</option>
                  <option>Comedia</option>
                </b-select>
              </b-field>

              <b-field label="Capitulos">
                <b-input
                  v-model="chapter"
                  type="number"
                  min="0"
                  max="1250"
                ></b-input>
              </b-field>
              <b-field label="Nota">
                <b-input
                  v-model="rating"
                  type="number"
                  min="0"
                  max="10"
                ></b-input>
              </b-field>

              <b-button @click="addAnime(id, anime)" type="is-success" >Aceptar</b-button
              >
            </div>
          </div>
        </div>
      </div>
    </b-modal>
  </section>
</template>

<script>
export default {
  props: ["id", "anime"],
  data() {
    return {
      isCardModalActive: false,

      nombre: "",
      genre: "",
      chapter: "",
      rating: "",
    };
  },

  methods: {
    addAnime() {
      const lasto = 5;

      this.anime.push({
        id: this.id,
        anime_name: this.nombre,
        genre: this.genre,
        chapters: this.chapter,
        rating: this.rating,
      });

      this.isCardModalActive = false;

      (this.nombre = ""),
        (this.genre = ""),
        (this.chapter = ""),
        (this.rating = "");

      this.$emit("plusOne", this.id + 1);
    },
  },
};
</script>
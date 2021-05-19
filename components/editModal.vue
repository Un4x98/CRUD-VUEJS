<template>
  <section>
    <div class="buttons">
      <b-button
        label="Editar"
        type="is-info"
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
              <b-button @click="editAnime(id)" type="is-success"
                >Aceptar</b-button
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
    };
  },
  methods: {
    editAnime(id) {
      console.log(this.anime.length);
      for (var i = 0; i < this.anime.length; i++) {
        let x = this.anime[i].id;
        if (x == id + 1) {
          (this.anime[i].id = id + 1), (this.anime[i].anime_name = this.nombre);
          this.anime[i].genre = this.genre;
          this.anime[i].chapters = this.chapter;
          this.anime[i].rating = this.rating;
        }
      }
      this.isCardModalActive = false;
    },
  },
};
</script>
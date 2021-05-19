<template>
  <b-button
    required="true"
    type="is-danger"
    label="Borrar"
    @click="deleteAnime(id)"
  ></b-button>
</template>
 
<script>
export default {
  props: ["id", "anime"],
  methods: {
    deleteAnime(id) {
      for (var i = 0; i < this.anime.length; i++) {
        let x = this.anime[i].id - 1;
        if (x == id) {
          this.anime.splice(i, 1);
        }
      }
    },
  },
};
</script>

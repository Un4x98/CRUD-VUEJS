<template>
  <section class="section">
    <basicTable :data="data"></basicTable>
    <addModal :id="id" :anime="data" @plusOne="masUno"></addModal>
  </section>
</template>

<script>
export default {
  data() {
    const data = [
      {
        id: 1,
        anime_name: "Shingeki no Kyojin",
        genre: "Seinen",
        chapters: "75",
        rating: "9",
      },
      {
        id: 2,
        anime_name: "Code Geass",
        genre: "Psicologico",
        chapters: "50",
        rating: "10",
      },
      {
        id: 3,
        anime_name: "Haikyuu",
        genre: "Deportes",
        chapters: "85",
        rating: "9",
      },
      {
        id: 4,
        anime_name: "Jujutsu Kaisen",
        genre: "Shounen",
        chapters: "24",
        rating: "8",
      },
    ];
    return {
      isCardModalActive: false,
      data,
      id: 5,
    };
  },

  methods: {
    masUno(id) {
      this.id = id;
    },
  },
};
</script>

<template>
  <section>
    <b-table :data="data">
      <b-table-column field="id" label="Id" width="40" numeric v-slot="props">
        {{ props.row.id }}
      </b-table-column>

      <b-table-column field="anime_name" label="Nombre" v-slot="props">
        {{ props.row.anime_name }}
      </b-table-column>

      <b-table-column field="genre" label="Genero" v-slot="props">
        {{ props.row.genre }}
      </b-table-column>

      <b-table-column
        field="chapters"
        label="Capitulos"
        centered
        v-slot="props"
      >
        {{ props.row.chapters }}
      </b-table-column>

      <b-table-column field="rating" label="Nota" v-slot="props">
        {{ props.row.rating }}
      </b-table-column>
      <b-table-column field="buttons" v-slot="props">
        <editModal :anime="data" v-bind:id="props.row.id - 1"></editModal>
        <deleteButton :anime="data" v-bind:id="props.row.id - 1"></deleteButton>
      </b-table-column>

      <template #empty>
        <div class="has-text-centered">No records</div>
      </template>
    </b-table>
  </section>
</template>
<script>
export default {
  props: ["data"],

  data() {
    const data = this.data;

    return {
      data,
    };
  },
};
</script>
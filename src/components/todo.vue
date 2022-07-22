<template>
  <div class="container">
    <h1 class="text-center mt-5">Ma Todo App</h1>

    <!-- input -->

    <div class="d-flex">
      <input
        v-model="tache"
        type="text"
        name=""
        placeholder="entrer une tache"
        class="form-control"
      />
      <button @click="AjouterTache" class="btn btn-warning rounded-0">
        AJOUTER UNE TACHE
      </button>
    </div>

    <!-- task table -->

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Tache</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">Modifier</th>
          <th scope="col" class="text-center">Supprimer</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(tache, index) in taches" :key="index">
          <td>
            <span :class="{ terminer: tache.status === 'Terminer' }">{{
              tache.nom
            }}</span>
          </td>
          <td>
            <span
              @click="changerStatus(index)"
              class="pointer"
              :class="{
                'text-danger': tache.status === 'A faire',
                'text-warning': tache.status === 'En cours',
                'text-success': tache.status === 'Terminer',
              }"
            >
              {{ firstCharUpper(tache.status) }}
            </span>
          </td>
          <td>
            <div class="text-center" @click="modifierTache(index)">
              <span class="fa fa-pen"> </span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="suprimerTache(index)">
              <span class="fa fa-trash"> </span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: "todo",

  data() {
    return {
      tache: "",
      tacheModifier: null,
      statusDisponible: ["A faire", "En cours", "Terminer"],
      taches: [
        {
          nom: "Danser",
          status: "A faire",
        },
        {
          nom: "Manger",
          status: "A faire",
        },
        {
          nom: "Sauter",
          status: "En cours",
        },
      ],
    };
  },
  methods: {
    AjouterTache() {
      if (this.tache.length === 0) return;
      if (this.tacheModifier === null) {
        this.taches.push({
          nom: this.tache,
          status: "A faire",
        });
      } else {
        this.taches[this.tacheModifier].nom = this.tache;
        this.tacheModifier = null;
      }
    },
    suprimerTache(index) {
      this.taches.splice(index, 1);
    },
    modifierTache(index) {
      this.tache = this.taches[index].nom;
      this.tacheModifier = index;
    },
    changerStatus(index) {
      let nveauIndex = this.statusDisponible.indexOf(this.taches[index].status);
      if (++nveauIndex > 2) nveauIndex = 0;
      this.taches[index].status = this.statusDisponible[nveauIndex];
    },
    firstCharUpper(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
  },
};
</script>
<style scoped>
.pointer {
  cursor: pointer;
}
.terminer {
  text-decoration: line-through;
}
</style>

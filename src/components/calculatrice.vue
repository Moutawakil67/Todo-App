<template>
  <h1 class="text-center mt-3">Calculatrice</h1>
  <div
    class="p-3"
    style="max-width: 400px; margin: 30px auto; background: #234"
  >
    <div
      class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark"
    >
      {{ valeurAfficher || 0 }}
    </div>

    <div class="row no-gutters">
      <div class="col-3" v-for="n in touche" :key="n">
        <div
          class="lead text-white text-center m-1 py-2 bg-vue-dark rounded survole"
          :class="{ vert: ['C', '*', '/', '-', '+', '%', '='].includes(n) }"
          @click="action(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "calculatrice",

  data() {
    return {
      valeurAfficher: "",
      signe: null,
      valeurPrecedante: "",
      touche: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
    };
  },
  methods: {
    action(n) {
      if (!isNaN(n) || n === ".") {
        this.valeurAfficher += n + "";
      }

      if (n === "C") {
        this.valeurAfficher = "";
      }
      if (n === "%") {
        this.valeurAfficher = this.valeurAfficher / 100;
      }
      if (["/", "*", "-", "+"].includes(n)) {
        this.signe = n;
        this.valeurPrecedante = this.valeurAfficher;
        this.valeurAfficher = "";
      }

      if (n === "=") {
        this.valeurAfficher = eval(
          this.valeurPrecedante + this.signe + this.valeurAfficher
        );

        (this.valeurPrecedante = ""), (this.signe = null);
      }
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.bg-vue-dark {
  background: #31475e;
}
.survole:hover {
  cursor: pointer;
  background: #3d5875;
}
.vert {
  background: #3fb984;
}
body {
  background: blueviolet;
}
</style>

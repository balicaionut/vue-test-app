<template>
  <h1>Vue Test Cegedim</h1>
  <p>
    Introduceți un șir de numere cuprinse între 100 și 999 separate prin
    virgulă:
  </p>
  <input v-model="inputText" placeholder="ex: 349, 437, 234, ..., 174" />
  <button @click="initList">Calculează</button>
  <p v-if="validList == 0">Introdu valorile</p>
  <p v-else>{{ validCheck }}</p>
  <p v-if="isValidList === false"></p>
  <p v-else>Modulo: {{ showModulo }}</p>
  <p v-if="isValidList === false"></p>
  <p element hidden v-else>Modulo: {{ findMod }}</p>

  <section class="board">
    <CardTemplate
      v-for="(card, index) in cardList"
      :key="`card-${index}`"
      :value="card.value"
      :visible="card.visible"
      :position="card.position"
      @select-card="flipCard"
    />
  </section>
</template>

<script>
import CardTemplate from "./components/CardTemplate";
import { ref, reactive, computed } from "vue";

export default {
  name: "App",
  components: {
    CardTemplate,
  },

  setup() {
    var inputText = ref("");
    var isValidList = ref(false);
    var validList = reactive([]);
    var categoryList = reactive([]);
    var finalList = reactive([]);
    var modList = reactive([]);
    var randModList = reactive([]);

    var abcList = reactive([]);

    function abc_list() {
      for (let i = 65; i < 91; i++) {
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        abcList.push(String.fromCharCode(i));
      }
    }

    // Functia inițială care este chemată la apăsarea butonului
    // Este menită să valideze formatul textului
    // Apoi să spargă valorile în cifre de câte 3 numere pe care le pune într-o listă validată
    // Iar înainte să facă asta, curăță variabilele care vor fi folosite mai târziu în caz că lista inițială se schimbă
    function initList() {
      categoryList = [0, 0, 0, 0, 0, 0, 0, 0, 0];

      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      cardList.value = cardList.value.map((card) => {
        return {
          ...card,

          visible: false,
        };
      });

      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      cardList.value.splice(0);

      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      validList.splice(0);

      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      finalList.splice(0);

      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      modList.splice(0);

      let l = inputText.value.length;
      let j = 0;
      let k = 0;
      for (let i = 0; i < l; i++) {
        if (
          (inputText.value[i] < 1 && j === 0) ||
          (isNaN(inputText.value[i]) === true && j < 3) ||
          (j === 3 && inputText.value[i] != ",")
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          isValidList.value = false;
          break;
        } else if (
          inputText.value[i] < 10 &&
          j === 0 &&
          isNaN(inputText.value[i]) === false
        ) {
          k = inputText.value[i] * 100;
          j++;
        } else if (
          inputText.value[i] < 10 &&
          j === 1 &&
          isNaN(inputText.value[i]) === false
        ) {
          k = k + inputText.value[i] * 10;
          j++;
        } else if (
          inputText.value[i] < 10 &&
          j === 2 &&
          isNaN(inputText.value[i]) === false
        ) {
          k = k + inputText.value[i] * 1;

          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          validList.push(k);
          j++;
          k = 0;

          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          isValidList.value = true;
        } else if (inputText.value[i] === "," && j === 3) {
          j = 0;
        } else {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          isValidList.value = false;
        }
      }
      return validList;
    }

    // Ajută la afișarea textului aferent validității
    const validCheck = computed(() => {
      if (isValidList.value === false) {
        return "The list is not valid";
      } else {
        return "Maximele din clase sunt: " + maxListBuilder.value;
      }
    });

    // Compară valorile din lista validată cu valorile din lista pe categorii, iar dacă găsește valori mai mari decât cele prezente în categoria aferentă, le înlocuiește
    const compareNumbers = computed(() => {
      let l = validList.length;
      for (let i = 0; i < l; i++) {
        if (
          validList[i] > 99 &&
          validList[i] < 200 &&
          categoryList[0] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[0] = validList[i];
        } else if (
          validList[i] > 199 &&
          validList[i] < 300 &&
          categoryList[1] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[1] = validList[i];
        } else if (
          validList[i] > 299 &&
          validList[i] < 400 &&
          categoryList[2] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[2] = validList[i];
        } else if (
          validList[i] > 399 &&
          validList[i] < 500 &&
          categoryList[3] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[3] = validList[i];
        } else if (
          validList[i] > 499 &&
          validList[i] < 600 &&
          categoryList[4] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[4] = validList[i];
        } else if (
          validList[i] > 599 &&
          validList[i] < 700 &&
          categoryList[5] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[5] = validList[i];
        } else if (
          validList[i] > 699 &&
          validList[i] < 800 &&
          categoryList[6] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[6] = validList[i];
        } else if (
          validList[i] > 799 &&
          validList[i] < 900 &&
          categoryList[7] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[7] = validList[i];
        } else if (
          validList[i] > 899 &&
          validList[i] < 1000 &&
          categoryList[8] < validList[i]
        ) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          categoryList[8] = validList[i];
        }
      }
      return categoryList;
    });

    // Lista finală de maxime
    const maxListBuilder = computed(() => {
      for (let i = 0; i < 9; i++) {
        if (compareNumbers.value[i] > 0) {
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          finalList.push(compareNumbers.value[i]);
        }
      }
      return finalList;
    });

    // Calculează modulo și este folosită pentru afișare
    const showModulo = computed(() => {
      let mod = 0;
      let intr = 0;
      let l = finalList.length;
      for (let i = 0; i < l; i++) {
        intr = Math.trunc(finalList[i] / 26);
        mod = finalList[i] - intr * 26;

        abc_list();
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        modList.push(abcList[mod]);
      }
      return modList;
    });

    // Construiește lista de 16 valori random din modulo
    const findMod = computed(() => {
      if (modList.length > 0) {
        return generateRandList.value;
      }
      return modList;
    });

    // Alocă și construiește cardurile
    const generateRandList = computed(() => {
      let rand = 0;
      for (let i = 0; i < 16; i++) {
        rand = Math.floor(Math.random() * modList.length);
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        randModList[i] = modList[rand];
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        cardList.value.push({
          value: modList[rand],
          visible: false,
          position: i,
        });
      }
      return randModList;
    });

    const cardList = ref([]);

    // Funcția pentru întoarcerea cardurilor
    const flipCard = (payload) => {
      cardList.value[payload.position].visible = true;
    };

    return {
      initList,
      inputText,
      validList,
      validCheck,
      compareNumbers,
      maxListBuilder,
      finalList,
      categoryList,
      findMod,
      cardList,
      flipCard,
      randModList,
      generateRandList,
      isValidList,
      showModulo,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.board {
  display: grid;
  grid-template-columns: repeat(4, 120px);
  grid-template-rows: repeat(4, 120px);
  grid-column-gap: 24px;
  grid-row-gap: 24px;
  justify-content: center;
}
</style>

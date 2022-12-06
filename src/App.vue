<script setup lang="ts">
import { ref } from "vue";
import redflags from "@/stores/redflags.json";

const soma = ref(0);
const marcados = ref([{ flag: "", value: 0 }]);

marcados.value.pop();

const addValue = (flag: string, value: string) => {
  if (marcados.value.some((e) => e.flag === flag)) {
    marcados.value.splice(
      marcados.value.findIndex((e) => e.flag === flag),

      1
    );

    soma.value -= +value;
  } else {
    marcados.value.push({ flag: flag, value: +value });

    soma.value += +value;
  }
};
</script>

<template>
  <main>
    <div class="container">
      <label :key="i" v-for="({ flag, valor }, i) in redflags" :for="flag">
        <input
          class="cb select"
          :id="flag"
          @click="addValue(flag, valor)"
          type="checkbox"
        />
        {{ flag }}
      </label>
    </div>
    <div v-if="marcados.length > 0" class="container-result">
      <div class="result" :key="i" v-for="({ flag, value }, i) in marcados">
        <div class="flag">
          {{ flag }}
        </div>
        <div class="line"></div>
        <div class="value">
          {{ value }}
        </div>
      </div>
      <br />
      <div class="result">
        <div class="flag">REDFLAGS</div>
        <div class="line"></div>
        <div class="value">{{ marcados.length }} de {{ redflags.length }}</div>
      </div>
      <div class="result">
        <div class="flag">TOTAL</div>
        <div class="line"></div>
        <div class="value">
          {{ soma }}
        </div>
      </div>
    </div>
  </main>
</template>

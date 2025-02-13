<script lang="ts">
import { obterCategorias } from '@/http/index';
import type ICategory from '@/interfaces/ICategory';

export default {
  data() {
    return {
      categorias: [] as ICategory[]
    }
  },
  async created() {
    this.categorias = await obterCategorias();
  }
}
</script>
<template>
    <section class="selecionar-ingredientes">
      <h1 class="cabecalho titulo-ingredientes">Ingredients</h1>

      <p class="paragrafo-lg instrucoes">
        Select below the ingredients you want to use in this recipe:
      </p>

      <ul class="categorias">
        <li v-for="categoria in categorias" :key="categoria.nome">
            {{ categoria.nome }}
        </li>
    </ul>

      <p class="paragrafo dica">
        *Please note: we assume you have salt, pepper and water at home.
      </p>
    </section>
  </template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}
</style>
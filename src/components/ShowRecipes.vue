<script lang="ts">
import { obterReceitas } from '@/http';
import MainButton from './MainButton.vue';
import type IRecipe from '@/interfaces/IRecipe';
import CardRecipe from './CardRecipe.vue';
import type { PropType } from 'vue';
import { itensDeLista1EstaoEmLista2 } from '@/helpers/list';

export default {
  props: {
    ingredientes: { type: Array as PropType<string[]>, required: true }
  },
  data() {
    return {
      receitasEncontradas: [] as IRecipe[]
    };
  },
  async created() {
    const receitas = await obterReceitas();
    this.receitasEncontradas = receitas.filter((receita) => {
      // Lógica que verifica se posso fazer receita:
      // Todos os ingredientes de uma receita devem estar inclusos na minha lista de ingredientes
      // Se sim, devemos retornar `true`

      const possoFazerReceita = itensDeLista1EstaoEmLista2(receita.ingredientes, this.ingredientes);

      return possoFazerReceita;
    })
  },
  components: { MainButton, CardRecipe },
  emits: ['editarReceitas']
}
</script>

<template>
  <section class="mostrar-receitas">
    <h1 class="cabecalho titulo-receitas">Receipe</h1>

    <p class="paragrafo-lg resultados-encontrados">
      Results found: {{ receitasEncontradas.length }}
    </p>

    <div v-if="receitasEncontradas.length" class="receitas-wrapper">
      <p class="paragrafo-lg informacoes">
        Check out the recipe options we found with the ingredients you have around!
      </p>

      <ul class="receitas">
        <li v-for="receita of receitasEncontradas" :key="receita.nome">
          <CardRecipe :receita="receita" />
        </li>
      </ul>
    </div>

    <div v-else class="receitas-nao-encontradas">
      <p class="paragrafo-lg receitas-nao-encontradas__info">
        Oops, we couldn't find any results for your match. Let's try again?
      </p>

      <img src="../assets/images/sem-receitas.png"
        alt="Desenho de um ovo quebrado. A gema tem um rosto com uma expressão triste.">
    </div>

    <MainButton texto="Edit list" @click="$emit('editarReceitas')" />
  </section>
</template>

<style scoped>
.mostrar-receitas {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.titulo-receitas {
  color: var(--verde-medio, #3D6D4A);
  margin-bottom: 1.5rem;
}

.resultados-encontrados {
  color: var(--verde-medio, #3D6D4A);
  margin-bottom: 0.5rem;
}

.receitas-wrapper {
  margin-bottom: 3.5rem;
}

.informacoes {
  margin-bottom: 2rem;
}

.receitas {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.receitas-nao-encontradas {
  margin-bottom: 2rem;
}

.receitas-nao-encontradas__info {
  margin-bottom: 0.5rem;
}

@media only screen and (max-width: 767px) {
  .receitas-wrapper {
    margin-bottom: 2rem;
  }
}
</style>
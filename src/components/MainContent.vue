<script lang="ts">
import SelectIngredients from './SelectIngredients.vue';
import Tag from './Tag.vue';
import YourList from './YourList.vue';

export default {
  data() {
    return {
      ingredientes: [] as string[],
    };
  },
  components: { SelectIngredients, Tag, YourList},
  methods: { 
    adicionarIngrediente(ingrediente: string){
      this.ingredientes.push(ingrediente)
    },
    removerIngrediente(ingrediente: string){
      this.ingredientes = this.ingredientes.filter(i => i!== ingrediente)
    }
  }
}
</script>

<template>
  <main class="conteudo-principal">
    <YourList :ingredientes="ingredientes" />

    <SelectIngredients @adicionar-ingrediente="adicionarIngrediente" @remover-ingrediente="removerIngrediente"/>
  </main>
</template>

<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #FFFAF3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

.ingrediente {
  display: inline-block;
  border-radius: 0.5rem;
  min-width: 4.25rem;
  padding: 0.5rem;
  text-align: center;
  transition: 0.2s;
  color: var(--creme, #FFFAF3);
  background: var(--coral, #F0633C);
  font-weight: 700;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>
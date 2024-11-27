<script lang="ts">
import { obterReceitas } from "@/http";
import type ICategoria from "@/interfaces/ICategoria";
import CardReceita from "@/components/CardReceita.vue";

export default {
  data() {
    return {
      receitas: [] as ICategoria[],
    };
  },
  async created() {
    this.receitas = await obterReceitas();
  },
  components: {
    CardReceita,
  },
};
</script>

<template>
  <section class="seleciona-ingredientes">
    <h1 class="cabecalho titulo-ingredientes">Receitas</h1>
    <p class="paragrafo-lg instrucoes resultado">Resultados encontrados: 8</p>
    <p class="paragrafo-lg instrucoes">
      Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!
    </p>

    <ul class="categorias">
      <li v-for="receita in receitas" :key="receita.nome">
        <CardReceita
          :receita="receita"
        />
      </li>
    </ul>

    <p class="paragrafo dica">
      *Atenção: consideramos que você tem em casa sal, pimenta e água.
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
  text-align: center;
  color: var(--verde-medio, #3d6d4a);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  text-align: center;
  margin-bottom: 2rem;
}

.resultado {
  color: var(--verde-medio, #3d6d4a);
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

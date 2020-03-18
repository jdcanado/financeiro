<template>
  <div class="content">
    <div class="md-layout">
      <div
        class="md-layout-item md-medium-size-50 md-xsmall-size-30 md-size-50"
      > 
       <md-table v-model="searched" md-sort="name" md-sort-order="asc" md-card md-fixed-header>
         <md-table-toolbar>
           <div class="md-toolbar-section-start">
             <h1 class="md-title">Categorias de pagamento</h1>
           </div>
           <md-field md-clearable class="md-toolbar-section-end">
             <md-input placeholder="Busca por nome..." v-model="search" @input="searchOnTable" />
           </md-field>
         </md-table-toolbar>

         <md-table-empty-state
           md-label="Nenhuma categoria cadastrada"
           :md-description="`Nenhuma categoria encontrada com o termo '${search}'. Tente uma busca com um termo diferente.`">
           <md-button class="md-primary md-raised" @click="addCategoriaPagamento">Adicionar</md-button>
         </md-table-empty-state>

         <md-table-row slot="md-table-row" slot-scope="{ item }">
           <md-table-cell md-label="Id" md-sort-by="id" md-numeric>{{ item.id }}</md-table-cell>
           <md-table-cell md-label="Descrição" md-sort-by="descricao">{{ item.descricao }}</md-table-cell>
           <md-table-cell md-label="Editar"></md-table-cell>
           <md-table-cell md-label="Inativar"></md-table-cell>
         </md-table-row>
       </md-table> 
      </div>
    </div>  
  </div>
</template>

<script>
  const toLower = text => {
    return text.toString().toLowerCase()
  }

  const searchByName = (items, term) => {
    if (term) {
      return items.filter(item => toLower(item.descricao).includes(toLower(term)))
    }

    return items
  }

  export default {
    name: 'TableSearch',
    data: () => ({
      search: null,
      searched: [],
      categoriaPagamentos: [
        {
          id: 1,
          descricao: "Conta de energia elétrica"
        },
        {
          id: 2,
          descricao: "Conta de água e esgoto"
        }
      ]
    }),
    methods: {
      addCategoriaPagamento () {
        window.alert('Noop')
      },
      searchOnTable () {
        this.searched = searchByName(this.categoriaPagamentos, this.search)
      }
    },
    created () {
      this.searched = this.categoriaPagamentos
    }
  }
</script>

<style lang="scss" scoped>
  .md-field {
    max-width: 300px;
  }
</style>

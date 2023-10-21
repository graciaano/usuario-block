<template>
    <div id="app">
      <h1>Usuários Bloqueados</h1>
      <div class="custom-table-container">
        <div class="custom-table">
          <table>
            <thead>
              <tr>
                <th>Selecione</th>
                <th @click="ordenarPor('nome')" :class="{ 'asc': colunaOrdenada === 'nome' && ordemAscendente, 'desc': colunaOrdenada === 'nome' && !ordemAscendente }">Nome</th>
                <th @click="ordenarPor('numero')" :class="{ 'asc': colunaOrdenada === 'numero' && ordemAscendente, 'desc': colunaOrdenada === 'numero' && !ordemAscendente }">Número</th>
                <th @click="ordenarPor('status')" :class="{ 'asc': colunaOrdenada === 'status' && ordemAscendente, 'desc': colunaOrdenada === 'status' && !ordemAscendente }">Status</th>
                <th>Ações</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in items" :key="index">
                <td>
                  <input type="checkbox" v-model="item.selecionado"  />
                </td>
                <td>
                  <input type="text" v-model="item.nome" />
                </td>
                <td>
                  <input type="text" v-model="item.numero" />
                </td>
                <td>
                  <input type="text" v-model="item.status" />
                </td>
                <td class="delete-button-container">
                  <button @click="excluirItem(index)" class="delete-button">Excluir</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        items: [
          { nome: 'junior', numero: '(81)940028922', status: 'Bloqueado', selecionado: false },
          { nome: 'graciano', numero: '(81)940028922', status: 'Bloqueado', selecionado: false },
          { nome: 'gracianojunior', numero: '(81)940028922', status: 'Bloqueado', selecionado: false }
        ],
        colunaOrdenada: '',
        ordemAscendente: true
      };
    },
    methods: {
      excluirItem(index) {
        this.items.splice(index, 1);
      },
      excluirItensSelecionados() {
        this.items = this.items.filter(item => !item.selecionado);
      },
      ordenarPor(coluna) {
        if (this.colunaOrdenada === coluna) {
          this.ordemAscendente = !this.ordemAscendente;
        } else {
          this.ordemAscendente = true;
        }
  
        this.colunaOrdenada = coluna;
  
        this.items.sort((a, b) => {
          const valorA = a[coluna].toLowerCase();
          const valorB = b[coluna].toLowerCase();
          if (valorA < valorB) {
            return this.ordemAscendente ? -1 : 1;
          }
          if (valorA > valorB) {
            return this.ordemAscendente ? 1 : -1;
          }
          return 0;
        });
      }
    }
  };
  </script>
  
  <style scoped>
    .asc::after {
      content: '↑';
    }
  
    .desc::after {
      content: '↓';
    }
  
    .delete-button {
      background-color: red;
      color: white;
      border: none;
      padding: 5px 1px;
      border-radius: 4px;
      cursor: pointer;
    }
  
    .delete-button:hover {
      background-color: darkred;
    }
  
    .custom-checkbox {
      width: 15px;
      height: 15px;
      appearance: none;
      border: 1.5px solid rgb(59, 57, 57);
      border-radius: 4px;
      background-color: #fff;
      cursor: pointer;
      outline: none;
    }
  
    .custom-checkbox:checked {
      background-color: green;
      border: 2px solid green;
    }
  
    .custom-table-container {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 60vh;
      background-color: white;
    }
  
   
  </style>
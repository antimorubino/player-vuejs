<script setup>
import DataTable from 'datatables.net-vue3'
import DataTablesCore from 'datatables.net-bs5'

import { ref } from 'vue'

import Riproduci from '../components/Riproduci.vue'
import $ from 'jquery';

DataTable.use(DataTablesCore)

const columns = [
  { data: null,
    render: function(data) {
      return `<a href="#?" data-id="${data.id}" data-src="${data.src}" data-titolo="${data.titolo}" class="play">${data.titolo}</a>`;
      //return `<button type="button" data-id="${data.id}" data-src="${data.src}" data-titolo="${data.titolo}" class="btn btn-link play" value="${data.src}">${data.titolo}</button>`;
    }
  }
];

var idP = '';
var src = '';
var titolo = '';

$(document).on('click', '.play', function(){
  idP = $(this).data("id");
  src = $(this).data("src");
  titolo = $(this).data("titolo");

  $("#audio").get(0).play();
  //audio.play();

  //console.log(src);
});

defineProps({
  idP: String,
  titolo: String,
  src: String
})



</script>

<template>

  <div class="container">
    <DataTable :columns="columns" ajax="/data.json" class="table table-striped table-bordered" 
      :options="{
        language: {
          'search': 'Cerca',
          'sEmptyTable': 'Nessun dato presente nella tabella',
          'sInfo': 'Vista da _START_ a _END_ di _TOTAL_ elementi',
          'sInfoEmpty': 'Vista da 0 a 0 di 0 elementi',
          'sInfoFiltered': '(filtrati da _MAX_ elementi totali)',
          'sInfoPostFix': '',
          'sInfoThousands': '.',
          'sLengthMenu': 'Visualizza _MENU_ elementi',
          'sLoadingRecords': 'Caricamento...',
          'sProcessing': 'Elaborazione...',
          'sZeroRecords': 'La ricerca non ha portato alcun risultato.',
          'oPaginate': {
            'sFirst': 'Inizio',
            'sPrevious': 'Precedente',
            'sNext': 'Successivo',
            'sLast': 'Fine'
          },
          'oAria': {
            'sSortAscending':  ': attiva per ordinare la colonna in ordine crescente',
            'sSortDescending': ': attiva per ordinare la colonna in ordine decrescente'
          }
        },
        'order': [[ 0, 'desc' ]],
        'pageLength': 25,
        //'sScrollY' : '80',
      }"    
    >
    <thead>
      <tr>
        <th width="50%">Titolo</th>
      </tr>
    </thead>
    </DataTable>
  </div>

  <div class="sepAudio"></div>

  <div class="container psAudio">
    <Riproduci :idP :src :titolo />
  </div>

</template>

<style>

.tableSong {
  padding: 15px 0;
}

.psAudio {
  position: -webkit-sticky;
  position: sticky;
  bottom: 0;
  /*width: 100%;*/
  /*margin-top: 50px; */
  background: #fff;
  border-top: 1px solid #ccc;
  padding: 0 10px;
  z-index: 9999;
}

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>

<template>
  <div>
    <v-card-title>
    <h1  max-height="600">ТС на приемке по качеству июнь 2022</h1> 
    <v-spacer></v-spacer>
    <v-text-field
        v-model="search"
        label="Поиск"
        single-line
        hide-details
      ></v-text-field>
      <!--append-icon="search"-->  
    </v-card-title>
     <v-dialog
      v-model="dialog"
      persistent
      max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="#EA5F4B"
          dark
          v-bind="attrs"
          v-on="on">
          Open Dialog
        </v-btn>
      </template>

      <v-card>
        <v-card-text>
          <v-container>
            content
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false">
            Close
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false">
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
<div class="filters-line">
    <v-chip
        :key="item.field"
        v-for="item in items"
        class="mr-2"
        @click="$emit('click', item)"
    >
      {{ item.label }}
    </v-chip>
    <v-chip @click="$emit('clear')">Сбросить фильтры</v-chip>
  </div>
  <v-card>
    <v-data-table
      :headers="headers"
      :items="ts"
      :search="search"
    >
    <template v-slot:items="props">
        <td>{{ props.item.name }}</td>
        <td id="transport" name="transport" class="transport" placeholder="transport">{{ props.item.transport}} </td>
      </template>
      <template v-slot:no-results>
        <v-alert :value="true" color="error" icon="warning">
          Your search for "{{ search }}" found no results.
        </v-alert>
      </template>
    </v-data-table>
  </v-card>
  </div>
</template>

<script>
import axios from "axios";
import { server } from "../utils/helper";
  export default {
    data () {
      return {
        page: 1,
        pageCount: 0,
        itemsPerPage: 10,
        search: '',
        transport: " ",
        items: [
      { label: 'Поставщик Лен-Инвест', value: 'Лен-Инвест', field: 'Поставщик' },
      { label: 'Все ТСы с кодом 34554', value: '34554', field: 'transport' }
    ],
        headers: [
          {
            text: 'ID',
            align: 'start',
            sortable: false,
            value: 'ID',
          },
          { text: 'transport', value: 'transport' },
        ],
        ts: [
          {
            ID: '34554',
            transport: 'transport',
          },
        ],
        dialog: false,
      }
    },
        
      filters: {
      'filt': function(value) {
      return value.ToUpperCase();
      }
  },

      created() {
      this.load()
      // this.getOne()
      },
      methods: {
      load(){
      // new td = new Transport()
      axios.get(`${server.baseURL}/compliet-cargo/TS`).then(data => (this.ts = data.data))
      console.log(ts)
      },
}
  }
</script>
<!-- created() {
    this.date = new Date().toLocaleDateString();
    },
    methods: {
    Table() {
      let date = {
        transport: this.transport,
        date: this.date
      };
      this.__submitToServer(postData);
    },
    __submitToServer(data) {
      axios.post(`${server.baseURL}compliet-cargo/TS`, data).then(data => {
        console.log(data);
        router.push({ name: "home" });
      });
    }   
    }, -->

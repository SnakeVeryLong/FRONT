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

    <filters-line
        class="my-5"
        @click="handleFilterLineItemClick"
        @clear="clearFilterLines"
    />

  <v-card>

    <v-data-table
      :headers="headers"
      :items="items"
      :search="search"
    >

    <!-- @click="dialog = false"-->
    
    <template v-slot:items="props">
        <td>{{ props.item.name }}</td>
        <td id="transportNumber" name="transportNumber" class="transportNumber" placeholder="transportNumber">{{ props.item.transportNumber }} </td>


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
  import FiltersLine from '@/components/FiltersLine.vue';
  import axios from 'axios';
  import helper from '../utils/helper.js';

  const isObjectEmpty = (obj) => {
    return obj
    && Object.keys(obj).length === 0
    && Object.getPrototypeOf(obj) === Object.prototype;
  }
  export const server = {
    baseURL: 'http://localhost:3000'
  }

  export default {
    components: {
      FiltersLine
    },
    data () {
      return {
        page: 1,
        pageCount: 0,
        itemsPerPage: 10,
        search: '',
        transportNumber: [],
        headers: [
          {
            text: 'ID',
            align: 'start',
            sortable: false,
            value: 'ID',
          },
          { text: 'transportNumber', value: 'transportNumber' },
        ],

        dialog: false,
        filters: {}
      }
      //,
      //mounted() {
        //this.axios.get()
      //}
    },

    
    computed: {
      items() {
        return this.ts?.filter((item) => {
          if (isObjectEmpty(this.filters)) return true;
          return !Object.keys(this.filters).some((field) => this.filters[field] !== item[field]);
        });
      }
    },
    methods: {
      clearFilterLines() {
        this.filters = {};
      },
      handleFilterLineItemClick({ field, value }) {
        this.filters = {...this.filters, [field]: value };
      }
    },
      created() {
      this.load()
      // this.getOne()
      },
      methods: {
      async load(){
      // new td = new Transport()
     // axios.get(`${server.baseURL}/compliet-cargo/TS`).then(data => {this.transportNumber = data.data; console.log(data.data)})
      const result = await axios.get(`${server.baseURL}/compliet-cargo/TS`);
      this.transportNumber = result.data;
      console.log(this.transportNumber);
      },
      }
  }
</script>


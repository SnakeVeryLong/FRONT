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
          <v-card-title>
          <span class="text-h5">Приемка по качеству</span>
          <h5>
            Транспортное средство #...
            Накладная №...
          </h5>
        </v-card-title>

        <v-card-text>
          <h5>Виды лома заявленные поставщиком</h5>
          <v-container>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
              <h5>Виды лома</h5> 
                <v-text-field
                  label="5а"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
               <h5>Вес (Т)</h5> 
                <v-text-field
                  label="0,630"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
               <h5>Вес по приемке (Т)</h5> 
                <v-text-field
                  label=" "  
                  persistent-hint
                  required
                  outlined
                  dense
                ></v-text-field>
              </v-col>

              <v-col
                cols="12"
                sm="6"
                md="4"
              >
              <h5>Виды лома</h5> 
                <v-text-field
                  label="7а"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
               <h5>Вес (Т)</h5> 
                <v-text-field
                  label="0,840"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
               <h5>Вес по приемке (Т)</h5> 
                <v-text-field
                  label=" "  
                  persistent-hint
                  required
                  outlined
                  dense
                ></v-text-field>
              </v-col>
              
              
              <h5>Виды лома незаявленные поставщиком</h5>
              <v-spacer></v-spacer>
              <v-col
                cols="12"
                sm="6"
                md="8"
              >
              <h5>Виды лома</h5>

                 <v-autocomplete
            ref="name"
            
            :items="JSON.stringify(lom)"
            label="Выбор лома"
            placeholder="Вид..."
            required
            clearable
          ></v-autocomplete>
           </v-col>
           <v-col
                cols="12"
                sm="6"
                md="4"
              >
               <h5>Вес по приемке (Т)</h5> 
                <v-text-field
                  label=" "  
                  persistent-hint
                  required
                  outlined
                  dense
                  clearable
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="8"
              >
              <h5>Виды лома</h5>

          <v-autocomplete
            ref="name"
            
            :items="JSON.stringify(lom)"
            label="Выбор лома"
            placeholder="Вид..."
            required
            clearable
          ></v-autocomplete>
           </v-col>
           <v-col
                cols="12"
                sm="6"
                md="4"
              >
               <h5>Вес по приемке (Т)</h5> 
                <v-text-field
                  label=" "  
                  persistent-hint
                  required
                  outlined
                  dense
                  clearable
                ></v-text-field>
              </v-col>

              <h5>Наличие мусора обнаруженного при проверке</h5>
              <v-spacer></v-spacer>
              <v-col
                cols="12"
                sm="6"
                md="8"
              >
               <h5>Неотделимый мусор</h5> 
                <v-text-field
                  label=" "  
                  persistent-hint
                  required
                  outlined
                  dense
                  clearable
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
               <h5>Вес (Т)</h5> 
                <v-text-field
                  label=" "  
                  persistent-hint
                  required
                  outlined
                  dense
                  clearable
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="8"
              >
               <h5>Отделимый мусор</h5> 
                <v-text-field
                  label=" "  
                  persistent-hint
                  required
                  outlined
                  dense
                  clearable
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
               <h5>Вес (Т)</h5> 
                <v-text-field
                  label=" "  
                  persistent-hint
                  required
                  outlined
                  dense
                  clearable
                ></v-text-field>
              </v-col>
              
            </v-row>
          </v-container>
          <small>*Сохранить перед закрытием окна</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
            Close
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
            Save
          </v-btn>
        </v-card-actions>


        </v-card-text>
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
      :items="transport"
      :search="search"
    >

    <!-- @click="dialog = false"-->
    
    <template v-slot:items="props">
        <td>{{ props.item.name }}</td>
        <td id="transportNumber" name="transportNumber" class="transportNumber" placeholder="transportNumber">{{ props.item.transport }} </td>
        <td id="documentNumber" name="documentNumber" class="documentNumber" placeholder="documentNumber">{{ props.item.transport }} </td>
        <td id="weightFirst" name="weightFirst" class="weightFirst" placeholder="weightFirst">{{ props.item.transport }} </td>
        <td id="arrivalDate" name="arrivalDate" class="arrivalDate" placeholder="arrivalDate">{{ props.item.transport }} </td>
        <td id="shipmentDate" name="shipmentDate" class="shipmentDate" placeholder="shipmentDate">{{ props.item.transport }} </td>
         <!--<td id="problemId" name="problemId" class="problemId" placeholder="problemId">{{ props.item.transport }} </td>-->


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
        lom: [],
        arr: ['name'],
        cargoType: [],
        transport: [],
        headers: [
          {
            align: 'start',
            sortable: false,
          },
          { text: 'ID', value: 'id' },
          { text: '№ ТС', value: 'transportNumber' },
          { text: '№ Накладной', value: 'documentNumber' },
          { text: 'Вес', value: 'weightFirst' },
          { text: 'Дата отгрузки', value: 'arrivalDate' },
          { text: 'Дата', value: 'shipmentDate' },
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
      this.load();
      // this.getOne()
      this.loadCargoType()
      },
      methods: {
      async load(){
      // new td = new Transport()
      axios.get(`${server.baseURL}/compliet-cargo/TS`).then(data => (this.transport = data.data))
     /* const result = await axios.get(`${server.baseURL}/compliet-cargo/TS`);
      this.transportNumber = result.data;
      console.log(this.transportNumber);*/
      },

      async loadCargoType(){
      // new td = new Transport()
      axios.get(`${server.baseURL}/compliet-cargo/cargoType`).then(data => (this.lom = data.data))
     /* const result = await axios.get(`${server.baseURL}/compliet-cargo/cargoType`);
     
      this.cargoType = result.data;
      console.log(this.cargoType);*/


      }
    }
  }
</script>


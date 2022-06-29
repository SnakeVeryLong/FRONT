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
        <td id="transport" name="transport" class="form-control" placeholder="Enter title">{{ props.item.transport }} </td>
        <!-- <td id="title" name="title" class="text-xs-right">{{ props.item.nТС }}</td> -->
        <!-- <td id="title" name="title" class="text-xs-right">{{ props.item.nНакладной }}</td> -->
        <!-- <td id="title" name="title" class="text-xs-right">{{ props.item.ДатаОтгрузки }}</td> -->
        <!-- <td id="title" name="title" class="text-xs-right">{{ props.item.Поставщик }}</td> -->
        <!-- <td id="title" name="title" class="text-xs-right">{{ props.item.Отправитель }}</td> -->
        <!-- <td id="title" name="title" class="text-xs-right">{{ props.item.МестоОтправления }}</td> -->
        <!-- <td id="title" name="title" class="text-xs-right">{{ props.item.Направление }}</td> -->
        <!-- <td id="title" name="title" class="text-xs-right">{{ props.item.Получатель }}</td> -->
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

  const isObjectEmpty = (obj) => {
    return obj
    && Object.keys(obj).length === 0
    && Object.getPrototypeOf(obj) === Object.prototype;
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
        transport: " ",
        headers: [
          {
            text: 'ID',
            align: 'start',
            sortable: false,
            value: 'ID',
          },
          { text: 'transport', value: 'transport' },
          { text: '№ТС', value: 'nТС' },
          { text: '№Накладной', value: 'nНакладной' },
          { text: 'Дата отгрузки', value: 'ДатаОтгрузки' },
          { text: 'Поставщик', value: 'Поставщик' },
          { text: 'Отправитель', value: 'Отправитель' },
          { text: 'Место отправления', value: 'МестоОтправления' },
          { text: 'Направление', value: 'Направление' },
          { text: 'Получатель', value: 'Получатель' },
        ],
        ts: [
          {
            transport: '34554',
            ТС: 'img',
            nТС: 'U2002505',
            nНакладной: 'ЭИ588798',
            ДатаОтгрузки: '27.07.20',
            Поставщик: 'Лен-Инвест',
            Отправитель: 'ООО "КЭЛ" (0556678888)',
            МестоОтправления: 'ЛЕНИНСК -КУЗНЕЦКИЙ_1',
            Направление: 'ЗСМК ОАО',
            Получатель: 'ЗСМК (05785874)', 
          },
          {
            transport: '34555',
            ТС: 'img',
            nТС: 'U2002505',
            nНакладной: 'ЭИ588798',
            ДатаОтгрузки: '27.07.20',
            Поставщик: 'Лен-Инвест',
            Отправитель: 'ООО "КЭЛ" (0556678888)',
            МестоОтправления: 'ЛЕНИНСК -КУЗНЕЦКИЙ_1',
            Направление: 'ЗСМК ОАО',
            Получатель: 'ЗСМК (05785874)',
          },
          {
            transport: '34556',
            ТС: 'img',
            nТС: 'U2002505',
            nНакладной: 'ЭИ588798',
            ДатаОтгрузки: '27.07.20',
            Поставщик: 'Лен-Инвест2',
            Отправитель: 'ООО "КЭЛ" (0556678888)',
            МестоОтправления: 'ЛЕНИНСК -КУЗНЕЦКИЙ_1',
            Направление: 'ЗСМК ОАО',
            Получатель: 'ЗСМК (05785874)',
          },
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
    }
  }
</script>


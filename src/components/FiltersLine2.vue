<template>
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
</template>

<script>
export default {
  name: 'FiltersLine',
  data: () => ({
    items: [
      { label: 'Поставщик Лен-Инвест', value: 'Лен-Инвест', field: 'Поставщик' },
      { label: 'Все ТСы с кодом 34554', value: '34554', field: 'transport' }
    ]
  })
}
</script>
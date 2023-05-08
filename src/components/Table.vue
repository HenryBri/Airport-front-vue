<template>
  <table>
    <caption>
      {{
        caption
      }}
    </caption>
    <tr>
      <th v-for="(keyName, index) in Object.keys(items[0])" :key="index">
        {{ keyName }}
      </th>
      <slot name="additionalHeaders"></slot>
    </tr>
    <tr v-for="item in items" :key="item.id">
      <td v-for="(keyName, index) in Object.keys(item)" :key="index">
        {{ item[keyName] }}
      </td>
      <td v-if="showControlls">
        <button @click="$emit('show', item)">Show Info</button>
      </td>
      <slot name="additionalColumns"></slot>
    </tr>
  </table>
</template>

<script>
export default {
  props: {
    caption: String,
    items: Array,
    showControlls: Boolean,
  },
  computed: {
    keyNames() {
      return this.item.length > 0 ? Object.keys(this.items[0]) : [];
    },
  },
};
</script>

<style>
table,
th,
td {
  border: 1px solid black;
}
</style>

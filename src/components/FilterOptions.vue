<template>
  <div class="mb-5 flex w-full justify-center gap-3 xs:flex-col md:flex-row">
    <Dropdown
      classes="flex-1  basis-2/3"
      :shadow="true"
      :options="genres"
      :searchable="true"
      mode="tags"
      placeholder="Filter by genres"
      @on-selected-options="(ev) => $emit('on-selected-genres', ev)"
    />
    <Dropdown
      classes="flex-1 basis-1/3"
      :shadow="true"
      :options="filteringModes"
      :prefilled-options="[filteringModes[0].value]"
      :searchable="false"
      mode="single"
      placeholder="Select filtering mode"
      @on-selected-options="(ev) => $emit('on-selected-mode', ev)"
    />
  </div>
</template>

<script>
import { computed, ref } from 'vue';
import Dropdown from '@/components/shared/Dropdown.vue';

export default {
  setup() {
    const filteringModes = computed(() => [
      {
        name: 'Any of the following genres',
        value: 'any',
      },
      {
        name: 'All of the following genres',
        value: 'all',
      },
    ]);

    return {
      selectedFilters: ref([]),
      filteringModes,
    };
  },
  emits: ['on-selected-genres', 'on-selected-mode'],
  components: {
    Dropdown,
  },
  props: {
    genres: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped></style>

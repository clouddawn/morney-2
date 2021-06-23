<template>
  <Layout>
    <Types class="x" :value.sync="yyy"/>
  </Layout>
</template>

<style scoped lang="scss">
  .x ::v-deep li {
    &.selected {
      background: #f60;
    }
  }
</style>

<script lang="ts">
  import Types from '@/components/Money/Types.vue';
  import Vue from 'vue';
  import {Component} from 'vue-property-decorator';

  @Component({
    components: {Types}
  })
  export default class Statistics extends Vue {
    yyy = '-';
  }
</script>

<style lang="scss" scoped>

</style>
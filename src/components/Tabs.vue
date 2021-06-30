<template>
  <div>
    <ul class="tabs" :class="{[classPrefix + '-tabs']:classPrefix}">
      <li v-for="item in dataSource" :key="item.value" class="tabs-item" :class="liClass(item)" @click="select(item)">
        {{ item.text }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop} from 'vue-property-decorator';

  type DataSourceItem = { text: string, value: string }
  // let is = localStorage.getItem('is');
  @Component
  export default class Tabs extends Vue {
    @Prop({required: true, type: Array}) dataSource!: DataSourceItem[];
    @Prop(String)
    readonly value!: string;
    @Prop(String)
    classPrefix?: string;

    liClass(item: DataSourceItem) {
      return {selected: item.value === this.value, [this.classPrefix + '-tabs-item']: this.classPrefix};
    }
    // initialSelect(is: string) {
    //   this.$emit('update:value', is);
    // }
    select(item: DataSourceItem) {
      this.$emit('update:value', item.value);
      console.log(item);
      console.log(this.dataSource);
    }
  }
</script>

<style lang="scss" scoped>
  .tabs {
    background: #ffb73b;
    color: white;
    display: flex;
    text-align: center;
    font-size: 24px;
    margin-top: 1px;

    &-item {
      width: 50%;
      height: 64px;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;

      &.selected {
        background: #f60;

      }
    }
  }
</style>
<template>
  <Layout class-prefix="layout" :style="{height:h+'px'}">
    <NumberPad :value.sync="record.amount" @submit="saveRecord"/>
    <Tabs :data-source="recordTypeList" :value.sync="record.type"/>
    <div class="notes">
      <FormItem field-name="备注" placeholder="在这里输入备注" @update:value="onUpdateNotes"/>
    </div>
    <Tags @update:value = "record.tags = $event"/>
  </Layout>
</template>

<script lang="ts">
  import Vue from 'vue';
  import NumberPad from '@/components/Money/NumberPad.vue';
  import FormItem from '@/components/Money/FormItem.vue';
  import Tags from '@/components/Money/Tags.vue';
  import {Component} from 'vue-property-decorator';
  import Tabs from '@/components/Tabs.vue';
  import recordTypeList from '@/constants/recordTypeList';
  @Component({
    components: {Tabs, FormItem, Tags, NumberPad}
  })
  export default class Money extends Vue {
    h = document.body.clientHeight;
    get recordList() {
      return this.$store.state.recordList;
    }
    recordTypeList = recordTypeList;
    record: RecordItem = {tags: [], notes: '', type: '-', amount: 0};
    created() {
      this.$store.commit('fetchRecords');
    }
    onUpdateNotes(value: string) {
      this.record.notes = value;
    }
    saveRecord() {
      if(!this.record.tags || this.record.tags.length === 0){
        return window.alert('请至少选择一个标签');
      }
      this.$store.commit('createRecord', this.record);
    }
  }
</script>

<style lang="scss">
  .layout-content {
    display: flex;
    flex-direction: column-reverse;
  }
  .notes {
    padding: 10px 0;
  }
</style>

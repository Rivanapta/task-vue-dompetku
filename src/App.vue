<template>
  <v-app>
    <v-container>
      <v-row justify="center" class="mt-5">
        <v-col cols="12" md="8">
          <!-- Komponen Form untuk input data -->
          <formInput @add-record="addRecord" />

          <!-- Komponen Rekap Keuangan untuk daftar transaksi -->
          <recordList :records="records" @remove-record="removeRecord" @clear-all-records="clearAllRecords" />
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import formInput from './components/FormInput.vue';
import recordList from './components/recordList.vue';

export default {
  components: {
    formInput,
    recordList,
  },
  data() {
    return {
      records: [],
    };
  },

  created() {
    this.loadFromLocalStorage();
  },

  methods: {
    addRecord(record) {
      this.records.push(record);
      this.saveToLocalStorage();
    },
    removeRecord(index) {
      this.records.splice(index, 1);
      this.saveToLocalStorage();
    },
    clearAllRecords() {
      this.records = [];
      this.saveToLocalStorage();
    },

    saveToLocalStorage() {
      localStorage.setItem('records', JSON.stringify(this.records));
    },

    loadFromLocalStorage() {
      const savedRecords = localStorage.getItem('records');
      if (savedRecords) {
        this.records = JSON.parse(savedRecords);
      }
    },
  },
};
</script>

<style>
.v-application {
  background-color: #f5f5f5;
}
</style>

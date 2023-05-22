<template>
  <main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
    <div
      class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pb-2 mb-3 border-bottom"
    >
      <h1 class="h2">Интерактивная таблица</h1>
      <div class="btn-toolbar mb-2 mb-md-0">
        <div class="btn-group mx-2">
          <button class="btn btn-sm btn-outline-secondary">Отправить</button>
          <button class="btn btn-sm btn-outline-secondary">Экспорт</button>
        </div>
      </div>
    </div>
    <h2>Данные</h2>
    <div class="table-responsive">
      <table class="table table-striped table-sm">
        <thead>
          <tr>
            <th>#</th>
            <th v-for="header in headers" :key="header">{{ header }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, rowIndex) in table" :key="rowIndex">
            <td>{{ rowIndex + 1 }}</td>
            <td v-for="(cell, cellIndex) in row" :key="cellIndex">
              <input
                type="text"
                class="form-control"
                name=""
                id=""
                aria-describedby="helpId"
                placeholder=""
                v-model="cell.value"
              />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import AlphanumericEncoder from "alphanumeric-encoder";

class Cell {
  value: string;
  calcuatedValue?: string;

  constructor(value = "") {
    this.value = value;
    //
  }
}

@Options({})
export default class HelloWorld extends Vue {
  table: Array<Array<Cell>> = [];
  headers: Array<string> = [];
  rows = 10;
  collumns = 10;
  converter = new AlphanumericEncoder();

  mounted() {
    this.createTable();
    console.log(this.table);
  }
  //
  createTable() {
    for (var i = 0; i < this.rows; i++) {
      let row = [];
      for (var j = 0; j < this.collumns; j++) {
        row.push(new Cell());
      }
      this.table.push(row);
    }
    //
    for (var k = 1; k <= this.collumns; k++) {
      let header = this.converter.encode(k);
      if (header) this.headers.push(header);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less"></style>

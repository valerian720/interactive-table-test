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
                @input="cell.changeCell()"
                @focus="cell.onFocus()"
                @blur="
                  cell.onBlur();
                  recalculateTable();
                "
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
  value: string; // that is rendered on screen
  //
  inputedValue: string; // value that user have inputed
  processedValue: string; // value that was calculated
  //
  constructor(value = "=A1") {
    this.inputedValue = value;
    //
    this.processedValue = "0";
    this.value = this.processedValue;
    //
  }
  changeCell() {
    this.inputedValue = this.value;
  }
  onFocus() {
    this.value = this.inputedValue;
  }
  onBlur() {
    if (this.inputedValue.charAt(0) === "=") {
      this.value = this.processedValue;
    } else {
      this.value = this.inputedValue;
    }
  }
  getValue(): string {
    let ret = this.inputedValue;
    if (this.inputedValue.charAt(0) === "=") {
      ret = this.processedValue;
    }
    return ret;
  }
  getInputedValue(): string {
    return this.inputedValue;
  }
  processValue(newValue: string) {
    this.processedValue = newValue;
    this.value = newValue;
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
  recalculateTable() {
    console.log("recalculating...");
    for (const row of this.table) {
      for (const curCell of row) {
        let curVal = curCell.getInputedValue();
        // check if needed to calc
        if (curVal.charAt(0) === "=") {
          curVal = curVal.substring(1);
          // process "+"
          let curValArr = curVal.split("+").map((e) => e.trim());
          console.log(curValArr);
          let res = 0;
          for (const cellReference of curValArr) {
            let coordinates = this.getCoordinates(cellReference);
            console.log("coordinates", coordinates);

            if (coordinates) {
              res += Number(
                this.table[coordinates[0]][coordinates[1]].getValue()
              );
            }
          }
          console.log(res);

          //
          curCell.processValue(`${res}`);
        }
      }
    }
    return;
  }
  getCoordinates(pos: string) {
    let arr = pos.split(/(\d+)/);
    return [Number(this.converter.decode(arr[0])) - 1, Number(arr[1]) - 1];
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less"></style>

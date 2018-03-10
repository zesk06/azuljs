<template>
  <div class="azul">
    <h1>Azul</h1>

    <div class="container">
      <div class="row">
        <div class="col-md-4">
          {{ azul.score }}
          <button type="button" class="btn btn-danger btn-sm "
                  v-on:click="reset">reset</button>
        </div>
        <div class="col-md-4">
          <!-- stairs -->
          <div v-for="(row, rowIndex) in azul.stairs" v-bind:key="rowIndex" class="row">
            <div v-for="(cell, colIndex) in row" class="col"
                 v-bind:key="colIndex" v-on:click="click_stairs(rowIndex,colIndex)">
              <button type="button" class="btn btn-info btn-sm ">{{ cell }}</button>
            </div>
          </div>

        </div>
        <div class="col-md-4">
          <!-- eslint-disable-next-line vue/require-v-for-key -->
          <div v-for="(row, rowIndex) in azul.board" v-bind:key="rowIndex" class="row">
            <div v-for="(cell, colIndex) in row" class="col"
                 v-bind:key="colIndex" v-on:click="click(rowIndex,colIndex)">
              <button type="button" v-bind:class="getTileClass(cell)">{{ cell }}</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
const TILE_LIGHT = 0;
const TILE_BLUE = 1;
const TILE_GREEN = 2;
const TILE_RED = 3;
const TILE_YELLOW = 4;
const TILE_DARK = 5;
class AzulGame {
  constructor(size) {
    // console.log('new azul', size, TILE_BLUE);
    this.score = 0;
    this.size = size;
    this.board = [];
    this.stairs = [];
    this.reset();
  }

  reset() {
    this.score = 0;
    const matrix = [];
    const stairs = [];
    for (let i = 0; i < this.size; i += 1) {
      matrix[i] = new Array(this.size);
      matrix[i].fill(0);
      stairs[i] = new Array(i + 1);
      stairs[i].fill(0);
    }
    this.board = matrix;
    this.stairs = stairs;
  }

  /**
   * @function toggle
   */
  toggle(row, col) {
    const prev = this.board[row][col];
    this.board[row].splice(col, 1, prev + 1);
    const points = this.getPoints(row, col);
    this.score = this.score + points;
  }

  getPoints(row, col) {
    let points = 1;
    // lefty
    let rowIndex = row;
    let colIndex = col - 1;
    while (colIndex >= 0 && this.board[rowIndex][colIndex] > 0) {
      // console.log('lefty > 1');
      points += 1;
      colIndex -= 1;
    }
    // righty
    colIndex = col + 1;
    while (colIndex < this.size && this.board[rowIndex][colIndex] > 0) {
      points += 1;
      colIndex += 1;
    }
    // uppy
    colIndex = col;
    rowIndex = row - 1;
    while (rowIndex >= 0 && this.board[rowIndex][colIndex] > 0) {
      points += 1;
      rowIndex -= 1;
    }
    // downy
    colIndex = col;
    rowIndex = row + 1;
    while (rowIndex < this.size && this.board[rowIndex][colIndex] > 0) {
      points += 1;
      rowIndex += 1;
    }
    return points;
  }
}

export default {
  name: 'Azul',
  data() {
    return {
      msg: 'The Azul Game',
      azul: new AzulGame(5),
    };
  },
  computed: {
    tileClass() {
      return ['btn', 'btn-info'];
    },
  },
  methods: {
    click(row, col) {
      // console.log('clicked on ', row, col);
      this.azul.toggle(row, col);
    },
    reset() {
      this.azul.reset();
    },
    getTileClass(tileValue) {
      let tileClass = 'btn btn-sm';
      switch (tileValue) {
        case TILE_LIGHT:
          break;
        case TILE_BLUE:
          tileClass += 'btn-';
          break;
        case TILE_GREEN:
          tileClass += 'btn-';
          break;
        case TILE_RED:
          tileClass += 'btn-';
          break;
        case TILE_YELLOW:
          tileClass += 'btn-';
          break;
        case TILE_DARK:
          tileClass += 'btn-';
          break;
        default:
          break;
      }
      tileClass = `${tileClass} btn-success`;
      return tileClass;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
azul {
  background: lightblue;
}
</style>

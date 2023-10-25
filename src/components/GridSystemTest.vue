<template>
  <div class="grid-generator">
    <h1 class="text-left">Grid Generator</h1>

    <div class="headertop shadow-gray-500">
      <div class="inputs_in">
        <label class="margin_rite" for="numGrids">Generate:</label>
        <input
          class="inp_txt"
          v-model.number="numGrids"
          type="number"
          id="numGrids"
          min="1"
          max="5"
        />
      </div>
      <div class="inputs_in">
        <label class="margin_rite margin_left" for="gridSize">random grids, each with </label>
        <input
          class="inp_txt"
          v-model.number="gridSize"
          type="number"
          id="gridSize"
          min="2"
          max="5"
        />
      </div>
      <label class="margin_rite" for="gridSize"> rows/columns:</label>
      <div class="inputs_in">
        <button class="grn_button" @click="generateGrids">Generate</button>
      </div>
    </div>

    <div class="grid-container">
      <div v-for="(grid, gridIndex) in grids" :key="gridIndex" class="grid">
        <div v-for="(row, rowIndex) in grid" :key="rowIndex" class="row">
          <div
            class="grid-cell"
            v-for="(letter, cellIndex) in row"
            :key="cellIndex"
          >
            {{ letter }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numGrids: 1,
      gridSize: 5,
      grids: [],
    };
  },
  methods: {
    generateGrids() {
      this.grids = [];
      for (let i = 0; i < this.numGrids; i++) {
        const grid = this.generateRandomGrid();
        this.grids.push(grid);
      }
    },
    generateRandomGrid() {
      const grid = [];
      for (let i = 0; i < this.gridSize; i++) {
        const row = this.generateRandomRow();
        grid.push(row);
      }
      return grid;
    },
    generateRandomRow() {
      const row = [];
      for (let i = 0; i < this.gridSize; i++) {
        const randomCharCode = Math.floor(Math.random() * 26) + 65; // ASCII code for capital letters
        row.push(String.fromCharCode(randomCharCode));
      }
      return row;
    },
  },
};
</script>

<style scoped>
.grid-generator {
  text-align: center;
  padding: 2rem;
}
.grid-container {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}
.grid-generator h1 {
  font-family: 'Roboto Slab', serif;
  font-size: 48px;
  font-weight: 700;
  line-height: 63px;
  letter-spacing: 0em;
  text-align: left;
}

.grid {
  display: grid;
  grid-template-columns: repeat(var(--grid-size), 1fr);
  border: 5px solid #000;
  border-radius: 4px;
  box-shadow: 4px 4px 4px 0px rgba(0, 0, 0, 0.0625);
  margin-bottom: 20px;
}
.row {
  display: flex;
  justify-content: center;
  align-items: center;
}

.margin_rite{
  margin-right: 1.2em;
}
.margin_left{
  margin-left: 1.2em;
}

.grid-cell {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 60px;
  height: 60px;
  border: 5px solid #000;
  font-size: 36px;
  font-weight: bold;
  font-family: 'Roboto Slab', serif;
  background: #fff;
  text-transform: uppercase;
  font-weight: 900;
}
.grn_button {
  background: #0d6efd;
  font-family: 'Roboto Slab', serif;
  font-size: 24px;
  min-width: 94px;
  padding: 7px 13px;
  border-radius: 4px;
  color: #fff;
  line-height: 24px;
  border: 0px;
  box-shadow: 4px 4px 4px 0px rgba(0, 0, 0, 0.0625);
}
.inp_txt {
  width: 56px;
  padding: 7px 13px;
  border-radius: 4px;
  border: 1px solid #ced4da;
  font-size: 16px;
  line-height: 24px;
}
.inputs_in {
  display: inline;
}
.headertop {
  height: auto;
  min-width: 600px;
  background: #ffffff;
  border-radius: 4px;
  padding: 1.25em;
}
@media screen and (max-width: 800px) {
  .headertop {
    min-width: 100%;
    padding: 0em;
  }
}
@media screen and (max-width: 400px) {
  .grn_button {
    min-width: 200px;
    margin: 20px 0px;
  }
  .inp_txt{
    margin: 5px 0px;

}
}
</style>

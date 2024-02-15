<template>
  <v-app>
    <v-main>
      <v-app-bar>
        <img src="./assets/solver-icon.png" width="80" height="80" />
        <span class="text-h6">
          Sudoku Solver
        </span>
        <v-btn color="primary" class="mx-8" @click="showIns">Instructions</v-btn>
      </v-app-bar>
      <v-navigation-drawer>
        <span>
          
        </span>
        <v-divider/>
        <span>
          
        </span>
      </v-navigation-drawer>
      <UnsolvableDialog ref="unsDialog" />
      <Instructions ref="instructions"/>
      <SudokuGrid ref="sudokuGrid" @unsolvable="unsolv" />
      <v-btn class="d-block mx-auto my-10" color="primary" @click="solve" :disabled="solveDisabled">
        Solve
      </v-btn>
      <v-btn class="d-block mx-auto my-10" variant="tonal" color="error" @click="reset">
        Reset
      </v-btn>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      solveDisabled: false,
      solveLook: "primary"
    };
  },
  methods: {
    solve() {
      this.solveDisabled = true;
      this.$refs.sudokuGrid.collectPuzzleData();
    },
    reset() {
      this.$refs.sudokuGrid.resetPuzzle();
      this.solveDisabled = false;
    },
    unsolv() {
      console.log('Unsolvable puzzle!');
      this.$refs.unsDialog.activate();
    },
    showIns() {
      this.$refs.instructions.show();
    }
  },
}
</script>

<script setup>
import SudokuGrid from './components/SudokuGrid.vue';
import Instructions from './components/Instructions.vue';
import UnsolvableDialog from './components/UnsolvableDialog.vue';
</script>


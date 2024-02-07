<template>
  <v-app>
    <v-main>
      <v-app-bar>
        <img src="./assets/solver-icon.png" width="80" height="80" />
        <span class="text-h6">
          Sudoku Solver
        </span>
      </v-app-bar>
      <v-navigation-drawer>
        <span>
          Lorem ipsum dolor sit, amet consectetur adipisicing elit. Repellat blanditiis, velit laboriosam consequuntur,
          minus odit voluptatem consequatur fugiat totam tempore neque veniam fugit qui officia vero, iste dolore est
          delectus.
        </span>
        <v-divider></v-divider>
      </v-navigation-drawer>
      <SudokuGrid ref="sudokuGrid" />
      <v-btn class="d-block mx-auto my-10" variant="tonal" @click="solve">
        Solve
      </v-btn>
      <v-btn class="d-block mx-auto my-10" variant="tonal">
        Reset
      </v-btn>
    </v-main>
  </v-app>
</template>

<script>
export default {
  methods: {
    solve() {
      this.$refs.sudokuGrid.collectPuzzleData();
    },
  },
}
</script>

<script setup>
//
</script>

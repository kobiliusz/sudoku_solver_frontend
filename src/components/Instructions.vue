<template>
    <v-card class="text-center mx-3 my-3" v-show="showIns">
        <div class="mx-5 my-3">
            <h2>Sudoku Solver Instructions</h2>
            <h3>Overview</h3>

            <p>This Sudoku Solver is designed to help you quickly solve Sudoku puzzles. Simply input the numbers from your
                puzzle into the grid, click "Solve" to see the solution, or "Reset" to clear the board and start over.</p>
            <h3>Step-by-Step Instructions</h3>
            <ul class="text-left">
                <li><b>Entering the Puzzle:</b>
                    Find the Sudoku puzzle you wish to solve.
                    Click on a cell in the below grid to select it. Type in a number from your Sudoku puzzle corresponding
                    to that cell. Repeat this process for all cells that have numbers in your puzzle. The cells will accept
                    numbers 1 through 9.</li>

                <li><b>Solving the Puzzle:</b>
                    Once you have filled in all known numbers from your puzzle, click the "Solve" button.
                    Sudoku Solver will process the inputs. If a valid solution exists based on the inputs provided, the
                    empty cells will be automatically filled with the correct numbers, completing the puzzle.</li>

                <li><b>Using the Reset Button:</b>
                    If you wish to clear the entire board to start a new puzzle or correct a mistake, click the "Reset"
                    button.
                    Clicking "Reset" will clear all numbers from the grid, allowing you to start fresh.</li>

            </ul>

            <h3>Tips</h3>

            <ul class="text-left">
                <li>
                    <b>Accuracy:</b> Ensure that the numbers you input from your original Sudoku puzzle are accurate.
                    Incorrect inputs can lead to unsolvable puzzles or incorrect solutions.
                </li>
                <li>
                    <b>One Solution:</b> The Sudoku Solver aims to find a valid solution. Some puzzles may have more than
                    one solution, but the solver will provide one possible completion.
                </li>
            </ul>
            <h3>Troubleshooting</h3>

            <ul class="text-left">
                <li>
                    <b>Unsolvable Puzzle:</b> If the solver cannot find a solution, ensure all inputted numbers are correct.
                    Some puzzles might be incorrectly set up or too complex for automated solvers.
                </li>
            </ul>
            <p class="motto">Enjoy solving your Sudoku puzzles with ease!</p>

        </div>
        <v-btn class="my-3" color="success" @click="hideIns">
            Hide
        </v-btn>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            showIns: true
        };
    },
    methods: {
        hideIns() {
            this.showIns = false;
        },
        show() {
            this.showIns = true;
        }
    }

}

</script>

<style>
h1 {
    margin-top: 10px;
}

h3 {
    margin-top: 20px;
}

li {
    margin-left: 30px;
}

.motto {
    font-style: italic;
    margin-top: 20px;
}

</style>


<template>
        <v-container>
            <v-card class="board">
            <v-row v-for="regionRow in 3" :key="'regionRow-' + regionRow" class="region-row">
                <v-col cols="4" v-for="regionCol in 3" :key="'regionCol-' + regionCol" class="region-col">
                    <v-sheet outlined class="pa-3 region">
                        <v-row v-for="row in 3" :key="'row-' + row">
                            <v-col cols="4" v-for="col in 3" :key="'col-' + col" class="cell">
                                <input class="no-input" inputmode="numeric" :id="generateId(regionRow, regionCol, row, col)"
                                    maxlength="1" @input="validateCharacter" />
                            </v-col>
                        </v-row>
                    </v-sheet>
                </v-col>
            </v-row>
            <v-overlay v-model="isLoading" class="align-center justify-center" contained>
            <v-progress-circular color="primary" indeterminate size="64"></v-progress-circular>
        </v-overlay>
        </v-card>
        </v-container>
        
</template>
  
<script>
export default {
    name: 'SudokuGrid',
    data() {
        return {
            isLoading: false
        };
    },
    methods: {
        validateCharacter(e) {
            const value = e.target.value;
            const validPattern = /^[1-9]?$/;
            if (!validPattern.test(value)) {
                e.target.value = '';
            }
        },
        generateId(regionRow, regionCol, row, col) {
            const actualRow = (regionRow - 1) * 3 + row - 1;
            const actualCol = (regionCol - 1) * 3 + col - 1;
            return `input-${actualRow}-${actualCol}`;
        },
        collectPuzzleData() {
            let req_data = {};
            let puzzle = [];

            for (let row = 0; row < 9; row++) {
                let row_data = [];

                for (let col = 0; col < 9; col++) {
                    const inputId = `input-${row}-${col}`;
                    const inputElement = document.getElementById(inputId);
                    const value = parseInt(inputElement.value, 10);
                    if (!isNaN(value)) {
                        inputElement.classList.add("puzzle-no");
                    }
                    inputElement.readOnly = true;
                    row_data.push(!isNaN(value) ? value : 0);
                }
                puzzle.push(row_data);
            }

            req_data['puzzle'] = puzzle;

            var env = process.env.NODE_ENV || 'development';

            var url;

            if (env == 'development') {
                url = "http://127.0.0.1:8000/solve/"
            } else {
                url = "/solve/"
            }

            this.isLoading = true;

            // Use fetch to send a POST request
            fetch(url, {
                method: 'POST', // Specify the request method
                headers: {
                    'Content-Type': 'application/json', // Indicate that you're sending JSON data
                },
                body: JSON.stringify(req_data), // Convert the JavaScript object to a JSON string
            })
                .then(response => {
                    if (response.status == 406) {
                        this.$emit('unsolvable');
                        return null;
                    } if (!response.ok) {
                        // If the response is not 2xx, throw an error
                        throw new Error('Network response was not ok');
                    }
                    return response.json(); // Parse the JSON response body
                })
                .then(data => {
                    if (data == null) {
                        return;
                    }
                    console.log(data); // Handle the response data
                    for (let row = 0; row < 9; row++) {
                        for (let col = 0; col < 9; col++) {
                            const inputId = `input-${row}-${col}`;
                            const inputElement = document.getElementById(inputId);
                            inputElement.value = data['solution'][row][col];
                        }
                    }
                })
                .catch(error => {
                    console.error('There was a problem with your fetch operation:', error);
                })
                .finally(a => {
                    this.isLoading = false;
                });

            
        },
        resetPuzzle() {
            for (let row = 0; row < 9; row++) {
                for (let col = 0; col < 9; col++) {
                    const inputId = `input-${row}-${col}`;
                    const inputElement = document.getElementById(inputId);
                    inputElement.value = "";
                    inputElement.classList.remove("puzzle-no");
                    inputElement.readOnly = false;
                }
            }
        },
    }
}
</script>
  
<style>
.region-row {
    margin: 0px;
    padding: 0px;
}

.region-col {
    margin: 0px;
    padding: 0px;
}

.region-row:last-child .region-col {
    border-bottom: none;
}

.v-sheet.region {
    border: 3px solid black;
    margin: 0px;
}

.no-input {
    border: 0px solid black;
    width: 20px;
    height: 20px;
    text-align: center;
}

.puzzle-no {
    font-weight: bold;
}

.cell {
    border: 1px solid black;
}

.v-container {
    margin-top: 30px;
    max-width: 480px !important;
    line-height: 20px;
}

.board {
    box-shadow: none !important;
}

</style>
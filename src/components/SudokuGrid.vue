<template>
    <v-container fluid>
        <!-- Loop for each 3x3 region row -->
        <v-row v-for="regionRow in 3" :key="'regionRow-' + regionRow" class="region-row">
            <!-- Loop for each 3x3 region column -->
            <v-col cols="4" v-for="regionCol in 3" :key="'regionCol-' + regionCol" class="region-col">
                <v-sheet outlined tile class="pa-3 region">
                    <!-- Inner 3x3 grid for text fields -->
                    <v-row v-for="row in 3" :key="'row-' + row">
                        <v-col cols="4" v-for="col in 3" :key="'col-' + col">
                            <v-text-field outlined dense single-line
                                :hint="`R${(regionRow - 1) * 3 + row}, C${(regionCol - 1) * 3 + col}`" :rules="[validateCharacter]"
                                class="text-field"></v-text-field>
                        </v-col>
                    </v-row>
                </v-sheet>
            </v-col>
        </v-row>
    </v-container>
</template>
  
<script>
export default {
    name: 'SudokuGrid',
    methods: {
        validateCharacter(value) {
            const pattern = /^[1-9]?$/;
            return pattern.test(value) || 'Input must be an integer between 1 and 9 or empty.';
        },
    },
}
</script>
  
<style>
.region-row {
    margin-bottom: 8px;
    /* Adjust spacing between region rows for visual clarity */
}

.region-col {
    padding: 0 4px;
    /* Adjust spacing between region columns for visual clarity */
    border-right: 2px solid black;
    /* Vertical lines */
}

.region-col:last-child {
    border-right: none;
}

.region-row:last-child .region-col {
    border-bottom: none;
    /* Avoid double border at the bottom of the last row */
}

.v-sheet.region {
    border: 2px solid black;
    /* Border around each region for clear division */
    margin: 4px;
    /* Space between regions */
}

.text-field {
    margin-top: -8px;
    /* Adjust if necessary to decrease the size of the text field */
    margin-bottom: -8px;
    /* Adjust if necessary for tighter packing */
    border: 1px solid black;
}

.v-text-field--outlined .v-input__control {
    min-height: 40px;
    /* Adjust for smaller height */
}

.v-text-field .v-label {
    font-size: 0.875rem;
    /* Smaller label font size */
}

.v-text-field .v-text-field__slot {
    font-size: 0.875rem;
    /* Smaller input text */
}

/* Additional adjustments for spacing and alignment */
.v-container.fluid {
    padding-left: 0;
    padding-right: 0;
}</style>
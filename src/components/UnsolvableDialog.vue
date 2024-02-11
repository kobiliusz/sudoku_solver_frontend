
<template>
    <v-dialog width="500" v-model="isActive" persistent>
        <v-card title="Unsolvable!">
            <v-card-text>
                The puzzle cannot be solved.
            </v-card-text>

            <v-card-actions>
                <v-spacer></v-spacer>

                <v-btn text="Close" @click="isActive = false"></v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>

</template>

<script>
export default {
    data() {
        return {
            isActive: false 
        };
    },
    methods: {
        activate() {
            this.isActive = true;
        }
    }
}
</script>


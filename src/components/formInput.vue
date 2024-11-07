<template>
    <v-card>
        <v-card-title class="text-h5">Dompetku - Expense & Income Money Management</v-card-title>
        <v-card-text>
            <v-form ref="form" v-model="valid" lazy-validation>
                <v-text-field v-model="description" label="Keterangan" required></v-text-field>

                <!-- Dropdown untuk memilih jenis transaksi -->
                <v-select v-model="dropdown" :items="items" label="Pilih Jenis Transaksi" outlined required></v-select>

                <v-text-field v-model="amount" label="Jumlah Uang" type="number" required></v-text-field>

                <v-btn color="primary" @click="handleSubmit">Submit</v-btn>
            </v-form>
        </v-card-text>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            description: '',
            dropdown: null,
            items: ['Transaksi Masuk', 'Transaksi Keluar'],
            amount: null,
            valid: true,
        };
    },
    methods: {
        handleSubmit() {
            if (this.description && this.amount && this.dropdown) {
                this.$emit('add-record', {
                    description: this.description,
                    amount: parseInt(this.amount),
                    type: this.dropdown,
                });
                // Reset form setelah submit
                this.description = '';
                this.amount = null;
                this.dropdown = null;
            }
        },
    },
};
</script>

<style scoped>
.v-btn {
    margin-top: 10px;
}
</style>
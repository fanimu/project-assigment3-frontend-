<template>
    <div class="row">
        <div class="col">
            <h1>Keranjang Belanja</h1>
            <table class="table table-bordered table-striped">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Quantity</th>
                        <th>Price</th>
                        <th></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(k, index) in keranjangbelanja" :key="index">
                        <td>{{ k.name }}</td>
                        <td>{{ k.quantity }}</td>
                        <td>
                            {{
                                k.price
                                    .toLocaleString("id-ID", {
                                        style: "currency",
                                        currency: "IDR",
                                    })
                                    .replace(",00", "")
                            }}
                        </td>
                        <td class="text-center">
                            <button
                                @click="deleteProdukKeranjang(index)"
                                class="btn btn-danger"
                            >
                                Delete
                            </button>
                        </td>
                    </tr>
                </tbody>
                <tfoot class="fw-bold">
                    <tr>
                        <td colspan="2">Total</td>
                        <td>
                            {{
                                keranjangbelanja
                                    .reduce((total, k) => {
                                        return total + k.price;
                                    }, 0)
                                    .toLocaleString("id-ID", {
                                        style: "currency",
                                        currency: "IDR",
                                    })
                                    .replace(",00", "")
                            }}
                        </td>
                        <td colspan="2"></td>
                    </tr>
                </tfoot>
            </table>
            <button @click="checkout" class="btn btn-success">Checkout</button>
        </div>
    </div>
</template>

<script>
export default {
    emits: ["emit-deleteProdukKeranjang"],
    props: ["keranjangbelanja"],
    data() {
        return {
            totalHarga: 0,
        };
    },
    methods: {
        deleteProdukKeranjang(index) {
            this.$emit("emit-deleteProdukKeranjang", index);
        },
        checkout() {
            this.totalHarga = this.keranjangbelanja.reduce((total, k) => {
                return total + k.price;
            }, 0);

            if (this.keranjangbelanja.length > 0) {
                alert(
                    "Total pembelian: " +
                        this.totalHarga
                            .toLocaleString("id-ID", {
                                style: "currency",
                                currency: "IDR",
                            })
                            .replace(",00", "")
                );
            } else {
                alert("Keranjang belanja kosong.");
            }
        },
    },
};
</script>

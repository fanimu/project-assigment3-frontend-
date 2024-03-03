<template>
    <div class="row">
        <div class="col">
            <h1>Semua Produk</h1>
            <table class="table table-bordered table-striped">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Description</th>
                        <th>Stock</th>
                        <th>Price</th>
                        <th></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(p, index) in daftarproduk" :key="index">
                        <td>{{ p.name }}</td>
                        <td>{{ p.description }}</td>
                        <td>{{ p.stock }}</td>
                        <td>
                            {{
                                p.price
                                    .toLocaleString("id-ID", {
                                        style: "currency",
                                        currency: "IDR",
                                    })
                                    .replace(",00", "")
                            }}
                        </td>
                        <td class="text-center">
                            <button
                                @click="addToChart(index)"
                                class="btn btn-primary"
                                v-if="p.stock > 0"
                            >
                                Add To Chart
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    emits: ["emit-addtocart"],
    props: ["daftarproduk"],
    data() {
        return {};
    },
    methods: {
        addToChart(index) {
            this.$emit("emit-addtocart", index);
        },
    },
    mounted() {},
};
</script>

<template>
    <div class="container shadow-lg p-3 mt-5">
        <daftar-produk :daftarproduk="produk" @emit-addtocart="addToChart" />
        <keranjang-belanja
            :keranjangbelanja="produkKeranjang"
            @emit-deleteProdukKeranjang="deleteProdukKeranjang"
        />
    </div>
</template>

<script>
export default {
    data() {
        return {
            produk: [
                {
                    name: "Indomie Goreng Rendang",
                    description: "Masakan instan terenak didunia",
                    stock: 10,
                    price: 3900,
                },
                {
                    name: "Mie Gelas Rendang",
                    description: "Mie instan khusus anak kosan",
                    stock: 3,
                    price: 1500,
                },
                {
                    name: "Bakmi mewah",
                    description: "Kalau anak kosan jangan macam2 deh",
                    stock: 80,
                    price: 10000,
                },
            ],
            produkKeranjang: [],
        };
    },
    methods: {
        addToChart(index) {
            if (this.produk[index].stock > 0) {
                this.produk[index].stock--;

                let existingIndex = this.produkKeranjang.findIndex(
                    (item) => item.index == index
                );

                if (existingIndex !== -1) {
                    this.produkKeranjang[existingIndex].quantity++;
                    this.produkKeranjang[existingIndex].price +=
                        this.produk[index].price;
                } else {
                    this.produkKeranjang.push({
                        ...this.produk[index],
                        quantity: 1,
                        index: index,
                    });
                }
            }
        },
        deleteProdukKeranjang(index) {
            const deletedProduct = this.produkKeranjang[index];
            const originalProductIndex = this.produk.findIndex(
                (product) => product.name === deletedProduct.name
            );

            if (originalProductIndex !== -1) {
                this.produk[originalProductIndex].stock +=
                    deletedProduct.quantity;
            }
            this.produkKeranjang.splice(index, 1);
        },
    },
    mounted() {},
};
</script>

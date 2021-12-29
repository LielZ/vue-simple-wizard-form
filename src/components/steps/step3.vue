<template>
    <p>
        היי {{this.name}}, יש לך כסף ב:
    </p>
    <ul v-if="this.nineteenNine === 0">
        <li v-for="(item, id) in this.values" :key="id">
            {{item.title}}
        </li>
    </ul>
    <ul v-else>
        <li>
            אין לי
        </li>
    </ul>
    <h1> אין פה כלום 🤷</h1>
</template>

<script>
    export default {
        name: "step3",
        data() {
            return {
                nineteenNine: 0
            }
        },
        props: {
            name: {
                type: String
            },
            values: {
                type: Array
            }
        },
        methods: {
            thereIsNineteenNine() {
                for (var i = this.values.length - 1; i >= 0; --i) {
                    if (this.values[i].id == 99) {
                        this.nineteenNine = 1;
                    }
                }
            }
        },
        beforeMount() {
            this.thereIsNineteenNine()
        }
    }
</script>

<style scoped>
    li {
        list-style: none;
        text-align: right;
        font-weight: bold;
    }
    p {
        text-align: right;
        font-size: 1.4rem;
    }
</style>

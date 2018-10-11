<template>
    <div> <!-- manter esta div -->
        <!-- Aqui vai o código HTML da página utilizando a sintaxe de template Vue -->
    </div>
</template>

<script>
    export default {

        // Propriedades
        data() {
            return {
                // ...
            }
        },

        // Métodos
        methods: {
            // ...
        },

        // Watchers
        watch: {
            // ...
        },

        // Filtros
        filters: {
            // ...
        },

        // O hook [mounted] rodará o código fornecido assim que a página for renderizada
        mounted() {
            this.form = this.$refs.form;
        }

    }
</script>
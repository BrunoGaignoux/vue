<template>
    <div class="row wrapper border-bottom white-bg page-heading">
        <div class="col-sm-6">
            <h3>{{ title }}</h3>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            title: window.Laravel.title
        }
    }
}
</script>

<style scoped>
    .page-heading {
        padding: 15px 25px;
    }
    h3 {
        margin: 0;
        font-weight: normal;
    }
</style>
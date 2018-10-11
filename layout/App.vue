<template>
    <div>
        <alvo-sidebar></alvo-sidebar>
        <div id="page-wrapper" class="gray-bg">

            <alvo-topbar></alvo-topbar>

            <alvo-page-header></alvo-page-header>

            <div class="wrapper wrapper-content">
                <div id="loading">
                    <div class="sk-spinner sk-spinner-wave">
                        <div class="sk-rect1"></div>
                        <div class="sk-rect2"></div>
                        <div class="sk-rect3"></div>
                        <div class="sk-rect4"></div>
                        <div class="sk-rect5"></div>
                    </div>
                </div>
                <slot></slot>
                <div class="clearfix"></div>
            </div>

            <alvo-footer :fixed="true" :version="dockerImgTag"></alvo-footer>

            <vc-alert></vc-alert>
            <div class="clearfix"></div>
        </div>
    </div>

</template>

<script>

    import VcAlert from '../componentes/VcAlert.vue';

    export default {
        data() {
            return {
                dockerImgTag: window.Laravel.dockerImgTag
            }
        },

        mounted() {
            Event.$on('VcLoader', data => {
                if (data) {
                    $('#loading').addClass('sk-loading');
                } else {
                    $('#loading').removeClass('sk-loading');
                }
            });
        },

        components: {
            VcAlert
        }
    }
</script>

<style scoped>
    .wrapper-content {
        position: relative;
    }
    #loading {
        display: none;
        position: absolute;
        height: 100%;
        width: 100%;
        background-color: rgba(255,255,255,0.80);
        z-index: 999999;
    }
    #loading.sk-loading {
        display: block;
    }
    .sk-spinner {
        position: fixed !important;
        top: 45vh !important;
        width: 100% !important;
    }
</style>

<template>
    <div class="row border-bottom app-top">
        <nav class="navbar navbar-top" role="navigation">
            <div class="navbar-header">
                <a class="navbar-minimalize minimalize-styl-2 btn btn-primary" href="#"><i class="fa fa-bars"></i> </a>
                <div class="logo">
                    <a href="/">
                        <img :src="window.Laravel.cssTemplate ? `/img/Logo_${window.Laravel.cssTemplate}.png` : `/img/Logo.png`" alt=""/>
                    </a>
                </div>
            </div>

            <ul class="nav navbar-top-links navbar-right">
                <a v-if="window.Laravel.session.orig_user" href="/suporte/encerra_atendimento" class="dropdown-toggle">Encerrar Suporte</a>
                <li v-else-if="window.Laravel.session.suporte">
                    <form ref="userSupportForm" action="/suporte/inicio_atendimento" method="POST">
                        <select ref="userSupportSelect" required="required" id="usuario_suporte"
                                name="usuario_suporte" class="form-control usuario_suporte">
                        </select>
                    </form>
                </li>

                <li class="dropdown">
                    <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                        <span v-if="window.Laravel.user.empresa">{{ window.Laravel.user.empresa.nome }}</span>
                        <span v-else>Selecione a Empresa</span>
                        <b class="caret"></b>
                    </a>
                    <ul class="dropdown-menu animated fadeInDown m-t-xs">
                        <li class="dropdown-header">Selecione a Empresa</li>

                        <li v-for="empresa in window.Laravel.empresas"><a :href="window.Laravel.routeEmpresas + empresa.id">{{ empresa.nome }}</a></li>
                    </ul>
                </li>
                <li>
                    <a data-toggle="dropdown" class="dropdown-toggle" href="#">

                        <strong class="font-bold">{{ window.Laravel.user.name }} <b class="caret"></b></strong>
                    </a>
                    <ul class="dropdown-menu animated fadeInDown m-t-xs">
                        <li><a :href="window.Laravel.routeProfile">Perfil</a></li>

                        <li><a href="#" class="solicitar_acesso">Solicitar Acesso</a></li>
                        <li class="divider"></li>
                        <li>
                            <a href="/logout" @click.prevent="submitLogout()">
                                <i class="fa fa-sign-out"></i> Sair
                            </a>

                            <form ref="logoutForm" id="logout-form" action="/logout" method="POST">
                                <input type="hidden" name="_token" :value="window.Laravel.csrfToken">
                            </form>
                        </li>

                    </ul>
                </li>

                <li class="dropdown">
                    <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                        <span v-html="window.Laravel.languages[window.Laravel.locale]"></span>
                        <b class="caret"></b>
                    </a>
                    <ul class="dropdown-menu animated fadeInDown m-t-xs">
                        <li v-for="(lang, prop) in window.Laravel.languages" v-if="prop !== window.Laravel.locale">
                            <a :href="window.Laravel.routeSwitchLang + prop">
                                <span v-html="lang"></span>
                            </a>
                        </li>
                    </ul>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>
export default {
    computed: {
        window() {
            return window;
        }
    },
    mounted() {
        $(this.$refs.userSupportSelect).change(() => {
            this.$refs.userSupportForm.submit();
        });
    },
    methods: {
        submitLogout() {
            this.$refs.logoutForm.submit();
        }
    }
}
</script>

<style scoped>
    .navbar-top {
        margin-bottom: 0 !important;
    }
</style>
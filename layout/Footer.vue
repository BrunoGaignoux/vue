<template>
    <div>
        <div class="footer" :class="{ fixed: this.fixed }">
            <div class="pull-right">
                <a href="javascript:;" data-toggle="modal" data-target="#politica_privacidade">Politica de Privacidade</a>|
                <a href="javascript:;" data-toggle="modal" data-target="#termo_uso">Termos de Uso</a>&nbsp;&nbsp;
                <strong>Versão:</strong> {{ version }} <span id="easter" @click="clickEaster()" :style="{ color: easter.color }">(enduro)</span>

            </div>
            <div>
                <strong>Copyright</strong> Alvo &copy; 2016
            </div>

        </div>

        <alvo-privacy></alvo-privacy>
        <alvo-terms></alvo-terms>
        <alvo-enduro></alvo-enduro>
    </div>
</template>

<script>
import privacy from './Privacy.vue';
import terms from './Terms.vue';
import AlvoEnduro from '../easter/Enduro.vue';

export default {

    data() {
        return {
            easter: {
                clicks: 0,
                color: 'black'
            }
        }
    },
    
    props: {
        fixed: Boolean,
        version: String
    },

    components: {
        'alvo-privacy': privacy,
        'alvo-terms': terms,
        AlvoEnduro
    },

    computed: {
        window() {
            return window;
        }
    },

    methods: {

        clickEaster(clicks) {

            this.easter.clicks++;

            if (this.easter.clicks == 1) this.easter.color = 'pink';
            else if (this.easter.clicks == 2) this.easter.color = 'blue';
            else if (this.easter.clicks == 3) this.easter.color = 'red';
            else if (this.easter.clicks == 4) this.easter.color = 'orange';
            else if (this.easter.clicks == 5) this.easter.color = 'yellow';
            else if (this.easter.clicks == 6) this.easter.color = 'purple';

            if (this.easter.clicks == 7) {
                this.easter.clicks = 0;
                this.easter.color = 'black';

                Event.$emit('showEaster');
            }
        }
    },
}
</script>

<style scoped>
#easter:hover {
    font-weight: bold
}
</style>

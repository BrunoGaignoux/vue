<template>
    <div>
        <vc-box :title="$t('Filtros da Listagem')">
            <vc-form>
                <vc-row>
                    <vc-form-box :width="4">
                        <vc-row>
                            <vc-input
                                    :label="$t('Mês/Ano')"
                                    type="date"
                                    date-type="month"
                                    v-model="filtros.ano_mes">
                            </vc-input>
                        </vc-row>
                        <vc-row>
                            <vc-input-range :label="$t('Sequência')">
                                <template slot="first">
                                    <vc-input type="select" :group="false" :data="[1,2,3,4]" :width="0"
                                              v-model="filtros.seq_de"></vc-input>
                                </template>
                                <template slot="second">
                                    <vc-input type="select" :group="false" :data="[1,2,3,4]" :width="0"
                                              v-model="filtros.seq_a"></vc-input>
                                </template>
                            </vc-input-range>
                        </vc-row>
                        <vc-row>
                            <vc-input :label="$t('Tipo')" type="select" :data="['S', 'D', 'Q', 'M']" :width="4" v-model="filtros.tipo"></vc-input>
                            <vc-input :label="$t('Marca')" :width="8" v-model="filtros.marca"></vc-input>
                        </vc-row>
                    </vc-form-box>
                    <vc-form-box :width="4">
                        <vc-input :label="$t('Todos')" name="opt1" type="radio" :width="6" val="td" v-model="filtros.opt1"></vc-input>
                        <vc-input :label="$t('Aprovado')" name="opt1" type="radio" :width="6" val="apr" v-model="filtros.opt1"></vc-input>
                        <vc-input :label="$t('Não Lançado')" name="opt1" type="radio" :width="6" val="nlan" v-model="filtros.opt1"></vc-input>
                        <vc-input :label="$t('Financeiro')" name="opt1" type="radio" :width="6" val="fin" v-model="filtros.opt1"></vc-input>
                        <vc-input :label="$t('Lançado')" name="opt1" type="radio" :width="6" val="lan" v-model="filtros.opt1"></vc-input>
                        <vc-input :label="$t('N/A Fatura')" name="opt1" type="radio" :width="6" val="na" v-model="filtros.opt1"></vc-input>
                    </vc-form-box>
                    <vc-form-box :width="4">
                        <vc-input :label="$t('Todos')" name="opt2" type="radio" :width="6" val="td" v-model="filtros.opt2"></vc-input>
                        <vc-input :label="$t('Armazenagem')" name="opt2" type="radio" :width="6" val="arm" v-model="filtros.opt2"></vc-input>
                        <vc-input :label="$t('ND')" name="opt2" type="radio" :width="6" val="nd" v-model="filtros.opt2"></vc-input>
                        <vc-input :label="$t('Recibo')" name="opt2" type="radio" :width="6" val="rec" v-model="filtros.opt2"></vc-input>
                    </vc-form-box>
                    <vc-button template="limpar-tela" :width="2" :aligned="false" @click.native="limparTela()"></vc-button>
                    <vc-button template="filtrar" :width="2" :aligned="false" @click.native="filtrar()"></vc-button>
                </vc-row>
            </vc-form>
        </vc-box>

        <vc-box :title="$t('Listagem de Mapas de Faturamento')">
            <vc-table :items="listagemMapas" select="single" :cols="colsTableMapa" :row-callback="rowCallback"></vc-table>
        </vc-box>

        <vc-box :title="$t('Outras Informações')">
            <vc-row>
                <vc-input :label="$t('C.Custo Cliente')" :disabled="true" :width="3"></vc-input>
                <vc-input :label="$t('Emp. Fiscal')" :disabled="true" :width="3"></vc-input>
                <vc-input :label="$t('C.Custo Filial')" :disabled="true" :width="3"></vc-input>
                <vc-input :label="$t('Mínimo')" type="currency" :disabled="true" :width="3"></vc-input>
            </vc-row>
            <vc-row>
                <vc-input :label="$t('ISS')" type="percent" :disabled="true" :width="2"></vc-input>
                <vc-input :label="$t('Valor ISS')" type="currency" :disabled="true" :width="2"></vc-input>
                <vc-input :label="$t('Valor Total')" type="currency" :disabled="true" :width="2"></vc-input>
                <vc-input :label="$t('Já Faturado')" type="currency" :disabled="true" :width="2"></vc-input>
                <vc-input :label="$t('Desconto')" type="currency" :disabled="true" :width="2"></vc-input>
                <vc-input :label="$t('À Faturar')" type="currency" :disabled="true" :width="2"></vc-input>
            </vc-row>
        </vc-box>

        <vc-box :title="$t('Itens do Mapa de Faturamento')">
            <vc-table select="multi" :items="listagemItens" :cols="colsTableItens"></vc-table>
        </vc-box>
    </div>
</template>

<script>

    import VcBox from '../../../../../vue/componentes/VcBox.vue'
    import VcButton from '../../../../../vue/componentes/VcButton.vue'
    import VcRow from '../../../../../vue/componentes/VcRow.vue'
    import VcCol from '../../../../../vue/componentes/VcCol.vue'
    import VcForm from '../../../../../vue/componentes/VcForm.vue'
    import VcFormBox from '../../../../../vue/componentes/VcFormBox.vue'
    import VcInputRange from '../../../../../vue/componentes/VcInputRange.vue'
    import VcInput from '../../../../../vue/componentes/VcInput.vue'
    import VcModal from '../../../../../vue/componentes/VcModal.vue'
    import VcTable from '../../../../../vue/componentes/VcTable.vue'
    
    export default {

        data() {
            return {
                filtros: {},
                listagemMapas: null,
                infosMapa: null,
                listagemItens: null,

                url: {
                    tabelaMapa: window.Laravel.baseUri + 'movimento/erp-mov-mapa-faturamento/lista-controle-financeiro'
                },

                colsTableMapa: [
                    {title: 'Faturar', data: 'nro_controle'},
                    {title: 'Número', data: 'nro_controle'},
                    {title: 'Descrição', data: 'descricao'},
                    {title: 'Cliente', data: 'cliente'},
                    {title: 'PAI', data: 'pai'},
                    {title: 'C.Custo', data: 'ccusto'},
                    {title: 'Tipo', data: 'tipo_fatur'},
                    {title: 'Seq', data: 'sequencia'},
                    {
                        title: 'F. Mínimo', data: 'minimo',
                        render(data) {
                            if (data === '1' || data === 1) {
                                return '<div class="text-center"><i class="fa fa-check-circle" ' +
                                    'style="color: #3bd00a;"></i></div>';
                            } else {
                                return '';
                            }
                        }
                    },
                    {
                        title: 'N. Lançado', data: 'nlancado',
                        render(data) {
                            if (data === '1' || data === 1) {
                                return '<div class="text-center"><i class="fa fa-check-circle" ' +
                                    'style="color: #3bd00a;"></i></div>';
                            } else {
                                return '';
                            }
                        }
                    },
                    {
                        title: 'Lançado', data: 'lancado',
                        render(data) {
                            if (data === '1' || data === 1) {
                                return '<div class="text-center"><i class="fa fa-check-circle" ' +
                                    'style="color: #3bd00a;"></i></div>';
                            } else {
                                return '';
                            }
                        }
                    },
                    {
                        title: 'Aprov. PAI', data: 'aprovado',
                        render(data) {
                            if (data === '1' || data === 1) {
                                return '<div class="text-center"><i class="fa fa-check-circle" ' +
                                    'style="color: #3bd00a;"></i></div>';
                            } else {
                                return '';
                            }
                        }
                    },
                    {
                        title: 'Financeiro', data: 'financeiro',
                        render(data) {
                            if (data === '1' || data === 1) {
                                return '<div class="text-center"><i class="fa fa-check-circle" ' +
                                    'style="color: #3bd00a;"></i></div>';
                            } else {
                                return '';
                            }
                        }
                    },
                    {title: 'Movto', data: 'nro_controle'},
                    {title: 'Documento', data: 'nro_controle'},
                    {title: 'Vencto', data: 'nro_controle'},
                ],

                colsTableItens: [
                    {title: 'Item', data: null},
                    {title: 'Descrição', data: null},
                    {title: 'Tipo Fat.', data: null},
                    {title: 'Cálculo', data: null},
                    {title: 'Valor', data: null},
                    {title: 'Quantidade', data: null},
                    {title: 'Valor Total', data: null},
                    {title: 'Cliente Serv.', data: null},
                    {title: 'Serviço', data: null},
                    {title: 'Descr.', data: null},
                ]
            }
        },

        computed: {

        },

        watch: {

        },

        methods: {

            limparTela() {
                this.filtros = {
                    ano_mes: moment().subtract(1, 'months').format('YYYY-MM'),
                    seq_de: 1,
                    seq_a: 4,
                    tipo: null,
                    marca: null,
                    opt1: 'td',
                    opt2: 'td',
                };
                this.listagemMapas = null;
                this.mapaSelecionado = null;
                this.itensMapa = null;
            },

            filtrar() {
                Event.$emit('VcLoader', true);
                $.ajax({
                    method: 'GET',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.tabelaMapa,
                    data: this.filtros
                }).done((response) => {
                    Event.$emit('VcLoader', false);
                    if(response.success) {
                        this.listagemMapas = response.data;
                    } else {
                        Event.$emit('VcAlert', {
                            type: 'warning',
                            title: 'Atenção!',
                            text: response.message
                        });
                    }
                }).fail(() => {
                    Event.$emit('VcLoader', false);
                    Event.$emit('VcAlert', {
                        type: 'error',
                        title: 'Erro!',
                        text: 'Houve uma falha no processamento.'
                    });
                });
            },

            rowCallback(row, data) {
                let fat = new Vue({
                    data: {vuedata: data, disable: false},
                    template: `<td class="text-center">
                                   <div style="display: inline; position: relative">
                                        <vc-input
                                            ref="input"
                                            type="checkbox"
                                            :disabled="disable"
                                            :group="false"
                                            :aligned="false"
                                            :width="0">
                                        </vc-input>
                                        <div v-show="disable"
                                            style="position:absolute; top: 0; right: 0; bottom: 0; left: 0"
                                            @click="notif">
                                        </div>
                                   </div>
                               </td>`,
                    components: {
                        VcInput
                    },
                    mounted() {
                        if (this.vuedata.editavel !== 'sim') {
                            this.disable = true;
                        }
                    },
                    methods: {
                        notif() {
                            if (this.vuedata.editavel !== 'sim') {
                                Event.$emit('VcAlert', {
                                    type: 'warning',
                                    title: 'Atenção!',
                                    text: this.vuedata.editavel
                                });
                            }
                        }
                    }
                });
                fat.$mount($('td:eq(0)', row)[0]);
            }
        },

        mounted() {
            this.limparTela();
        },
        
        components: {
            VcBox,
            VcButton,
            VcRow,
            VcCol,
            VcForm,
            VcFormBox,
            VcInputRange,
            VcInput,
            VcModal,
            VcTable
        }
    }
</script>
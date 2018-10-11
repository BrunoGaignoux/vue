<template>
    <div>
        <vc-box title="Mapa de Faturamento">
            <vc-form ref="mapaForm">
                <vc-row>
                    <vc-form-box title="Informações do Mapa de Faturamento" :width="6">
                        <vc-row>
                            <vc-input
                                    label="Número"
                                    type="select"
                                    :api-url="url.mascaraFatura"
                                    option-value="nro_controle"
                                    :option-text="['nro_controle', 'descricao']"
                                    sort="faturamento.nro_controle"
                                    :disabled="regra.nro_controle.disabled"
                                    v-model="mapa.nro_controle">
                            </vc-input>
                        </vc-row>

                        <vc-row>
                            <vc-input
                                    label="Descrição"
                                    :width="7"
                                    v-model="mapa.descricao"
                                    :disabled="true"
                            >
                            </vc-input>
                            <vc-input
                                    label="Centro de Custo"
                                    :width="5"
                                    v-model="mapa.ccusto_fili"
                                    :disabled="true">
                            </vc-input>
                        </vc-row>
                    </vc-form-box>

                    <vc-form-box title="Informações do Cliente" :width="6">
                        <vc-row>
                            <vc-input
                                    label="Cliente"
                                    v-model="mapa.nome_cli"
                                    :disabled="true">
                            </vc-input>
                        </vc-row>
                        <vc-row>
                            <vc-input
                                    label="Código"
                                    :width="5"
                                    v-model="mapa.cod_cli"
                                    :disabled="true">
                            </vc-input>
                            <vc-input label="CNPJ"
                                      v-model="mapa.cnpj_cli"
                                      :width="7"
                                      :disabled="true">
                            </vc-input>
                        </vc-row>
                    </vc-form-box>
                </vc-row>

                <vc-row>
                    <vc-form-box title="Informações do Centro de Custo" :width="12">
                        <vc-row>
                            <vc-input
                                    label="Centro de Custo"
                                    :width="2"
                                    v-model="mapa.ccusto_cli"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label=" "
                                    :width="4"
                                    v-model="mapa.ccusto_cli_desc"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="Unidade"
                                    :width="2"
                                    v-model="mapa.ccusto_cli_uni"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label=" "
                                    :width="4"
                                    v-model="mapa.ccusto_cli_uni_desc"
                                    :disabled="true">
                            </vc-input>
                        </vc-row>
                        <vc-row>
                            <vc-input
                                    label="Op SPOT"
                                    :width="1"
                                    v-model="mapa.op_spot"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="Responsável SPOT"
                                    :width="3"
                                    v-model="mapa.resp_spot"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="Coordenador"
                                    :width="1"
                                    v-model="mapa.coordenador"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label=" "
                                    :width="3"
                                    v-model="mapa.coordenador_usu"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="Controller"
                                    :width="1"
                                    v-model="mapa.controller"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label=" "
                                    :width="3"
                                    v-model="mapa.controller_usu"
                                    :disabled="true">
                            </vc-input>
                        </vc-row>
                    </vc-form-box>
                </vc-row>

                <vc-row>
                    <vc-form-box title="Outras Infos" :width="12">
                        <vc-row>
                            <vc-input
                                    label="Período"
                                    :width="3"
                                    v-model="mapa.periodo"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    type="currency"
                                    label="Faturamento Mínimo"
                                    :width="3"
                                    v-model="mapa.fatur_minimo"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="Cobrança ISS"
                                    :width="2"
                                    v-model="mapa.cobranca_iss"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="ISS Retido"
                                    :width="2"
                                    v-model="mapa.retido_iss"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="Prazo"
                                    :width="2"
                                    v-model="mapa.prazo"
                                    :disabled="true">
                            </vc-input>
                        </vc-row>
                        <vc-row>
                            <vc-input
                                    label="Cidade Prestação"
                                    :width="5"
                                    v-model="mapa.cidade_prest"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="PIS"
                                    :width="2"
                                    type="percent"
                                    v-model="mapa.pis"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    label="COFINS"
                                    type="percent"
                                    :width="2"
                                    v-model="mapa.cofins"
                                    :disabled="true">
                            </vc-input>
                            <vc-input
                                    type="date"
                                    label="Data Contrato"
                                    :width="3"
                                    v-model="mapa.data_contrato"
                                    :disabled="true">
                            </vc-input>
                        </vc-row>
                    </vc-form-box>
                </vc-row>

                <vc-row>
                    <vc-form-box title="Informações do Faturamento" :width="6">
                        <vc-row>
                            <vc-input
                                    label="Mês/Ano"
                                    type="date"
                                    date-type="month"
                                    :width="6"
                                    :disabled="regra.ano_mes.disabled"
                                    v-model="mapa.ano_mes">
                            </vc-input>
                            <vc-input
                                    label="Sequência"
                                    type="select"
                                    :data="[1, 2, 3, 4]"
                                    :width="6"
                                    :disabled="regra.sequencia.disabled"
                                    v-model="mapa.sequencia">
                            </vc-input>
                        </vc-row>
                    </vc-form-box>

                    <vc-form-box title="Faturar?" :width="6">
                        <vc-row>
                            <vc-input
                                    label="Faturar este mês?"
                                    type="select"
                                    :data="['S', 'N']"
                                    :width="4"
                                    v-model="mapa.faturar"
                                    :disabled="regra.faturar.disabled">
                            </vc-input>
                            <vc-input
                                    label="Justificativa"
                                    :width="8"
                                    :maxlength="150"
                                    v-model="mapa.just_fatura_mes"
                                    :disabled="regra.just_fatura_mes.disabled">
                            </vc-input>
                        </vc-row>
                    </vc-form-box>
                </vc-row>

                <vc-row>
                    <vc-col :width="5">&nbsp;</vc-col>
                    <vc-input
                            label="NFe Referência"
                            :width="2"
                            v-model="mapa.nfe_referencia"
                            :maxlength="10"
                            :disabled="regra.nfe_referencia.disabled">
                    </vc-input>
                </vc-row>

                <vc-row>
                    <vc-input
                            label="Descritivo de cobrança"
                            type="textarea"
                            v-model="mapa.descritivo_cob"
                            :maxlength="256"
                            :disabled="regra.descritivo_cob.disabled">
                    </vc-input>
                </vc-row>

                <vc-row>
                    <vc-col :width="5"></vc-col>
                    <vc-button
                            template="processar"
                            :width="2"
                            @click.native="processarMapa">
                    </vc-button>
                </vc-row>
            </vc-form>
        </vc-box>

        <vc-box title="Itens de Faturamento">
            <vc-table
                    ref="tabela"
                    :items="itens"
                    :cols="colunasTabela"
                    :row-callback="rowCallback">
            </vc-table>
        </vc-box>

        <vc-box title="Valores e Ações">
            <vc-row>
                <vc-input
                        label="Valor faturado"
                        type="currency"
                        :disabled="true"
                        v-model="mapa.valorjafaturado"
                        :width="3">
                </vc-input>
                <vc-input
                        label="Valor itens"
                        type="currency"
                        :disabled="true"
                        v-model="mapa.valor_itens"
                        :width="3">
                </vc-input>
                <vc-input
                        label="Valor impostos"
                        type="currency"
                        :disabled="true"
                        v-model="mapa.valor_impostos"
                        :width="3">
                </vc-input>
                <vc-input
                        label="Valor faturar"
                        type="currency"
                        :disabled="true"
                        v-model="mapa.valor_faturado"
                        :width="3">
                </vc-input>
            </vc-row>
            <vc-row>
                <vc-col><div class="text-center text-danger">{{ alertaValores }}</div></vc-col>
            </vc-row>
            <vc-row>
                <vc-col :width="2"></vc-col>
                <vc-button
                        template="limpar-tela"
                        :width="2"
                        :aligned="true"
                        @click.native="limparForm()">
                </vc-button>
                <vc-button
                        template="excluir"
                        :width="2"
                        :aligned="true"
                        :disabled="regra.excluir.disabled"
                        @click.native="excluirMapa()">
                </vc-button>
                <vc-button
                        template="gravar"
                        type="default"
                        :width="2"
                        :aligned="true"
                        :disabled="regra.gravar.disabled"
                        @click.native="gravarMapa()">
                </vc-button>
                <vc-button
                        template="processar"
                        text="Aprovar"
                        :width="2"
                        :aligned="true"
                        :disabled="regra.aprovar.disabled"
                        @click.native="aprovarMapa()">
                </vc-button>
            </vc-row>
        </vc-box>
    </div>
</template>

<script>

    // Import de componentes utilizados na página
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

    // @todo atualizar campos required
    
    export default {

        data() {
            return {
                // Mapa ativo na tela (será pre-setado no limparForm())
                mapa: { },

                // Regras de input (será pre-setado no limparForm())
                regra: { },

                // Tabela de itens
                tabela: null,
                itens: [ ],
                colunasTabela: [
                    {title: 'Item', data: 'codigo'},
                    {title: 'Descrição', data: 'descricao'},
                    {title: 'Tipo Fatura', data: 'tipo'},
                    {title: 'Cálculo', data: 'forma_calculo'},
                    {
                        title: 'Obrigatório', data: 'item_obrig',
                        render: function (data) {
                            if (data === '1' || data === 1) {
                                return '<div class="text-center"><i class="fa fa-check-circle" ' +
                                    'style="color: #3bd00a;"></i></div>';
                            } else {
                                return '';
                            }
                        }
                    },
                    {
                        title: 'Fatur Mínimo', data: 'compoe_minimo',
                        render: function (data) {
                            if (data === '1' || data === 1) {
                                return '<div class="text-center"><i class="fa fa-check-circle" ' +
                                    'style="color: #3bd00a;"></i></div>';
                            } else {
                                return '';
                            }
                        }
                    },
                    {
                        title: 'Compõe ISS', data: 'compoe_iss',
                        render: function (data) {
                            if (data === '1' || data === 1) {
                                return '<div class="text-center"><i class="fa fa-check-circle" ' +
                                    'style="color: #3bd00a;"></i></div>';
                            }
                        }
                    },
                    {title: 'Mês reajuste', data: 'mes_reajuste'},
                    {title: 'Valor', data: 'valor', width: '250px'},
                    {title: 'Quantidade', data: 'quantidade'},
                    {title: 'Valor Total', data: 'valor_total'},
                ],

                alertaValores: '',

                // URLs API
                url: {
                    api: window.Laravel.baseUri,
                    mascaraFatura: window.Laravel.baseUri + 'cadastro/erp-cad-faturamento/lista-mascara-faturamento',
                    processar: window.Laravel.baseUri + 'movimento/erp-mov-mapa-faturamento/processar',
                    gravar: window.Laravel.baseUri + 'movimento/erp-mov-mapa-faturamento/gravar',
                    aprovar: window.Laravel.baseUri + 'movimento/erp-mov-mapa-faturamento/aprovar',
                    baseMapa: window.Laravel.baseUri + 'movimento/erp-mov-mapa-faturamento/',
                },
            }
        },

        computed: {
            faturarMes() {
                return this.mapa.faturar;
            }
        },

        watch: {
            faturarMes(val) {
                this.regra.just_fatura_mes.disabled = val === 'S';
            },
            itens: {
                handler() {
                    if(this.itens.length > 0) {
                        this.recalcularValores();
                    }
                }, deep: true
            }
        },

        methods: {

            recalcularValores() {
                let soma_itens = 0;
                this.itens.forEach((e) => {
                    soma_itens += parseFloat(e.valor_total);
                });
                this.mapa.valor_itens = parseFloat(soma_itens);
                this.mapa.valor_impostos = 0;
                this.mapa.valor_faturado = 0;
                this.alertaValores = 'É necessário gravar o Mapa de Faturamento para ver os totais';
            },

            habilitaBotoes(bool = true) {
                this.regra.excluir.disabled = !bool;
                this.regra.gravar.disabled = !bool;
                if(this.mapa.aprova) {
                    this.regra.aprovar.disabled = !bool;
                } else {
                    this.regra.aprovar.disabled = true;
                }
            },

            travaMapa() {
                this.regra.nro_controle.disabled = true;
                this.regra.ano_mes.disabled = true;
                this.regra.sequencia.disabled = true;
            },

            processarMapa() {
                Event.$emit('VcLoader', true);
                $.ajax({
                    method: 'GET',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.processar,
                    data: this.mapa
                }).done((response) => {
                    Event.$emit('VcLoader', false);
                    if(response.success) {
                        this.mapa = response.data.mapa;
                        this.itens = response.data.itens;
                        this.habilitaEdicao();
                        this.habilitaBotoes();
                        this.travaMapa();
                        Vue.nextTick(() => {
                            this.alertaValores = '';
                        });
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
                        text: 'Houve uma falha no processamento do mapa.'
                    });
                });
            },

            // Habilita edição dos campos do mapa após buscá-lo
            habilitaEdicao() {
                this.regra.faturar.disabled = false;
                this.regra.nfe_referencia.disabled = false;
                this.regra.descritivo_cob.disabled = false;
            },

            excluirMapa() {
                Event.$emit('VcLoader', true);
                $.ajax({
                    method: 'DELETE',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.baseMapa + this.mapa.id,
                }).done((response) => {
                    Event.$emit('VcLoader', false);
                    if(response.success) {
                        Event.$emit('VcAlert', {
                            mode: 'alert',
                            type: 'success',
                            title: 'Sucesso!',
                            text: response.message
                        });
                        this.limparForm();
                    } else {
                        Event.$emit('VcAlert', {
                            mode: 'alert',
                            type: 'warning',
                            title: 'Atenção!',
                            text: response.message
                        });
                    }
                }).fail(() => {
                    Event.$emit('VcLoader', false);
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'error',
                        title: 'Erro!',
                        text: 'Houve uma falha no processamento!'
                    });
                });
            },

            gravarMapa() {
                Event.$emit('VcLoader', true);
                $.ajax({
                    method: 'POST',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.gravar,
                    data: {mapa: this.mapa, itens: this.itens}
                }).done((response) => {
                    Event.$emit('VcLoader', false);
                    if(response.success) {
                        this.mapa = response.data.mapa;
                        this.itens = response.data.itens;
                        Vue.nextTick(() => {
                            this.alertaValores = '';
                        });
                        Event.$emit('VcAlert', {
                            mode: 'alert',
                            type: 'success',
                            title: 'Sucesso!',
                            text: response.message
                        });
                    } else {
                        Event.$emit('VcAlert', {
                            mode: 'alert',
                            type: 'warning',
                            title: 'Atenção!',
                            text: response.message
                        });
                    }
                }).fail((response) => {
                    Event.$emit('VcLoader', false);
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'error',
                        title: 'Erro!',
                        text: 'Houve uma falha no processamento!'
                    });
                });
            },

            aprovarMapa() {
                let parar = false;
                this.itens.forEach((e) => {
                    if (((e.item_obrig === '1' || e.item_obrig === 1)  && (parseFloat(e.quantidade) === 0.0) || parseFloat(e.valor_total) === 0.0)) {
                        parar = true;
                    }
                });
                if (parar) {
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'warning',
                        title: 'Atenção!',
                        text: 'Há itens obrigatórios que não foram preenchidos!'
                    });
                    return;
                }

                if (this.alertaValores) {
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'warning',
                        title: 'Atenção!',
                        text: 'Você precisa gravar o mapa antes de aprová-lo!'
                    });
                    return;
                }

                Event.$emit('VcLoader', true);
                $.ajax({
                    method: 'POST',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.aprovar,
                    data: {mapa_id: this.mapa.id}
                }).done((response) => {
                    Event.$emit('VcLoader', false);
                    if(response.success) {
                        Event.$emit('VcAlert', {
                            mode: 'alert',
                            type: 'success',
                            title: 'Sucesso!',
                            text: response.message
                        });
                        this.limparForm();
                    } else {
                        Event.$emit('VcAlert', {
                            mode: 'alert',
                            type: 'warning',
                            title: 'Atenção!',
                            text: response.message
                        });
                    }
                }).fail((response) => {
                    Event.$emit('VcLoader', false);
                    console.log(response);
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'error',
                        title: 'Erro!',
                        text: 'Houve uma falha no processamento!'
                    });
                });
            },

            // Callback para linhas da tabela
            rowCallback(row, data) {
                // QUANTIDADE
                let qut = new Vue({
                    data: { vuedata: data },
                    template: `<td class="text-center">
                                   <vc-input v-model="vuedata.quantidade" type="number" :decimal="8">
                                   </vc-input>
                               </td>`,
                    components: { VcInput },
                    watch: {
                        vuedata: {
                            handler() {
                                this.vuedata.valor_total = parseFloat(this.vuedata.valor) * parseFloat(this.vuedata.quantidade);
                                if (this.vuedata.forma_calculo === 'P') {
                                    this.vuedata.valor_total = this.vuedata.valor_total / 100;
                                }
                                $(row).closest('table').DataTable().row(row).data(this.vuedata);
                            }, deep: true
                        }
                    }
                });
                qut.$mount($('td:eq(9)', row)[0]);

                // VALOR
                let vlr = new Vue({
                    data: { vuedata: data },
                    template: `<td class="text-center">
                                   <vc-input v-model="vuedata.valor" type="currency" :disabled="true"
                                        :width="'200px'">
                                   </vc-input>
                               </td>`,
                    components: { VcInput }
                });
                vlr.$mount($('td:eq(8)', row)[0]);

                // VALOR TOTAL
                let tot = new Vue({
                    data: { vuedata: data },
                    template: `<td class="text-center">
                                   <vc-input v-model="vuedata.valor_total" type="currency" :disabled="true"
                                        :width="'200px'">
                                   </vc-input>
                               </td>`,
                    components: { VcInput }
                });
                tot.$mount($('td:eq(10)', row)[0]);
            },

            limparForm() {
                // Seta os valores padrão
                this.mapa = {
                    nro_controle: null,
                    descricao: null,
                    ccusto_fili: null,
                    cod_cli: null,
                    periodo: null,
                    fatur_minimo: null,
                    cobranca_iss: null,
                    retido_iss: null,
                    prazo: null,
                    pis: null,
                    cofins: null,
                    data_contrato: null,
                    ccusto_cli_uni: null,
                    op_spot: null,
                    resp_spot: null,
                    coordenador: null,
                    ccusto_cli: null,
                    controller: null,
                    nome_cli: null,
                    cnpj_cli: null,
                    ccusto_cli_desc: null,
                    ccusto_cli_uni_desc: null,
                    coordenador_usu: null,
                    controller_usu: null,
                    just_fatura_mes: null,
                    nfe_referencia: null,
                    descritivo_cob: null,
                    valorjafaturado: null,
                    id: null,
                    valor_itens: null,
                    valor_impostos: null,
                    valor_faturado: null,
                    valor_desconto: null,
                    aliq_iss: null,
                    desct_obs: null,
                    desct_autoriz: null,
                    desct_data: null,
                    desct_hora: null,

                    sequencia: '1',
                    faturar: 'S',
                    ano_mes: moment().format('YYYY-MM')
                };

                // Seta as regras padrão
                this.regra = {
                    nro_controle: {
                        disabled: false
                    },
                    ano_mes: {
                        disabled: false
                    },
                    sequencia: {
                        disabled: false
                    },
                    just_fatura_mes: {
                        disabled: true
                    },
                    faturar: {
                        disabled:true
                    },
                    nfe_referencia: {
                        disabled: true
                    },
                    descritivo_cob: {
                        disabled: true
                    },
                    excluir: {
                        disabled: true
                    },
                    gravar: {
                        disabled: true
                    },
                    aprovar: {
                        disabled: true
                    }
                };

                // Limpa a tabela
                this.itens = [];
                this.alertaValores = '';
                this.habilitaBotoes(false);
            }
        },

        beforeMount() {
            this.limparForm();
        },

        mounted() {
            this.limparForm();
            this.tabela = this.$refs.tabela.tableApi;
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
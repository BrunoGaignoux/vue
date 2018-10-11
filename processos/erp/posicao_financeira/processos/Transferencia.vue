<template>
    <div>
        <vc-box title="Realizar transferência">
            <vc-form ref="formTransferencia">
                <vc-row>
                    <vc-input
                            label="Banco débito"
                            type="select"
                            :api-url="url.bancos"
                            option-value="cod"
                            :option-text="['cod', 'des', 'con', 'nom']"
                            v-model="transf.banco_deb"
                            :width="3">
                    </vc-input>
                    <vc-input
                            label="Banco crédito"
                            type="select"
                            :api-url="url.bancos"
                            option-value="cod"
                            :option-text="['cod', 'des', 'con', 'nom']"
                            v-model="transf.banco_cred"
                            :width="3">
                    </vc-input>
                    <vc-input
                            label="Tipo lançamento"
                            type="select"
                            :api-url="url.tipoLancto"
                            option-value="cod"
                            :option-text="['cod', 'des']"
                            v-model="transf.tipo_lancto"
                            :width="3">
                    </vc-input>
                    <vc-input
                            label="Data"
                            type="date"
                            v-model="transf.data"
                            :width="3">
                    </vc-input>
                </vc-row>
                <vc-row>
                    <vc-input
                            label="Documento"
                            :maxlength="20"
                            v-model="transf.doc"
                            :width="2">
                    </vc-input>
                    <vc-input
                            label="Histórico"
                            :maxlength="40"
                            v-model="transf.his"
                            :width="3">
                    </vc-input>
                    <vc-input
                            label="Valor"
                            type="currency"
                            v-model="transf.valor"
                            :width="2">
                    </vc-input>
                    <vc-input
                            label="Marca"
                            type="select"
                            :api-url="url.marca"
                            option-value="descricao"
                            :option-text="['descricao']"
                            v-model="transf.marca"
                            :width="3">
                    </vc-input>
                    <vc-button template="processar" :width="2"></vc-button>
                </vc-row>
            </vc-form>
        </vc-box>
        <vc-box title="Filtros para Consulta">
            <vc-form ref="formTransferencia">
                <vc-row>
                    <vc-input
                            label="Banco débito"
                            type="select"
                            :api-url="url.bancos"
                            option-value="cod"
                            :option-text="['cod', 'des', 'con', 'nom']"
                            v-model="filtros.banco_deb"
                            :width="3">
                    </vc-input>
                    <vc-input
                            label="Tipo lançamento"
                            type="select"
                            :api-url="url.tipoLancto"
                            option-value="cod"
                            :option-text="['cod', 'des']"
                            v-model="filtros.tipo_lancto"
                            :width="3">
                    </vc-input>
                    <vc-input
                            label="Data"
                            type="date"
                            v-model="filtros.data"
                            :width="2">
                    </vc-input>
                    <vc-input
                            label="Documento"
                            :maxlength="20"
                            v-model="filtros.doc"
                            :width="2">
                    </vc-input>
                    <vc-button template="filtrar" :width="2"></vc-button>
                </vc-row>
            </vc-form>
        </vc-box>
        <vc-box title="Consulta de Transferências">
            <vc-table
                    :cols="colunasTabela"
                    :filters="filtros"
                    :button="['excel']"
                    :row-callback="rowCallback">
            </vc-table>
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
                transf: {},
                filtros: {},
                url: {
                    bancos: window.Laravel.baseUri + 'cadastro/erp-cad-local-bancario',
                    tipoLancto: window.Laravel.baseUri + 'cadastro/erp-cad-tplancamento?transferencia=S',
                    marca: window.Laravel.baseUri + 'cadastro/erp-cad-marca',
                    exluir: window.Laravel.baseUri + 'movimento/erp-mov-posicao-financeira/excluirPosicaoFinanceiraId?id=',
                    validaBanco: window.Laravel.baseUri + 'movimento/erp-mov-posicao-financeira/validaBancoDeb?cod=',
                    validaTrava: window.Laravel.baseUri + 'movimento/erp-mov-posicao-financeira/validaDataTransfTrava',
                    validaDoc: window.Laravel.baseUri + 'movimento/erp-mov-posicao-financeira/localizaPosicaoFinanceira',
                    excluirEncontrada: window.Laravel.baseUri + 'movimento/erp-mov-posicao-financeira/excluirPosicaoFinanceira',
                    finalizaTransf: window.Laravel.baseUri + 'movimento/erp-mov-posicao-financeira/transferenciaBancariaGravar'


                },
                colunasTabela: [
                    {title: 'Ação', data: 'id'},
                    {title: 'Banco Deb', data: 'banco_deb'},
                    {title: 'Banco Cred', data: 'banco_cred'},
                    {title: 'Data', data: 'dmv'},
                    {title: 'Tipo Lancto', data: 'tipo_lancto'},
                    {title: 'Valor', data: 'valor'},
                    {title: 'Documento', data: 'doc'},
                    {title: 'Histórico', data: 'his'},
                    {title: 'Marca', data: 'marca'}
                ]
            }
        },

        computed: {

        },

        watch: {

        },

        methods: {
            confExcluir() {
                Event.$emit('VcAlert', {
                    mode: 'alert',
                    type: 'warning',
                    title: 'Atenção!',
                    text: 'Você tem certeza que deseja excluir esta transferência?',
                    confirmButtonText: 'Sim, excluir!',
                    cancelButtonText: 'Cancelar',
                    dangerMode: true,
                    caseConfirm: this.excluir()
                });
            },

            excluir() {
                Event.$emit('VcLoader', true);
                $.ajax({
                    type: 'GET',
                    headers: {'Authorization': 'Bearer ' + window.Laravel.userToken},
                    url: this.url.exluir + id,
                }).done((response) => {
                    Event.$emit('VcLoader', false);
                    if (response.success) {
                        Event.$emit('VcAlert', {
                            type: 'success',
                            title: 'Sucesso!',
                            text: response.message,
                        });
                    } else {
                        Event.$emit('VcAlert', {
                            type: 'error',
                            title: 'Erro!',
                            text: response.message,
                        });
                    }
                }).fail(() => {
                    this.emiteErro();
                });
            },

            carregarTabela() {
                this.tabela.tableApi.ajax.reload();
            },

            validaTransf() {
                if(!this.transf.banco_deb || !this.transf.banco_cred){
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'warning',
                        title: 'Atenção!',
                        text: 'Você precisa selecionar um Banco de Débito e um Banco de Crédito',
                    });
                    return false;
                }
                if(!this.transf.tipo_lancto){
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'warning',
                        title: 'Atenção!',
                        text: 'Você precisa selecionar um Tipo de Lançamento',
                    });
                    return false;
                }
                if(!this.transf.data || !this.transf.data){
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'warning',
                        title: 'Atenção!',
                        text: 'Você precisa preencher uma data e um valor para a transferência',
                    });
                    return false;
                }
                if(!this.transf.doc || !this.transf.his){
                    Event.$emit('VcAlert', {
                        mode: 'alert',
                        type: 'warning',
                        title: 'Atenção!',
                        text: 'Você precisa preencher o documento e o histórico da transferência',
                    });
                    return false;
                }
                return true;
            },

            validaBanco(cod) {
                let retorno = false;
                $.ajax({
                    type: 'GET',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: url.validaBanco + cod,
                }).done((result) => {
                    if (result.success) {
                        if (result.data[0] !== false) {
                            retorno = true;
                        }
                    } else {
                        Event.$emit('VcLoader', false);
                        Event.$emit('VcAlert', {
                            type: 'error',
                            title: 'Erro!',
                            text: response.message,
                        });
                    }
                }).fail(() => {
                    Event.$emit('VcLoader', false);
                    this.emiteErro();
                });
                return retorno;
            },

            validaTrava() {
                let retorno = false;
                $.ajax({
                    data: this.transf,
                    type: 'GET',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.validaTrava
                }).done((result) => {
                    if (result.success) {
                        if (result.data[0] !== false) {
                            retorno = true;
                        }
                    } else {
                        Event.$emit('VcLoader', false);
                        Event.$emit('VcAlert', {
                            type: 'error',
                            title: 'Erro!',
                            text: result.message,
                        });
                    }
                }).fail(() => {
                    Event.$emit('VcLoader', false);
                    this.emiteErro();
                });
                return retorno;
            },

            validaDoc() {
                let retorno = true;
                $.ajax({
                    data: this.transf,
                    type: 'GET',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.validaDoc,
                }).done((result) => {
                    if (result.success) {
                        retorno = result.data;
                    } else {
                        Event.$emit('VcLoader', false);
                        Event.$emit('VcAlert', {
                            type: 'error',
                            title: 'Erro!',
                            text: result.message,
                        });
                    }
                }).fail(() => {
                    Event.$emit('VcLoader', false);
                    this.emiteErro();
                });
                return retorno;
            },

            excluirEncontrada() {
                let retorno = false;
                $.ajax({
                    data: this.transf,
                    type: 'GET',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.excluirEncontrada,
                }).done((result) => {
                    if(result.success) {
                        retorno = true;
                    }  else {
                        Event.$emit('VcLoader', false);
                        Event.$emit('VcAlert', {
                            type: 'error',
                            title: 'Erro!',
                            text: result.message,
                        });
                    }
                }).fail(() => {
                    Event.$emit('VcLoader', false);
                    this.emiteErro();
                });
                return retorno;
            },

            finalizaTransf() {
                $.ajax({
                    data: this.transf,
                    type: 'GET',
                    headers: {
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.url.finalizaTransf,

                }).done((result) => {
                    Event.$emit('VcLoader', false);
                    if(result.success) {
                        Event.$emit('VcAlert', {
                            type: 'success',
                            title: 'Sucesso!',
                            text: result.message,
                        });
                        this.limparForm();
                    } else {
                        Event.$emit('VcAlert', {
                            type: 'error',
                            title: 'Erro!',
                            text: result.message,
                        });
                    }
                }).fail(() => {
                    Event.$emit('VcLoader', false);
                    this.emiteErro();
                });
            },

            emiteErro() {
                Event.$emit('VcAlert', {
                    type: 'error',
                    title: 'Erro!',
                    text: 'Falha ao processar a requisição',
                });
            },

            rowCallback(row, data) {
                let act = new Vue({
                    template: `<td class="text-center">
                                   <vc-button template="dtbexcluir"></vc-button>
                               </td>`,
                    components: {
                        VcButton
                    }
                });
                act.$mount($('td:eq(0)', row)[0]);
            },

            limparForm() {
                // Seta os valores padrão
                this.transf = {
                    banco_deb: null,
                    banco_cred: null,
                    tipo_lancto: null,
                    doc: null,
                    his: null,
                    data: null,
                    marca: null
                };
            }
        },

        beforeMount() {
            this.limparForm();
        },

        mounted() {
            this.limparForm();
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
<template>
    <div>
        <!-- INPUT -->
        <vc-box title="Input &lt;vc-input&gt;">
            <vc-row>
                <vc-col :width="4"></vc-col>
                <vc-input type="text" ref="retorno" :uppercase="false" placeholder="Retorno..." :width="3"
                          v-model="retorno"></vc-input>
                <vc-button template="limpar-tela" text="Limpar" :aligned="false" :width="2"
                           @click.native="limpaRetorno"></vc-button>
            </vc-row>
            <vc-row>
                <vc-form-box title="FormBox">
                    <vc-row>
                        <vc-input type="text" label="Text" :uppercase="true" :maxlength="25" :width="3"
                                  @input="updateRetorno"></vc-input>
                        <vc-input type="number" label="Number" prefix="UN " :width="3" :unmask="true"
                                  @input="updateRetorno"></vc-input>
                        <vc-input type="currency" label="Currency" :decimal="4" :width="3"
                                  @input="updateRetorno"></vc-input>
                        <vc-input type="percent" label="Percent" :decimal="2" :width="3"
                                  @input="updateRetorno"></vc-input>
                    </vc-row>
                    <vc-row>
                        <vc-input type="file" label="File" accept=".txt" :multi="true" :width="3"></vc-input>
                        <vc-input type="date" label="Date" :width="3" @input="updateRetorno"></vc-input>
                        <vc-input type="date" label="Date (month)" date-type="month" :width="3"
                                  @input="updateRetorno"></vc-input>
                        <vc-input type="date" label="Date (year)" date-type="year" :width="3"
                                  @input="updateRetorno"></vc-input>
                    </vc-row>
                </vc-form-box>

                <vc-form-box title="FormBox" :width="8">
                    <vc-row>
                        <vc-input type="cpf" label="CPF" :width="6" @input="updateRetorno"></vc-input>
                        <vc-input type="cnpj" label="CNPJ" :width="6" @input="updateRetorno"></vc-input>
                    </vc-row>
                    <vc-row>
                        <vc-input type="cpfcnpj" label="CPF/CNPJ" :width="6" @input="updateRetorno"></vc-input>
                        <vc-input type="cep" label="CEP" :width="6" @input="updateRetorno"></vc-input>
                    </vc-row>
                </vc-form-box>

                <vc-form-box title="FormBox" :width="4">
                    <vc-row>
                        <vc-input type="checkbox" label="Checkbox" :aligned="true" :width="6"
                                  @input="updateRetorno"></vc-input>
                        <vc-input type="checkbox" label="Checkbox" :aligned="true" :disabled="true" :width="6"></vc-input>
                    </vc-row>
                    <vc-row>
                        <vc-input type="radio" label="Radio" :aligned="true" :width="6" @input="updateRetorno"></vc-input>
                        <vc-input type="radio" label="Radio" :aligned="true" :width="6" :disabled="true"></vc-input>
                    </vc-row>
                </vc-form-box>
                <vc-form-box title="FormBox" :width="6">
                    <vc-row>
                        <vc-input type="select" label="Select" @input="updateRetorno" :data="selectOpts"
                                  :width="6"></vc-input>
                        <vc-input type="select" @input="updateRetorno" label="Select (multi)" :data="selectOpts"
                                  :width="6" :multi="true"></vc-input>
                    </vc-row>
                    <vc-row>
                        <vc-input type="select" label="Select Api" @input="updateRetorno"
                                  :api-url="`${apiBaseUri}cadastro/testes-vue`"
                                  :option-text="['nome', 'tipo']" option-value="nome" :width="6">
                        </vc-input>
                        <vc-input type="select" label="Select Api Params" @input="updateRetorno"
                                  :api-url="`${apiBaseUri}cadastro/testes-vue`"
                                  :option-text="['nome', 'tipo']" option-value="nome"
                                  :additional-params="{tipo: 'carro'}" :width="6">
                        </vc-input>
                    </vc-row>
                </vc-form-box>

                <vc-form-box title="FormBox" :width="6">
                    <vc-row>
                        <vc-input-range label="Input Range">
                            <template slot="first">
                                <vc-input type="text" :uppercase="true" :maxlength="25" :group="false"
                                          :width="0"></vc-input>
                            </template>
                            <template slot="second">
                                <vc-input type="text" :uppercase="true" :maxlength="25" :group="false"
                                          :width="0"></vc-input>
                            </template >
                        </vc-input-range>
                    </vc-row>
                    <vc-row>
                        <vc-input-range label="Input Range">
                            <template slot="first">
                                <vc-input type="select" :data="selectOpts" :group="false" :width="0">
                                </vc-input>
                            </template>
                            <template slot="second">
                                <vc-input type="select" :data="selectOpts" :group="false" :width="0">
                                </vc-input>
                            </template >
                        </vc-input-range>
                    </vc-row>
                </vc-form-box>
            </vc-row>

            <vc-row>
                <vc-form-box title="FormBox">
                    <vc-row>
                        <vc-input type="textarea" label="Textarea" :uppercase="true" :width="12" @input="updateRetorno"
                                  placeholder="Algum placeholder..."></vc-input>
                    </vc-row>
                </vc-form-box>
            </vc-row>
        </vc-box>

        <vc-box title="Table &lt;vc-table&gt;" :width="12">
            <vc-table ref="tabela" :api-url="`${apiBaseUri}cadastro/testes-vue`" select="multi" :cols="colsTable"
                      :row-callback="rowCallback"></vc-table>
        </vc-box>

        <vc-box title="Button &lt;vc-button&gt;" :width="6">
            <vc-col><h3>Type</h3></vc-col>
            <vc-button ref="btn1" type="default" :width="4" text="Default" @click.native="btnStart('btn1')"
                       :aligned="true"></vc-button>
            <vc-button ref="btn2" type="primary" :width="4" text="Primary" @click.native="btnStart('btn2')"
                       :aligned="true"></vc-button>
            <vc-button ref="btn3" type="danger" :width="4" text="Danger" @click.native="btnStart('btn3')"
                       :aligned="true"></vc-button>
            <vc-button ref="btn4" type="success" :width="4" text="Success" @click.native="btnStart('btn4')"
                       :aligned="true"></vc-button>
            <vc-button ref="btn5" type="info" :width="4" text="Info" @click.native="btnStart('btn5')"
                       :aligned="true"></vc-button>
            <vc-button ref="btn6" type="link" :width="4" text="Link" @click.native="btnStart('btn6')"
                       :aligned="true"></vc-button>

            <vc-col><div class="ruler"></div></vc-col>

            <vc-col><h3>Mode & Size</h3></vc-col>
            <vc-button type="primary" text="Block" :width="2" mode="block" :aligned="true"></vc-button>
            <vc-button type="default" text="Inline" :width="2" mode="inline" :aligned="true"></vc-button>
            <vc-button type="success" :width="2" mode="circle" icon="fa fa-paint-brush" size="lg"
                       :aligned="true"></vc-button>
            <vc-button type="danger" :width="2" mode="bitbucket" icon="fa fa-heart" :aligned="true"></vc-button>

            <vc-col><div class="ruler"></div></vc-col>

            <vc-col><h3>Template</h3></vc-col>
            <vc-button template="filtrar" :width="4" :aligned="true"></vc-button>
            <vc-button template="limpar-filtros" :width="4" :aligned="true"></vc-button>
            <vc-button template="processar" :width="4" :aligned="true" @click.native="loader()"></vc-button>
            <vc-button template="limpar-tela" :width="4" :aligned="true"></vc-button>
            <vc-button template="gravar" :width="4" :aligned="true"></vc-button>
            <vc-button template="editar" :width="4" :aligned="true"></vc-button>
            <vc-button template="excluir" :width="4" :aligned="true"></vc-button>
            <vc-button template="download" :width="4" :aligned="true"></vc-button>
            <vc-button template="upload" :width="4" :aligned="true"></vc-button>
            <vc-button template="table-info" :width="1" :aligned="true"></vc-button>
            <vc-button template="table-editar" :width="1" :aligned="true"></vc-button>
            <vc-button template="table-excluir" :width="1" :aligned="true"></vc-button>
        </vc-box>

        <vc-box title="Alert &lt;vc-alert&gt;" :width="6">
            <vc-button type="default" :width="3" text="Notificação" @click.native="notificacao"></vc-button>
            <vc-button type="default" :width="3" text="Alerta" @click.native="alerta"></vc-button>
            <vc-button type="primary" :width="3" text="Escolha" @click.native="escolha"></vc-button>
            <vc-button type="danger" :width="3" text="Perigo" @click.native="perigo"></vc-button>
        </vc-box>

        <vc-box title="Modal &lt;vc-modal&gt;" :width="2">
            <vc-button type="primary" :width="12" text="Modal" :aligned="false" @click.native="modalMd"></vc-button>
            <vc-modal ref="modal" title="Modal por componente">
                <template slot="body">
                    <p>Corpo da modal</p>
                </template>
                <template slot="footer">
                    <p>Rodapé da modal</p>
                </template>
            </vc-modal>
        </vc-box>

        <vc-box title="Localization" :width="4">
            {{ $t('Teste internacionalização') }}
        </vc-box>
    </div>
</template>

<script>

    // Import de componentes utilizados na página
    import VcBox from '../../vue/componentes/VcBox.vue'
    import VcButton from '../../vue/componentes/VcButton.vue'
    import VcRow from '../../vue/componentes/VcRow.vue'
    import VcForm from '../../vue/componentes/VcForm.vue'
    import VcFormBox from '../../vue/componentes/VcFormBox.vue'
    import VcInputRange from '../../vue/componentes/VcInputRange.vue'
    import VcInput from '../../vue/componentes/VcInput.vue'
    import VcModal from '../../vue/componentes/VcModal.vue'
    import VcTable from '../../vue/componentes/VcTable.vue'
    import VcCol from '../../vue/componentes/VcCol.vue'

    export default {

        // Declaração dos componentes utilizados na página
        components: {
            VcBox,
            VcButton,
            VcRow,
            VcForm,
            VcFormBox,
            VcInputRange,
            VcInput,
            VcModal,
            VcTable,
            VcCol
        },

        // Propriedades da instância Vue
        data() {
            return {
                retorno: null,
                apiBaseUri: window.Laravel.baseUri,
                colsTable: [
                    {title: 'Ações', width: '5%', data: null},
                    {title: 'ID', data: 'id'},
                    {title: 'Detalhe', width: '5%', data: null},
                    {title: 'Tipo', data: 'tipo'},
                    {title: 'Nome', data: 'nome'}
                ],
                selectOpts: [
                    {id: 'Peugeot', text: 'Peugeot'},
                    {id: 'Fiat', text: 'Fiat'},
                    {id: 'Ford', text: 'Ford'},
                    {id: 'Chevrolet', text: 'Chevrolet'},
                    {id: 'Renault', text: 'Renault'},
                    {id: 'Hyundai', text: 'Hyundai'},
                    {id: 'Toyota', text: 'Toyota'},
                ]
            }
        },

        // Lifecycle hook para inicializar a tabela
        mounted() {
            this.$refs.tabela.tableApi.draw();
        },

        // Métodos da instância Vue
        methods: {

            // Função que será executada em cada linha do VcTable após sua renderização
            rowCallback(row, data) {
                let act = new Vue({
                    template: `<td class="text-center">
                                   <vc-button template="table-editar" width="inline"></vc-button>&nbsp;&nbsp;
                                   <vc-button template="table-excluir" width="inline"></vc-button>
                               </td>`,
                    components: {
                        VcButton
                    }
                });
                act.$mount($('td:eq(0)', row)[0]);

                let det = new Vue({
                    template: '<td><vc-button template="table-info"></vc-button></td>',
                    components: {
                        VcButton
                    }
                });
                det.$mount($('td:eq(2)', row)[0]);
            },

            // Atualiza o input 'Retorno' do topo da página
            updateRetorno(value) {
                this.retorno = value;
            },
            limpaRetorno() {
                this.retorno = null;
            },

            // Abre a modal configurada na página
            modalMd() {
                this.$refs.modal.show();
            },

            // Função auxiliar para exemplificar os botões, funcionalidade específica desta tela
            btnStart(btn) {
                this.$refs[btn].loader.start();
                setTimeout(() => {
                    this.$refs[btn].loader.stop();
                }, 3000);
            },

            // Abre uma notificação
            notificacao() {
                Event.$emit('VcAlert', {
                    type: 'success',
                    title: 'Notificação!',
                    text: 'Esta é uma mensagem de notificação!'
                });
            },

            // Abre um alerta simples
            alerta() {
                Event.$emit('VcAlert', {
                    mode: 'alert',
                    type: 'warning',
                    title: 'Alerta!',
                    text: 'Esta é uma mensagem de alerta!'
                });
            },

            // Abre um alerta com escolha
            escolha() {
                Event.$emit('VcAlert', {
                    mode: 'alert',
                    type: 'question',
                    title: 'Escolha',
                    text: 'Aqui você pode fazer uma escolha.',
                    cancelButtonText: 'Não',
                    confirmButtonText: 'Sim',
                    caseConfirm() {
                        console.log('clicou em Sim');
                    },
                    caseCancel() {
                        console.log('clicou em Não');
                    }
                })
            },

            // Abre um alerta no modo DANGER
            perigo() {
                Event.$emit('VcAlert', {
                    mode: 'alert',
                    type: 'error',
                    dangerMode: true,
                    title: 'Perigo!',
                    text: 'Esta é uma confirmação de uma ação perigosa!',
                    cancelButtonText: 'Cancelar',
                    confirmButtonText: 'Prossiga'
                });
            },

            loader() {
                Event.$emit('VcLoader', true);
                setTimeout(() => {
                    Event.$emit('VcLoader', false);
                }, 5000)
            }
        }
    }
</script>

<style scoped>
    /* CSS que será aplicado somente ao template da instância Vue*/
    .ruler {
        margin-top: 25px;
        margin-bottom: 25px;
        width: 100%;
        height: 1px;
        background-color: #ddd;
        vertical-align: middle;
    }
</style>
<template>
    <div class="table-responsive">
        <table ref="tableElement" class="table table-striped table-bordered table-hover">
            <slot>
            </slot>
        </table>
    </div>
</template>

<script>

    export default {

        data() {
            return {
                tableApi: null,
                tableHtml: null
            }
        },

        props: {
            cols: Array,
            select: {
                type: String,
                default: ''
            },
            buttons: Array,
            drawCallback: Function,
            rowCallback: Function,
            apiUrl: String,
            serverSide: {
                type: Boolean,
                default: false
            },
            items: Array,
            filters: Object,
            orderCol: {
                type: Number,
                default: 1
            },
            orderDir: {
                type: String,
                default: 'asc'
            }
        },

        watch: {
            items(val) {
                if (this.tableApi) {
                    this.tableApi.clear();
                    this.tableApi.rows.add(val);
                    this.tableApi.draw();
                    if (val.length > 0) {
                        this.tableApi.columns.adjust().draw();
                    }
                }
            }
        },

        mounted() {
            let buttons = this.buttons ? this.buttons : [];
            if(this.select && this.select === 'multi') {
                buttons.push('selectAll');
                buttons.push('selectNone');
            }

            let options = {
                // Opções fixas
                destroy: true,
                responsive: false,
                autoWidth: false,
                lengthMenu: [3,10,25,50],
                displayLength: 10,
                scrollX: true,
                deferRender: true,
                processing: true,
                dom: '<"html5buttons"B>lTfgirtp',
                language: {
                    buttons: {
                        selectAll: 'Selecionar todos',
                        selectNone: 'Desselecionar'
                    },
                    url: 'https://cdn.datatables.net/plug-ins/1.10.12/i18n/Portuguese-Brasil.json'
                },

                // Opções alternativas
                order: [this.orderCol, this.orderDir],
                data: this.items,
                columns: this.cols,
                buttons: buttons,
                select: this.select ? {style: this.select} : false,
                serverSide: this.serverSide,
                ajax: this.apiUrl ? {
                    type: 'GET',
                    dataType: 'json',
                    data: {filters: this.filters, table: 1, vueComp: 1},
                    headers: {
                        'Accept': 'application/json',
                        'Content-Type':'application/json',
                        'Authorization': 'Bearer ' + window.Laravel.userToken
                    },
                    url: this.apiUrl
                } : false,
                sAjaxDataProp: this.apiUrl ? 'data' : null,
                drawCallback: (settings) => {
                    if(this.drawCallback) {
                        this.drawCallback(settings);
                    }
                },
                rowCallback: (row, data) => {
                    if(this.rowCallback) {
                        this.rowCallback(row, data);
                    }
                }
            };

            this.tableApi = $(this.$refs.tableElement).DataTable(options);
            this.tableHtml = this.$refs.tableElement;
        }
    }
</script>

<style>
    div.dataTables_wrapper div.dataTables_filter input,
    div.dataTables_wrapper div.dataTables_length select {
        height: 34px !important;
    }
    table.dataTable tbody td {
        white-space: nowrap;
        overflow: hidden;
    }
    div.dataTables_wrapper div.dataTables_processing {
        background-color: #fff !important;
        color: #fff !important;
        border: 0 !important;
        z-index: 999 !important;
    }
</style>
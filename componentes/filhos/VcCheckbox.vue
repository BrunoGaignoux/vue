<template>
    <div>
        <label v-show="aligned" class="control-label label-pad">&nbsp;</label>
        <label class="control-label input-label">
            <input type="checkbox" :autofocus="focus" :required="required" :disabled="disabled" class="i-checks"
                   ref="input" :checked="value">
            {{ label }}
        </label>
    </div>
</template>

<script>

    export default {

        data() {
            return {
                input: null
            }
        },

        props: {
            value: false,
            label: String,
            disabled: {
                default: false,
                type: Boolean
            },
            required: {
                default: false,
                type: Boolean
            },
            focus: {
                default: false,
                type: Boolean
            },

            // Específicas
            aligned: {
                default: true,
                type: Boolean
            }
        },

        mounted() {
            $(this.$refs.input).on('ifChanged', () => {
                this.$emit('input', $(this.$refs.input).is(':checked'));
            });
            this.input = this.$refs.input;
        }
    }
</script>
<style scoped>
    label.label-pad {
        min-height: 1.3em !important;
        margin-bottom: 5px !important;
        display: block;
    }
</style>
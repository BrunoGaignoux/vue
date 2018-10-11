<template>
    <div>
        <label v-show="aligned" class="control-label label-pad">&nbsp;</label>
        <label class="control-label input-label">
            <input type="radio" :autofocus="focus" :required="required" :name="name" :disabled="disabled" class="i-checks"
                   ref="input" :value="val">
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
            value: null,
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
            },
            name: String,
            val: String
        },

        mounted() {
            $(this.$refs.input).on('ifChanged', () => {
                this.$emit('input', this.$refs.input.value);
            });
            this.input = this.$refs.input;
        },

        watch: {
            value(val) {
                let cond = (val === this.$refs.input.value);
                $(this.$refs.input).prop('checked', cond);
            }
        }
    }
</script>
<style scoped>
    label.label-pad {
        min-height: 1.3em !important;
        margin-bottom: 5px !important;
        display: block;
    }
    .input-label {
        margin-bottom: 12px !important;
    }
</style>
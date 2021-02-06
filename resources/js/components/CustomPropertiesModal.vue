<template>
    <modal @modal-close="handleClose">
        <card class="overflow-hidden">
            <form class="bg-white rounded-lg shadow-lg overflow-hidden w-action-fields"
                @submit.prevent="handleUpdate"
                autocomplete="off"
            >

                <h2 class="border-b border-40 py-8 px-8 text-90 font-normal text-xl">Дополнительные настройки</h2>

                <div v-for="field in fields" :key="field.attribute" class="action">
                    <component :is="'form-' + field.component" :field="field"/>
                </div>

                <div class="bg-30 px-6 py-3 flex">
                    <div class="flex items-center ml-auto">
                        <button type="button" dusk="cancel-action-button" class="btn btn-link dim cursor-pointer text-80 ml-auto mr-6" @click.prevent="handleClose">
                            {{__('Cancel')}}
                        </button>

                        <button type="submit" class="btn btn-default btn-primary">
                            {{__('Update')}}
                        </button>
                    </div>
                </div>

            </form>
        </card>
    </modal>
</template>

<script>
  export default {
    props: {
        fields: {
            type: Array,
            required: true,
        }
    },

    methods: {
        handleClose () {
            this.$emit('close')
        },

        handleUpdate () {
            let formData = new FormData()

            this.fields.forEach(field => field.fill(formData))

            this.$emit('update', formData)
        }
    }
  }
</script>

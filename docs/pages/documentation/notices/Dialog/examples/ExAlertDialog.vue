<template>
    <section>
        <button class="button is-medium is-primary" @click="alert">
            Launch alert (default)
        </button>
        <button class="button is-medium is-primary" @click="alertCustom">
            Launch alert (custom)
        </button>
    </section>
</template>

<script>
    export default {
        methods: {
            alert() {
                this.$dialog.alert('Everything looks fine!')
            },
            alertCustom() {
                this.$dialog.alert({
                    title: 'Title Alert',
                    message: 'I have a title, a custom button and <b>HTML</b>!',
                    confirmText: 'Cool!'
                })
            }
        }
    }
</script>

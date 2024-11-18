<template>
    <v-snackbar v-model="isOpen" v-bind="snackProps">
        <span v-html=text></span>
        <template v-slot:actions>
            <v-btn variant="text" @click="isOpen = false">
                Close
            </v-btn>
        </template>
    </v-snackbar>
</template>

<script setup>

const props = defineProps(["defaultProps"]);

let isOpen = defineModel({ name: 'isOpen', default: false });
let text = defineModel('text');

let snackProps = {};
let snackQueue = [];


/* Adds snack to queue
properties is object defined here https://vuetifyjs.com/en/api/v-snackbar/
*/
function showSnack(message, properties) {
    snackQueue.push({ message: message, props: properties });
    if (isOpen.value === false) { consumeSnack(); }
}

function consumeSnack() {
    if (snackQueue.length == 0) return;
    let snack = snackQueue.shift();
    snackProps = { ...props.defaultProps, ...snack.props };
    text = snack.message;
    isOpen.value = true;
}

Vue.watch(isOpen, (newVal, oldVal) => {
    if (newVal === false) {
        setTimeout(() => {
            consumeSnack();
        }, 100);
    }
});

window.showSnack = showSnack;

</script>
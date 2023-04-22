<template>
    <Transition enter-active-class="animated animate__fadeIn"
        leave-active-class="animated animate__fadeOut" mode="out-in">
        <div v-if="resultado" class="panel result">
            <div v-if="life == 0" class="win">Você ganhou!!</div>
            <div v-else class="lose">Você perdeu!!</div>
        </div>
    </Transition>

</template>

<script>
export default {
    props: ['resultado', 'life']
}
</script>

<style>

</style>
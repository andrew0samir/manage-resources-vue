<template>
    <button :class="mode">
        <slot></slot>
    </button>
</template>

<script>
export default {
    props: ['mode']
}
</script>

<style scoped>
button {
    padding: 0.75rem 1.5rem;
    margin: .5rem;
    font-family: inherit;
    background-color: #3a0061;
    border: 1px solid #290044;
    border-radius: 10px;
    color: white;
    cursor: pointer;
}

button:hover,
button:active {
    background-color: #270041;
    border-color: #270041;
}

.flat {
    background-color: transparent;
    color: #3a0061;
    border: none;
}

.flat:hover,
.flat:active {
    background-color: #edd2ff;
}
</style>
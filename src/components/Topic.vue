<template>
    <div>
        <h1>Topic!: {{ title }}</h1>
        <ul>
            <li v-for="(child, idx) in children" :key="idx">
                <a href="#" @click="$emit('select', idx)">{{ idx }}</a>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        title: { type: String, required: true },
        children: { type: Array, required: false, default: () => [] },
    },
};
</script>
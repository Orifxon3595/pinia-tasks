<template>
    <div class="task">
        <h1>{{ task.title }}</h1>
    </div>
</template>

<script>
    export default {
        props: ['task']
    }
</script>
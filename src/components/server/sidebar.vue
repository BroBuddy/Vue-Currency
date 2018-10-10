<template>
<div class="col-xs-12 col-md-4">
    <ul class="list-group">
        <li class="list-group-item"
        v-for="(index, key) in 5" :key="key">
            Server #{{ index }} - {{ key }}
        </li>
    </ul>
</div>
</template>

<script>
</script>

<style lang="scss" scoped>
</style>

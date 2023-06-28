<template>
<div id="app">
    <div class="vh-100 vw-100 d-flex justify-content-center align-items-lg-center page-background row m-0">
        <CombinationSum />
    </div>
</div>
</template>

<script>
import CombinationSum from './components/CombinationSum.vue'

export default {
    name: 'App',
    components: {
        CombinationSum
    }
}
</script>

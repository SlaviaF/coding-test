<template>
<div id="app">
    <div class="vh-100 d-flex container-fluid justify-content-center align-items-lg-center page-background row rounded" >   
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



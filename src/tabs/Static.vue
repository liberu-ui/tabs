<template>
    <div class="animated fadeIn"
        v-if="active">
        <slot/>
    </div>
</template>

<script>

export default {
    props: {
        active: {
            type: Boolean,
            default: false,
        },
    },
};

</script>

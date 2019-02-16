<template>
    <renderless-tabs>
        <div slot-scope="{ tabs, select }">
            <div :class="[
                    'tabs', 'is-' + alignment, 'is-' + size, { 'is-boxed': boxed },
                    { 'is-toggle': toggle }, { 'is-toggle-rounded': toggleRounded },
                    { 'is-fullwidth': fullwidth }
                ]">
                <ul class="tab-list">
                    <li :class="{ 'is-active': tab.active }"
                        v-for="tab in tabs"
                        :key="tab.id">
                        <a @click="select(tab)"
                            :disabled="tab.disabled">
                            <slot name="label"
                                :tab="tab.id">
                                {{ tab.id }}
                            </slot>
                        </a>
                    </li>
                </ul>
            </div>
            <slot/>
        </div>
    </renderless-tabs>
</template>

<script>
import RenderlessTabs from '../renderless/Tabs.vue';

export default {

    components: { RenderlessTabs },

    props: {
        alignment: {
            type: String,
            default: 'left',
            validator: value => ['left', 'centered', 'right']
                .includes(value),
        },
        boxed: {
            type: Boolean,
            default: false,
        },
        fullwidth: {
            type: Boolean,
            default: false,
        },
        size: {
            type: String,
            default: 'normal',
            validator: value => ['normal', 'small', 'medium', 'large']
                .includes(value),
        },
        toggle: {
            type: Boolean,
            default: false,
        },
        toggleRounded: {
            type: Boolean,
            default: false,
        },
    },
};
</script>

<style lang="scss">
    a[disabled] {
        opacity: .5;
        cursor: not-allowed;
    }
</style>

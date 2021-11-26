<template>
    <div class="wrapper">
        <div :class="[
                'tabs', 'is-' + alignment, 'is-' + size, { 'is-boxed': boxed },
                { 'is-toggle': toggle }, { 'is-toggle-rounded': toggleRounded },
                { 'is-fullwidth': fullwidth }
            ]">
            <ul class="tab-list">
                <core-tabs>
                    <template #default="{ key, tabs, tabEvents }">
                        <li :class="{ 'is-active': tab.active }"
                            v-for="tab in tabs"
                            :key="key(tab.id)">
                            <a :disabled="tab.disabled"
                                v-on="tabEvents(tab)">
                                <slot name="label"
                                    :tab="tab.id">
                                    {{ tab.id }}
                                </slot>
                            </a>
                        </li>
                    </template>
                </core-tabs>
            </ul>
        </div>
        <slot/>
    </div>
</template>

<script>
import CoreTabs from '../renderless/CoreTabs.vue';

export default {
    name: 'Tabs',

    components: { CoreTabs },

    props: {
        alignment: {
            type: String,
            default: 'left',
            validator: (value) => ['left', 'centered', 'right']
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
            validator: (value) => ['normal', 'small', 'medium', 'large']
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

<template>
    <core-tabs>
        <template v-slot:default="{ tabs, tabBindings, tabEvents }">
            <div class="wrapper">
                <div :class="[
                        'tabs', 'is-' + alignment, 'is-' + size, { 'is-boxed': boxed },
                        { 'is-toggle': toggle }, { 'is-toggle-rounded': toggleRounded },
                        { 'is-fullwidth': fullwidth }
                    ]">
                    <ul class="tab-list">
                        <li :class="{ 'is-active': tab.active }"
                            v-for="tab in tabs"
                            :key="tab.id">
                            <a v-bind="tabBindings(tab)"
                                v-on="tabEvents(tab)">
                                <slot name="label"
                                    :tab="tab.id">
                                    {{ tab.id }}
                                </slot>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
            <slot/>
        </template>
    </core-tabs>
</template>

<script>
import CoreTabs from '../renderless/Tabs.vue';

export default {
    name: 'Tabs',

    components: { CoreTabs },

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

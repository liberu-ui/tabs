<template>
    <core-tabs v-on="$listeners"
        ref="tabs">
        <template v-slot:default="{ tabs, tabEvents }">
            <div class="enso-tabs">
                <div class="tabs is-toggle is-fullwidth no-scrollbars"
                    :class="`is-${size}`">
                    <ul class="tab-list has-background-grey-light">
                        <li :class="{ 'is-active': tab.active }"
                            v-for="tab in tabs"
                            :key="tab.id">
                            <a :class="{ 'has-background-white has-text-grey-dark': tab.active }"
                                :disabled="tab.disabled"
                                v-on="tabEvents(tab)">
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
        </template>
    </core-tabs>
</template>

<script>
import CoreTabs from '../renderless/Tabs.vue';

export default {
    name: 'EnsoTabs',

    components: { CoreTabs },

    props: {
        size: {
            type: String,
            default: 'normal',
            validator: value => ['normal', 'small', 'medium', 'large']
                .includes(value),
        },
    },

    computed: {
        tabs() {
            return this.$refs.tabs.tabs;
        },
    },
};
</script>

<style lang="scss">
    .enso-tabs  {
        position: relative;

        .tabs.is-fullwidth.is-toggle > .tab-list {
            border-radius: 6px;

            li {
                padding: 0.4em;
            }

            .is-active > a {
                opacity: 1;
                font-weight: 600;
            }

            a {
                transition: background 0.3s;
                border: unset;
                border-radius: 6px;
                opacity: 0.7;

                &[disabled] {
                    opacity: .4;
                    cursor: not-allowed;
                }
            }
        }
    }
</style>

<template>
    <renderless-tabs>
        <div slot-scope="{ tabs, select }">
            <div class="tabs is-enso is-toggle is-fullwidth no-scrollbars"
                :class="`is-${size}`">
                <ul class="tab-list has-background-grey-light">
                    <li :class="{ 'is-active': tab.active }"
                        v-for="tab in tabs"
                        :key="tab.id">
                        <a :class="{ 'has-background-white has-text-grey-dark': tab.active }"
                            @click="select(tab)"
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
        size: {
            type: String,
            default: 'normal',
            validator: value => ['normal', 'small', 'medium', 'large']
                .includes(value),
        },
    },
};
</script>

<style lang="scss">
    .tabs.is-enso.is-fullwidth.is-toggle > .tab-list {
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
</style>

<script>

import Alive from './Alive.vue';
import Static from './Static.vue';

export default {
    props: {
        id: {
            type: [String, Object],
            required: true,
        },
        default: {
            type: Boolean,
            default: false,
        },
        keepAlive: {
            type: Boolean,
            default: false,
        },
    },

    data: () => ({
        active: false,
        disabled: false,
    }),

    computed: {
        tab() {
            return this.keepAlive
                ? Alive
                : Static;
        },
    },

    created() {
        this.register();

        if (this.default) {
            this.activate();
        }
    },

    methods: {
        register() {
            this.$parent.$emit('register', this);
        },
        activate() {
            this.$parent.$emit('activate', this);
        },
        enable() {
            this.disabled = false;
        },
        disable() {
            if (!this.active) {
                this.disabled = true;
            }
        },
        remove() {
            this.$parent.$emit('remove', this);
            this.$destroy();
        },
    },

    render(renderEl) {
        return renderEl(this.tab, {
            props: {
                active: this.active,
                key: this.id,
            },
        }, this.$slots.default);
    },
};

</script>

<script>
import Alive from './Alive.vue';
import Static from './Static.vue';

export default {
    inject: ['tabsState'],

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
        tabs() {
            return this.tabsState;
        },
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
            this.tabs.register(this);
        },
        activate() {
            this.tabs.activate(this);
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
            this.tabs.remove(this);
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

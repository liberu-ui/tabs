<script>
import 'animate.css';

export default {
    name: 'Tab',

    inject: { tabs: { from: 'tabState' } },

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

    created() {
        this.register();

        if (this.default) {
            this.activate();
        }
    },

    beforeDestroy() {
        this.remove();
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
        if (!this.keepAlive && !this.active) {
            return null;
        }

        return renderEl('div', {
            attrs: {
                class: 'animate__animated animate__fadeIn',
            },
            directives: this.keepAlive
                ? [{ name: 'show', value: this.active }]
                : [],
        }, [this.$slots.default]);
    },
};
</script>

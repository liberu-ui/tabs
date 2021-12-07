<script>
import { h, resolveDirective, withDirectives } from 'vue'
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

    beforeUnmount() {
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

    render() {
        if (!this.keepAlive && !this.active) {
            return null;
        }

        const show = resolveDirective('show');
        const directives = this.keepAlive
            ? [[show, this.active]]
            : [];

        return withDirectives(
            h(
                'div',
                { class: 'animate__animated animate__fadeIn'},
                [this.$slots.default()]
            ),
            directives);
    },
};
</script>

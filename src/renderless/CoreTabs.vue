<script>
export default {
    name: 'CoreTabs',

    inheritAttrs: false,

    emits: ['activated', 'registered', 'removed', 'selected'],

    data: () => ({
        tabs: [],
    }),

    provide() {
        return {
            tabState: {
                tabs: this.tabs,
                register: this.register,
                activate: this.activate,
                remove: this.remove,
            },
        };
    },

    methods: {
        activate(activeTab) {
            this.tabs.forEach((tab) => {
                tab.active = activeTab._.uid === tab._.uid;
            });

            this.$nextTick(() => this.$emit('activated', activeTab.id));
        },
        key(id) {
            return typeof id === 'object'
                ? JSON.stringify(id)
                : id;
        },
        register(tab) {
            this.tabs.push(tab);
            this.$emit('registered', tab.id);

            if (this.tabs.length === 1) {
                this.activate(tab);
            }
        },
        remove(tab) {
            const index = this.tabIndex(tab);
            this.tabs.splice(index, 1);
            this.$emit('removed', tab.id);
        },
        select(tab) {
            if (!tab.disabled) {
                this.$emit('selected', tab.id);
                this.activate(tab);
            }
        },
        tabIndex(tab) {
            return this.tabs.findIndex(({ _ }) => _.uid === tab._.uid);
        },
    },

    render() {
        return this.$slots.default({
            key: this.key,
            tabs: this.tabs,
            tabEvents: tab => ({
                click: () => this.select(tab),
            }),
        });
    },
};
</script>

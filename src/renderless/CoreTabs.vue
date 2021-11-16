<script>
export default {
    name: 'CoreTabs',

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
                tab.active = activeTab._uid === tab._uid;
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
            this.$emit('selected', tab.id);
            this.activate(tab);
        },
        tabIndex(tab) {
            return this.tabs.findIndex(({ _uid }) => _uid === tab._uid);
        },
    },

    render() {
        return this.$slots.default({
            key: this.key,
            tabs: this.tabs,
            tabEvents: tab => ({
                click: () => (!tab.disabled ? this.select(tab) : null),
            }),
        });
    },
};
</script>

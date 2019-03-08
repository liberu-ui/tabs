<script>
export default {
    name: 'CoreTabs',

    data: () => ({
        tabs: [],
    }),

    provide() {
        return {
            tabsState: {
                tabs: this.tabs,
                register: this.register,
                activate: this.activate,
                remove: this.remove,
            },
        };
    },

    methods: {
        register(tab) {
            this.tabs.push(tab);
            this.$emit('registered', tab.id);

            if (this.tabs.length === 1) {
                this.activate(tab);
            }
        },
        remove(tab) {
            this.tabs.splice(this.tabIndex(tab), 1);
            this.$emit('removed', tab.id);
            tab.$destroy();
        },
        select(tab) {
            this.$emit('selected', tab.id);
            this.activate(tab);
        },
        activate(activeTab) {
            this.tabs.forEach((tab) => {
                tab.active = activeTab._uid === tab._uid;
            });

            this.$emit('activated', activeTab.id);
        },
        tabIndex(tab) {
            return this.tabs
                .findIndex(({ _uid }) => _uid === tab._uid);
        },
    },

    render() {
        return this.$scopedSlots.default({
            tabs: this.tabs,
            register: this.register,
            remove: this.remove,
            select: this.select,
            activate: this.activate,
        });
    },
};
</script>

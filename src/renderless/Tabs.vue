<script>

export default {
    data: () => ({
        tabs: [],
    }),

    created() {
        this.$on('register', this.register);
        this.$on('activate', this.activate);
        this.$on('remove', this.remove);
    },

    methods: {
        register(tab) {
            this.tabs.push(tab);

            if (this.tabs.length === 1) {
                this.activate(tab);
            }
        },
        remove(tab) {
            this.tabs.splice(this.tabIndex(tab), 1);
            tab.$destroy();
        },
        select(tab) {
            this.$emit('selected', tab);
            this.activate(tab);
        },
        activate(activeTab) {
            this.tabs.forEach((tab) => {
                tab.active = activeTab._uid === tab._uid;
            });

            this.$emit('activated', activeTab);
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

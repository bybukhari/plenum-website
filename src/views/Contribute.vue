<template>
    <main ref="home" class="content-container">
        <!-- TODO: use component associated with given content-type -->
        <basic-page
            v-for="page in pages"
            :page="page"
        ></basic-page>
    </main>
</template>

<script lang="ts">
import {Component, Prop, Vue} from 'vue-property-decorator';
import BasicPage from '../components/content-types/BasicPage';

@Component({
    components: {
        BasicPage
    },
})

export default class Contribute extends Vue {
    private pages: Array<any>;

    constructor() {
        super();

        this.pages = [];
    }

    // When view is mounted, retrieve article
    private created() {
        this.initContributePage();
    }

    private initContributePage(): void {
        if (this.$store.getters['pages/getContributePage'].length === 0) {
            this.$store.dispatch('pages/initContributePage')
                .then(res => {
                    this.pages = this.$store.getters['pages/getContributePage'];
                    this.$store.dispatch('setAppLoading', false);
                });
        } else {
            this.pages = this.$store.getters['pages/getContributePage'];
            this.$store.dispatch('setAppLoading', false);
        }
    }
}
</script>

<style lang="scss" scoped>

</style>

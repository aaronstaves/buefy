<template>
    <section class="documentation">
        <app-header ref="header"></app-header>

        <div class="hero is-primary">
            <div class="hero-body">
                <div class="container">
                    <h1 class="title">Documentation</h1>
                    <h2 class="subtitle">Learn everything you need to start using Buefy ;)</h2>
                </div>
            </div>

            <div class="hero-foot">
                <div class="container">
                    <nav class="tabs is-boxed">
                        <ul>
                            <li v-for="tab in tabs"
                                :key="tab.title"
                                :class="{ 'is-active': currentTab === tab.component }">
                                <a @click="currentTab = tab.component">
                                    {{ tab.title }}
                                </a>
                            </li>
                        </ul>
                    </nav>
                </div>
            </div>
        </div>

        <nav class="navbar has-shadow">
            <div class="container">
                <component :is="currentTab"></component>
            </div>
        </nav>

        <section class="section">
            <router-view></router-view>
        </section>

        <app-footer></app-footer>
    </section>
</template>

<script>
    import AppHeader from '../../template/Header'
    import AppFooter from '../../template/Footer'

    import Installation from './installation/InstallationNav'
    import General from './general/GeneralNav'
    import Notices from './notices/NoticesNav'
    import FormElements from './form/FormNav'
    import DataManipulation from './data/DataNav'

    export default {
        components: {
            AppHeader,
            AppFooter
        },
        data() {
            return {
                currentTab: Installation,
                tabs: [
                    {
                        title: 'Installation',
                        component: Installation
                    },
                    {
                        title: 'General',
                        component: General
                    },
                    {
                        title: 'Notices',
                        component: Notices
                    },
                    {
                        title: 'Form',
                        component: FormElements
                    },
                    {
                        title: 'Data',
                        component: DataManipulation
                    }
                ]
            }
        },
        beforeRouteUpdate(to, from, next) {
            this.$refs.header.isMenuActive = false
            this.currentTab = to.meta.category
            next()
        },
        beforeRouteEnter(to, from, next) {
            next(vm => {
                vm.currentTab = to.meta.category
            })
        }
    }
</script>

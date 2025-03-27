<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resources')" :mode="addResButtonMode">Add Resource</base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResources from './AddResources.vue';

export default {
    components: {
        StoredResources,
        AddResources
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official guide to Vue.js',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'The most popular search engine',
                    link: 'https://google.com'
                }
            ]
        }
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.AddResource,
            removeResource: this.removeResource
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab
        },
        AddResource(title , description , url){
            this.storedResources.unshift({
                id: new Date().toISOString(),
                title,
                description,
                link: url
            });
            this.selectedTab = 'stored-resources';
        },
        removeResource(resId){
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        }
    },
    computed:{
        storedResButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat'; 
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resources' ? null : 'flat';
        }
    }
}
</script>
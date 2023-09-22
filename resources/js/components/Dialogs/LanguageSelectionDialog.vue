<template>
    <v-dialog v-model="value" persistent max-width="300px">
        <v-card class="rounded-lg">
            <v-card-title>
                <span class="text-h5">Language</span>
            </v-card-title>
            <v-card-text>
                <v-list rounded>
                    <v-list-item-group color="primary" v-model="selectedLanguage">
                        <v-list-item class="regular-list-height my-1" @click="selectLanguage('japanese')" value="japanese">
                            <v-list-item-avatar tile min-width="60">
                                <v-img class="border" :src="'/images/flags/japanese'" max-width="43" height="28"></v-img> 
                            </v-list-item-avatar>
                            <v-list-item-content>Japanese</v-list-item-content>
                        </v-list-item>
                        <v-list-item class="regular-list-height my-1" @click="selectLanguage('norwegian')" value="norwegian">
                            <v-list-item-avatar tile min-width="60">
                                <v-img class="border" :src="'/images/flags/norwegian'" max-width="43" height="28"></v-img> 
                            </v-list-item-avatar>
                            <v-list-item-content>Norwegian</v-list-item-content>
                        </v-list-item>
                        <v-list-item class="regular-list-height my-1" @click="selectLanguage('german')" value="german">
                            <v-list-item-avatar tile min-width="60">
                                <v-img class="border" :src="'/images/flags/german'" max-width="43" height="28"></v-img> 
                            </v-list-item-avatar>
                            <v-list-item-content>German</v-list-item-content>
                        </v-list-item>
                    </v-list-item-group>
                </v-list>
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn rounded text @click="close">Cancel</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
    export default {
        props: {
            value : Boolean,
        },
        emits: ['input'],
        data: function() {
            return {
                selectedLanguage: 'japanese',
            };
        },
        mounted: function() {
            axios.get('/language/get').then(function (response) {
                this.selectedLanguage = response.data;
            }.bind(this)).catch(function (error) {}).then(function () {});
        },
        methods: {
            selectLanguage: function(newLanguage) {
                this.selectedLanguage = newLanguage;
                axios.get('/language/change/' + this.selectedLanguage).then(function (response) {
                    document.location.href = '/';
                }.bind(this)).catch(function (error) {}).then(() => {
                });
            },
            close: function() {
                this.$emit('input', false);
            }
        }
    }
</script>
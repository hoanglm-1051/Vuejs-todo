<template>
    <div class='ui basic content center aligned segment'>
        <button class="ui basic button icon" @click="openForm()" v-show="!isCreating">
            Create
        </button>
        <div class="ui centered card" v-show="isCreating">
            <div class="content">
                <div class="ui form">
                    <div class="field">
                        <label for="title">Title</label>
                        <input type="text" v-model="titleText" ref="title" defaultvalue="">
                    </div>
                    <div class="field">
                        <label for="project">Project</label>
                        <input type="text" v-model="projectText" ref="project" defaultvalue="">
                    </div>
                    <div class='ui two button attached buttons'>
                        <button class='ui basic blue button' v-on:click="sendForm()">
                            Create
                        </button>
                        <button class='ui basic red button' v-on:click="closeForm()">
                            Cancel
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isCreating: false,
            titleText: '',
            projectText: '',
        }
    },
    methods: {
        openForm() {
            this.isCreating = true;
        },
        closeForm() {
            this.isCreating = false;
        },
        sendForm() {
            if (this.titleText.length > 0 && this.projectText.length > 0) {
                const title = this.titleText;
                const project = this.projectText;

                this.$emit('create-todo', {
                    title,
                    project,
                    done: false
                });

                this.titleText = '';
                this.projectText = '';
                this.isCreating = false;
            }
        },
    },
}
</script>
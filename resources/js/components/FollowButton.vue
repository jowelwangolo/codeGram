<template>
    <button class="btn btn-primary ml-4" @click='followUser' v-text='buttonText'></button>
</template>

<script>
    export default {
        props: ['userId', 'follows'],

        mounted() {
            console.log('Component mounted.')
        },


        data: function() {
            return {
                status: this.follows,
            }
        },

        methods: {
            followUser() {
                axios.post('/follow/' + this.userId)
                    .then((response) => {
                        this.status = !this.status;
                    })
                    .catch(error => {
                        if(error.response.status == '401') {
                            window.location = '/login';
                        }
                    });
            }
        },

        computed: {
            buttonText() {
                return (this.status) ? 'Unfollow' : 'Follow';
            }
        }
    }
</script>

<template>
    <div>
        <div class="container">
            <div id="date">{{getDay}} - {{getDate}}</div>
            <div id="display">{{time}}</div>
            <div id="content">
                <p id="quote">{{quote}} <br/>- {{author}}</p>
            </div>
        </div>
        <div id="b-nav">
            <ul>
                <button @click="newQuote" id="gen">Quote Me !</button>
            </ul>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import moment from 'moment';
    export default {
        data() {
            return {
                quote: '',
                author: '',
                time: ''
            }
        },
        created() {
            setInterval(() => this.updateTime(), 1000);
            this.newQuote();
        },
        methods: {
            updateTime() {
                this.time = moment().format('LTS');
            },
            newQuote(){
                axios.get('https://favqs.com/api/qotd')
                    .then(res => {
                        this.quote = res.data.quote.body;
                        this.author= res.data.quote.author;
                    })
                    .catch(error => console.log(error))
            }
        },
        computed: {
            getDay() {
                return moment().format('dddd');
            },
            getDate() {
                return moment().format('l');
            }
        }
        
    }
</script>

<style scoped>

</style>
<template>
    <div class="hello">
        <div>
            <ul>
                <li>Firstname: {{user.name | capitalize}}</li>
                <br>
                <li>Lastname: {{user.lastname | capitalize}}</li>
                <br>
                <li>Birth date: {{user.birthdate | formatDate | capitalize}}</li>
                <br>
                <li>Age: {{calculatedAge}}</li>
                <br>
                <li>Gender: {{user.gender}}</li>
                <br>
                <li style="white-space: pre-line;">About me: {{user.aboutMe}}</li>
                <br>
            </ul>
        </div>
        <div>
            <input type="text" v-model="user.name" placeholder="Firstname">
        </div>
        <div>
            <input type="text" v-model="user.lastname" placeholder="Lastname">
        </div>
        <div>
            <input type="date" v-model="user.birthdate" placeholder="Birth date">
        </div>
        <div>
            <input type="radio" v-model="user.gender" value="male" id="male"> <label for="male">Male</label>
            <br>
            <input type="radio" v-model="user.gender" value="female" id="female"> <label for="female">Female</label>
        </div>
        <div>
            <textarea v-model="user.aboutMe" placeholder="About me..."></textarea>
        </div>
        <button @click="submit">Submit</button>
        <div>
            <h3 v-for="(item, index) in cities" :key="index">{{item | capitalize}}</h3>
            <button @click="addCity">Add a city</button>
        </div>
    </div>
</template>

<script>
    import capitalize from '../Filters.js'

    export default {
        name: 'HelloWorld',
        data: function () {
            return {
                user: {
                    name: null,
                    lastname: null,
                    birthdate:  null,
                    age: null,
                    gender: null,
                    aboutMe: null,
                },
                myArray: [
                    "tallin",
                    "paris",
                    "london",
                    "helsinki"
                ]
            }
        },
        computed: {
            calculatedAge: function () {
                console.log('I am running')
                if (!this.user.birthdate) return ''
                let birthDate = new Date(this.user.birthdate);
                let currentDate = new Date();

                return currentDate.getFullYear() - birthDate.getFullYear()
            },
            cities: function () {
                let a = this.myArray
                return a.sort()
            }
        },
        methods: {
            submit: function () {
                console.log(this.user)
                // send data to api
            },
            addCity: function () {
               this.myArray.push("tbilisi")
               this.myArray.push("antananarivo")
            }
        },
        filters: {
            capitalize: capitalize,
            formatDate: function (value) {
                if (!value) return ''
                let date = new Date(value);
                let month = date.getMonth();
                let day = date.getDate();
                let year = date.getFullYear();

                let months = [
                    'january',
                    'february',
                    'march',
                    'april',
                    'may',
                    'june',
                    'july',
                    'august',
                    'september',
                    'october',
                    'november',
                    'december'
                ]

                let m = months[month];
                let d =  '';
                if (day == 11 || day == 12 || day == 13) {
                    d = day + 'th'
                }  else {
                    switch (day % 10) {
                        case 1:
                            d = day + 'st'
                            break;
                        case 2:
                            d = day + 'nd'
                            break;
                        case 3:
                            d = day + 'rd'
                            break;
                        default:
                            d = day + 'th'
                    }
                }

                return m + " " + d + ", " + year

            }
        },
        props: {
            msg: String
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>

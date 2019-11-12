<template>
    <div class="weather">
        <table className='table table-striped' align="center">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Date</th>
                    <th>Temp. (C)</th>
                    <th>Temp. (F)</th>
                    <th>Summary</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(forecast,index) in forecasts" :key="forecast.date">
                    <td>{{index+1}}</td>
                    <td>{{forecast.date}}</td>
                    <td>{{forecast.temperatureC}}</td>
                    <td>{{forecast.temperatureF}}</td>
                    <td>{{forecast.summary}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'WeatherForecast',
        data() {
            return {
                forecasts: []
            };
        },
        created() {
            this.axios.get("/weatherforecast").then(res => {
                // console.log(res.data);
                this.forecasts = res.data;
            });
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    .weather {
        margin: 0 auto;
        margin-top: 50px;
    }
</style>

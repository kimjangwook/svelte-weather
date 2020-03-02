<script>
    import { key } from './key.js';
    import { weatherList } from './store.js';

    let customApiKey = '';
    let cityName = '';


    function getFetchUrl(cityName) {
        return 'http://api.openweathermap.org/data/2.5/weather?units=metric&appid=' + (customApiKey || key) + '&q=' +
                cityName ;
    }

    async function addWeatherInfo() {
        const res = await fetch(getFetchUrl(cityName));
        if (res.status === 404) {
            alert('Invalid City Name.');
        } else {
            weatherList.add(await res.json());
        }
        cityName = '';
    }
</script>

<div class="api-key">
    <input type="text" placeholder="Input your API key." bind:value={customApiKey}>
</div>

<div class="search-form">
    <input type="text"
           placeholder="Enter City Name."
           bind:value={cityName}
    />
    <button type="button"
            on:click={addWeatherInfo}
    >ADD</button>
</div>


<style type="text/scss">
    .api-key {
        padding: 1rem 0;
    }
    .search-form {
        padding: 0;
        button {
            padding-left: 20px;
            padding-right: 20px;
            background-color: #f6d55c;
        }
    }

    input[type="text"] {
        width: 50%;
    }
</style>

<script>
const weatherForm = document.querySelector(".location");
const locationInput = document.querySelector(".locationTitle");
const apiKey = "1b8651fdb3ca42d82f15b6ba026e7bd7";


weatherForm.addEventListener("submit", async e => {

    e.preventDefault(); // Prevents the page from reloading
    const city = locationTitle.value;

    if (city){
    
        try{
            const weatherData = await getWeatherData(city);
            displayWeatherData(weatherData);
        }
        catch(error){
            console.error(error);
            errorSpotted(error);
        }
    
    }
    else{
        errorSpotted("Please enter the city");
    }
})


async function getWeatherData(city){
    const apiUrl = `https://api.openweathermap.org/data/2.5/forecast?q=${city}&appid=${apiKey}`;

    const response = await fetch(apiUrl);

    //console.log(response);

    if (!response.ok){
        throw new Error("Couldn't fetch weather data");
    }
    return await response.json();
}

function displayWeatherData(weatherData){

    const {name: city, 
           main: {temp, humidity, feels_like, sea_level},
           weather: [{description, id}],
           wind: {speed}} = weatherData.list[0];


    document.getElementById("currTemp").value = `${(temp - 273.15).toFixed(1)}°C`;
    document.getElementById("feeLik").value = `${(feels_like - 273.15).toFixed(1)}°C`;
    document.getElementById("humid").value = `${humidity}%`;
    document.getElementById("wind").value = `${speed * 3.6} km/h`; //wind default measurement is metres/second
    document.getElementById("precip").value = `${sea_level}%`;
    document.getElementById("emo").value = getWeatherEmoji(id);
    

}

function getWeatherEmoji(weatherID){
    switch(true){
        case(weatherID >= 200 && weatherID <= 232):
            return "⛈️";
        
        case(weatherID >= 300 && weatherID <= 321):
            return "🌦";
        
        case(weatherID >= 500 && weatherID <= 531):
            return "🌧️";
        
        case(weatherID >= 600 && weatherID <= 622):
            return "❄️";
        
        case(weatherID >= 701 && weatherID <= 781):
            return "🌫️";
        
        case(weatherID === 800):
            return "☀️";
        
        case(weatherID >= 801 && weatherID <= 804):
            return "☁️";

        default:
            return "NOTHING";
        
    }
}

function errorSpotted(message){
    console.log(message);
}

</script>
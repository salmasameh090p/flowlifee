const apiKey = "YOUR_API_KEY"; // ← Replace with your OpenWeather API key
const city = "Cairo"; // ← Change to your city or university location

const temp = document.getElementById("temperature");
const condition = document.getElementById("condition");
const humidity = document.getElementById("humidity");
const wind = document.getElementById("wind");
const icon = document.getElementById("icon");
const locationName = document.getElementById("location");
const refreshButton = document.getElementById("refresh");

// Function to fetch real weather data
async function getWeather() {
  try {
    const url = https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric;
    const response = await fetch(url);
    const data = await response.json();

    temp.textContent = ${Math.round(data.main.temp)}°;
    humidity.textContent = ${data.main.humidity}%;
    wind.textContent = ${data.wind.speed} km/h;
    condition.textContent = data.weather[0].description
      .split(" ")
      .map(word => word[0].toUpperCase() + word.slice(1))
      .join(" ");
    icon.src = https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png;
    locationName.textContent = data.name;
  } catch (error) {
    condition.textContent = "Error loading weather";
  }
}

// Load data on page open and on button click
refreshButton.addEventListener("click", getWeather);
getWeather();
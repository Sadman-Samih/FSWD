# Project 3: Weather App — Solution

## File Structure

```
weather-app/
├── weather-index.html
├── weather-style.css
└── weather.js
```

## weather-index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <link rel="stylesheet" href="weather-style.css">
</head>
<body>
  <div class="weather-app">
    <h1>Weather Check</h1>

    <div class="search">
      <input type="text" id="city-input" placeholder="Enter a city..." autofocus>
      <button id="search-btn">Search</button>
    </div>

    <div id="weather-result" class="weather-result hidden">
      <div class="weather-header">
        <h2 id="city-name"></h2>
        <span id="weather-date"></span>
      </div>
      <div class="weather-main">
        <img id="weather-icon" src="" alt="">
        <div class="temperature">
          <span id="temp"></span>
          <span class="unit">°C</span>
        </div>
        <div id="weather-description" class="description"></div>
      </div>
      <div class="weather-details">
        <div class="detail">
          <span class="detail-label">Humidity</span>
          <span id="humidity"></span>
        </div>
        <div class="detail">
          <span class="detail-label">Wind</span>
          <span id="wind"></span>
        </div>
        <div class="detail">
          <span class="detail-label">Feels Like</span>
          <span id="feels-like"></span>
        </div>
      </div>
    </div>

    <div id="error-message" class="error hidden"></div>
  </div>

  <script src="weather.js"></script>
</body>
</html>
```

## weather-style.css

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: linear-gradient(135deg, #1e3c72, #2a5298);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.weather-app {
  background: rgba(255,255,255,0.95);
  border-radius: 20px;
  padding: 40px;
  width: 100%;
  max-width: 450px;
  box-shadow: 0 10px 40px rgba(0,0,0,0.3);
}

h1 {
  text-align: center;
  color: #1e3c72;
  margin-bottom: 25px;
  font-size: 1.8rem;
}

.search {
  display: flex;
  gap: 10px;
  margin-bottom: 25px;
}

.search input {
  flex: 1;
  padding: 14px;
  border: 2px solid #e2e8f0;
  border-radius: 10px;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.2s;
}

.search input:focus {
  border-color: #2a5298;
}

.search button {
  padding: 14px 24px;
  background: #2a5298;
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
}

.search button:hover {
  background: #1e3c72;
}

.weather-result {
  text-align: center;
}

.weather-header {
  margin-bottom: 20px;
}

.weather-header h2 {
  font-size: 1.6rem;
  color: #1a1a1a;
}

.weather-header span {
  color: #666;
  font-size: 0.9rem;
}

.weather-main {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 25px;
}

.weather-main img {
  width: 80px;
  height: 80px;
}

.temperature {
  font-size: 3.5rem;
  font-weight: 700;
  color: #1e3c72;
  display: flex;
  align-items: flex-start;
}

.unit {
  font-size: 1.5rem;
  margin-top: 8px;
}

.description {
  font-size: 1.1rem;
  color: #555;
  text-transform: capitalize;
  margin-top: 5px;
}

.weather-details {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
}

.detail {
  background: #f0f4ff;
  border-radius: 10px;
  padding: 15px 10px;
  text-align: center;
}

.detail-label {
  display: block;
  font-size: 0.8rem;
  color: #888;
  margin-bottom: 5px;
}

.detail span:last-child {
  font-size: 1.1rem;
  font-weight: 600;
  color: #1e3c72;
}

.hidden {
  display: none;
}

.error {
  color: #dc2626;
  text-align: center;
  padding: 15px;
  background: #fee2e2;
  border-radius: 10px;
  margin-top: 15px;
}
```

## weather.js

```javascript
const API_KEY = 'YOUR_API_KEY_HERE';
const API_URL = 'https://api.openweathermap.org/data/2.5/weather';

const cityInput = document.getElementById('city-input');
const searchBtn = document.getElementById('search-btn');
const resultDiv = document.getElementById('weather-result');
const errorDiv = document.getElementById('error-message');

const cityName = document.getElementById('city-name');
const weatherDate = document.getElementById('weather-date');
const weatherIcon = document.getElementById('weather-icon');
const temp = document.getElementById('temp');
const description = document.getElementById('weather-description');
const humidity = document.getElementById('humidity');
const wind = document.getElementById('wind');
const feelsLike = document.getElementById('feels-like');

searchBtn.addEventListener('click', () => {
  const city = cityInput.value.trim();
  if (city) getWeather(city);
});

cityInput.addEventListener('keydown', (e) => {
  if (e.key === 'Enter') {
    const city = cityInput.value.trim();
    if (city) getWeather(city);
  }
});

cityInput.focus();

async function getWeather(city) {
  resultDiv.classList.add('hidden');
  errorDiv.classList.add('hidden');

  try {
    const res = await fetch(
      `${API_URL}?q=${encodeURIComponent(city)}&units=metric&appid=${API_KEY}`
    );

    if (!res.ok) {
      if (res.status === 404) throw new Error(`City "${city}" not found`);
      if (res.status === 401) throw new Error('Invalid API key');
      throw new Error(`Error ${res.status}`);
    }

    const data = await res.json();
    displayWeather(data, city);

  } catch (err) {
    errorDiv.textContent = err.message;
    errorDiv.classList.remove('hidden');
  }
}

function displayWeather(data, city) {
  cityName.textContent = `${data.name}, ${data.sys.country}`;

  const now = new Date();
  weatherDate.textContent = now.toLocaleDateString('en-US', {
    weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'
  });

  temp.textContent = Math.round(data.main.temp);
  description.textContent = data.weather[0].description
    .split(' ')
    .map(word => word[0].toUpperCase() + word.slice(1))
    .join(' ');

  humidity.textContent = `${data.main.humidity}%`;
  wind.textContent = `${Math.round(data.wind.speed)} km/h`;
  feelsLike.textContent = `${Math.round(data.main.feels_like)}°C`;

  weatherIcon.src = `https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
  weatherIcon.alt = data.weather[0].description;

  resultDiv.classList.remove('hidden');
}
```



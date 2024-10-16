<!-- src/components/WeatherApp.vue -->
<template>
    <div class="weather-app">
      <h1>Hava Durumu Uygulaması</h1>
      <div class="input-container">
        <input
          type="text"
          v-model="city"
          placeholder="Şehir ismini girin"
          @keyup.enter="getWeather" 
        />
        <button @click="getWeather">Hava Durumunu Getir</button>
      </div>
      <div>Girdiğiniz Şehir: <span>{{ city }}</span>
      </div>
      <div v-if="weatherData" class="weather-info">
        <h2>{{ weatherData.name }} için hava durumu:</h2>
        <p><strong>Sıcaklık:</strong> {{ weatherData.main.temp }}°C</p>
        <p><strong>Hava Durumu:</strong> {{ weatherData.weather[0].description }}</p>
        <p><strong>Nem:</strong> {{ weatherData.main.humidity }}%</p>
        <p><strong>Rüzgar Hızı:</strong> {{ weatherData.wind.speed }} m/s</p>
      </div>
      
      <div v-if="errorMessage" class="error">{{ errorMessage }}</div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        city: '',
        weatherData: null,
        errorMessage: '',
      };
    },
    methods: {
      async getWeather() {
        const apiKey = '7b5d394d03bdcf47d765d89bee273a11'; // API anahtarını buraya ekle
        if (!this.city) {
          this.errorMessage = 'Lütfen bir şehir girin.';
          return;
        }
        
        this.errorMessage = ''; // Hata mesajını temizle
        try {
          const response = await axios.get(
            `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${apiKey}`
          );
          this.weatherData = response.data; // Hava durumu verilerini kaydet
        } catch (error) {
          this.errorMessage = 'Hava durumu verileri alınamadı. Şehri kontrol edin.';
          this.weatherData = null; // Verileri sıfırla
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .weather-app {
    max-width: 500px;
    margin: 50px auto;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
    background-color: #f9f9f9;
  }
  
  h1 {
    font-size: 24px;
    color: #333;
    margin-bottom: 20px;
  }
  
  .input-container {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  input {
    padding: 10px;
    width: 70%;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-right: 10px;
    font-size: 16px;
  }
  
  button {
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    background-color: #007bff;
    color: white;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  .weather-info {
    margin-top: 20px;
    padding: 10px;
    border: 1px solid #007bff;
    border-radius: 5px;
    background-color: #e9f5ff;
  }
  
  .weather-info h2 {
    margin-bottom: 10px;
    color: #007bff;
  }
  
  .error {
    color: red;
    margin-top: 20px;
  }
  </style>
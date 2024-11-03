	<script>
	import axios from 'axios';

		export default {
			data() {
				return {
					city: "",
					error: '',
					info: null
				}
			},
			computed: {
				cityName() {
					return "'" + this.city + "'"
				},
				showTemp() {
					return "Temperature " + this.info.main.temp
				},
				showFeelsLike() {
					return "Feels like " + this.info.main.feels_like
				},
				showMinTemp() {
				return "Min Temperature " + this.info.main.temp_min
				},
				showMaxTemp() {
					return "Max Temperature " +this.info.main.temp_max
				},
			},
			methods: {
				getWeather() {
					if(this.city.trim().length < 2) {
						this.error = "Need a name more than one symbol"
						return false
					}
					this.error = ''

					axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=016083f48507df6d8fe537d79d82a6b9`)
					.then(res => (this.info = res.data))
				}
			}
		}

	</script>

	<template>
	<div class="wrapper">
		<h1>Weather app</h1>
		<p>Find out the weather in {{ city == "" ? 'your city' : cityName}}</p>
		<input type="text"
		placeholder="Enter city"
		v-model="city" >
		<button v-if="city !== ''" @click="getWeather()">Get the weather</button>
		<button disabled v-else>Enter the name of the city</button>
		<p class="error">{{ error }}</p>

	<div v-if="info != null">
		<p>{{ showTemp }}</p>
		<p>{{ showFeelsLike }}</p>
		<p>{{ showMinTemp }}</p>
		<p>{{ showMaxTemp }}</p>
	</div>
	</div>
	</template>

	<style scoped>
	.error {
		color: black;
	}
	.wrapper {
		width: 800px;
		height: 500px;
		border-radius:50px;
		background:purple;
		text-align: center;
		color: #fff;
	}
	.wrapper h1 {
		margin-top: 50px;
	}
	.wrapper p {
		margin-top: 20px;
	}
	.wrapper input {
		margin-top: 30px;
		background: transparent;
		border: 0;
		border-bottom: 2px solid #333;
		color: #fcfcfc;
		font-size: 14px;
		padding: 5px 8px;
		outline: none;
	}
	.wrapper input:hover {
		transform:scale(1.02) ;
	}
	.wrapper input:focus {
		border-bottom-color:black ;
	}
	.wrapper button {
		background: #3bc; 
		color: #fff;
		border-radius: 10px;
		border: 2px solid #3bc4;
		padding: 10px 15px;
		margin-left: 20px;
		cursor: pointer;
		transition: transform 500ms ease;
	}
	.wrapper button:disabled {
		background: #3bc;
		cursor: not-allowed;
	}
	.wrapper button:hover {
		transform: scale(1.05) translateY(-5px);
	}
	</style>

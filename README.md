# WeatherApp
Weather details according to location.


Building a Weather App with Angular 16 and OpenWeather API


Prerequisites:
Node.js and NPM: Make sure you have Node.js installed on your machine, as it comes bundled with NPM (Node Package Manager). You can download Node.js from the official website (https://nodejs.org).
Angular CLI: Install the Angular CLI globally by running the following command in your terminal
npm install -g @angular/cli
 
Step 1: Set up a new Angular project
To start building our weather app, let’s create a new Angular project using the Angular CLI. Open your terminal and run the following command: 
ng new weather-app

This command will generate a new Angular project with the name “weather-app” and set up the necessary files and dependencies.
 
Step 2: Set up the OpenWeather API
To fetch weather data, we will use the OpenWeather API. Visit the OpenWeather website (https://openweathermap.org) and sign up for a free account. Once registered, obtain an API key, which will be required for making API requests.
 
Step 3: Create a weather service
In Angular, services are used to encapsulate logic and handle data retrieval. We will create a weather service to interact with the OpenWeather API. Run the following command in your terminal to generate the service:
ng generate service weather

This command will create a new service file named “weather.service.ts” in the “app” folder. Open the file and replace its contents with the following code:

import { Injectable } from ‘@angular/core’;
import { HttpClient } from ‘@angular/common/http’;

@Injectable({
providedIn: ‘root’
})
export class WeatherService {
private apiKey = ‘YOUR_API_KEY’; // Replace with your OpenWeather API key

constructor(private http: HttpClient) { }

getWeather(city: string) {
const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${this.apiKey}`;
return this.http.get(apiUrl);
}
}

 

Make sure to replace 'YOUR_API_KEY' with the API key you obtained from the OpenWeather website.

Step 4: Create a weather component Components in Angular are responsible for rendering the user interface. Let’s create a weather component that will display the weather information. Run the following command in your terminal to generate the component:

ng generate component weather

This command will create a new component file named “weather.component.ts” in the “app” folder. Open the file and replace its contents with the following code:

 
import { Component, OnInit } from ‘@angular/core’;
import { WeatherService } from ‘../weather.service’;

@Component({
selector: ‘app-weather’,
templateUrl: ‘./weather.component.html’,
styleUrls: [‘./weather.component.css’]
})
export class WeatherComponent implements OnInit {
city = ”;
weatherData: any;

constructor(private weatherService: WeatherService) { }

ngOnInit(): void {
}

getWeather() {
this.weatherService.getWeather(this.city).subscribe((data: any) => {
this.weatherData = data;
});
}
}

Step 5: Display weather data in the template Open the “weather.component.html” file and replace its contents with the following code:

<h2>Weather App</h2>

<div>
<input type=”text” [(ngModel)]=”city” placeholder=”Enter city name”>
<button (click)=”getWeather()”>Get Weather</button>
</div>

<div *ngIf=”weatherData”>
<h3>{{ weatherData.name }}</h3>
<p>Temperature: {{ weatherData.main.temp }}°C</p>
<p>Weather: {{ weatherData.weather[0].main }}</p>
</div>

Step 6: Update the app component Open the “app.component.html” file and replace its contents with the following code:

<app-weather></app-weather>

Step 7: Start the development server Finally, run the following command in your terminal to start the development server and view the weather app in your browser:

ng serve        ✔

Navigate to http://localhost:4200/ in your browser, and you should see the Weather App with an input field to enter the city name. After entering the city name and clicking the “Get Weather” button, the app will fetch the weather data from the OpenWeather API and display it on the screen.

 Congratulations finally you run your application😊

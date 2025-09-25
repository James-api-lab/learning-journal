# learning-journal

Week 1 - Day 1 
Learning the basics of APIs
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}

Week 1 - Day 2

✅ Day 2 Log: I can use Postman to send a GET request and see the JSON response.

built a working Morning Brief generator in Python.
Pulls Seattle weather (Open-Meteo API)
Fetches top Seattle + world headlines (NewsAPI)
Uses OpenAI to generate a short banking/markets summary
Formats everything into an HTML email
Sends it automatically via SendGrid with an API (delivers to spam right now)
This is my first end-to-end workflow: local script → multiple external APIs → AI summary → email delivery.

Week 1 - Day 3 - Learn the Anatomy of an API

1. URL (endpoint - where I am sending the request
   today's example is : https://api.chucknorris.io/jokes/random
3. Method - what i am doing
   -GET (read),
   -POST (create),
   -PUT (update),
   -DELETE (delete)
4. Headers - information
   -Example: X-Api-Key: <yourkey>
5. Body - the data I send with the request
   -Example: JSON like { "city": "Seattle" }

I used Postman to set a GET request
URL: https://api.chucknorris.io/jokes/random

The response:
{
    "categories": [],
    "created_at": "2020-01-05 13:42:28.664997",
    "icon_url": "https://api.chucknorris.io/img/avatar/chuck-norris.png",
    "id": "99B90SWoSAOZiX2Gl_Kp9w",
    "updated_at": "2020-01-05 13:42:28.664997",
    "url": "https://api.chucknorris.io/jokes/99B90SWoSAOZiX2Gl_Kp9w",
    "value": "Chuck Norris doesn't have to say NO to drugs.....They don't ask"
}

Day 3 continue - Expanding the API categories

Turn:
https://api.chucknorris.io/jokes/random
into:
https://api.chucknorris.io/jokes/random?category=dev

{
    "categories": [
        "dev"
    ],
    "created_at": "2020-01-05 13:42:19.324003",
    "icon_url": "https://api.chucknorris.io/img/avatar/chuck-norris.png",
    "id": "poqerqlpqz2en3hacikbjw",
    "updated_at": "2020-01-05 13:42:19.324003",
    "url": "https://api.chucknorris.io/jokes/poqerqlpqz2en3hacikbjw",
    "value": "Chuck Norris doesn't use reflection, reflection asks politely for his help."
}

I explored the categories with:
https://api.chucknorris.io/jokes/categories

Response:
[
    "animal",
    "career",
    "celebrity",
    "dev",
    "explicit",
    "fashion",
    "food",
    "history",
    "money",
    "movie",
    "music",
    "political",
    "religion",
    "science",
    "sport",
    "travel"
]

There is a difference here that I did not know. 
The original response is an object ( { .... } )

The category call is an array

✅ Day 3 Practice Log:
- I used query parameters (?category=...) to filter jokes.
- I saw the difference between JSON objects ({ }) and arrays ([ ]).
- I triggered an error (wrong category) and learned how APIs respond with status codes.


📅 Day 4 — Weather API Setup

https://home.openweathermap.org/

Using my API key i called in browser

[{"id":804,"main":"Clouds","description":"overcast clouds","icon":"04n"}],"base":"stations","main":{"temp":8.87,"feels_like":7.15,"temp_min":8.87,"temp_max":8.87,"pressure":1025,"humidity":78,"sea_level":1025,"grnd_level":1021},"visibility":10000,"wind":{"speed":3.01,"deg":13,"gust":9.06},"clouds":{"all":94},"dt":1758771375,"sys":{"country":"GB","sunrise":1758779487,"sunset":1758822772},"timezone":3600,"id":2643743,"name":"London","cod":200}

In Postman I updated the call to Seattle

{
    "coord": {
        "lon": -122.3321,
        "lat": 47.6062
    },
    "weather": [
        {
            "id": 800,
            "main": "Clear",
            "description": "clear sky",
            "icon": "01n"
        }
    ],
    "base": "stations",
    "main": {
        "temp": 16.18,
        "feels_like": 15.73,
        "temp_min": 16.18,
        "temp_max": 16.18,
        "pressure": 1017,
        "humidity": 72,
        "sea_level": 1017,
        "grnd_level": 1008
    },
    "visibility": 10000,
    "wind": {
        "speed": 2.06,
        "deg": 11,
        "gust": 3.9
    },
    "clouds": {
        "all": 0
    },
    "dt": 1758771548,
    "sys": {
        "country": "US",
        "sunrise": 1758722351,
        "sunset": 1758765794
    },
    "timezone": -25200,
    "id": 5809844,
    "name": "Seattle",
    "cod": 200
}

📅 Day 4 Expanded — Weather API Deep Dive 🌤️

Updating the call 
 City = Seattle
 Unites = Imperial
 
{"coord":{"lon":-122.3321,"lat":47.6062},"weather":[{"id":800,"main":"Clear","description":"clear sky","icon":"01n"}],"base":"stations","main":{"temp":61.12,"feels_like":60.31,"temp_min":61.12,"temp_max":61.12,"pressure":1017,"humidity":72,"sea_level":1017,"grnd_level":1008},"visibility":10000,"wind":{"speed":4.61,"deg":11,"gust":8.72},"clouds":{"all":0},"dt":1758771258,"sys":{"country":"US","sunrise":1758722351,"sunset":1758765794},"timezone":-25200,"id":5809844,"name":"Seattle","cod":200}


In a room filled with errors:

200 OK → success
401 Unauthorized → bad key
404 Not Found → bad city

✅ Day 4 Log: I used my first real API key to pull live weather from OpenWeather.  
I also learned how query parameters (q, units, appid) change results.  
I tested errors (bad city, bad key).  
Backup: I can also fetch forecasts using Open-Meteo with latitude/longitude.


📅 Day 5 — Weather API Variations
Goal: Learn how query parameters change API responses.
1. Changing cities
2. Chaining Params with &
   - &lang=es didnt seem to work
3. Changing the mode=XML
This XML file does not appear to have any style information associated with it. The document tree is shown below.
<current>
<city id="5809844" name="Seattle">
<coord lon="-122.3321" lat="47.6062"/>
<country>US</country>
<timezone>-25200</timezone>
<sun rise="2025-09-24T13:59:11" set="2025-09-25T02:03:14"/>
</city>
<temperature value="60.73" min="60.73" max="60.73" unit="fahrenheit"/>
<feels_like value="60.12" unit="fahrenheit"/>
<humidity value="77" unit="%"/>
<pressure value="1017" unit="hPa"/>
<wind>
<speed value="4.61" unit="mph" name="Light breeze"/>
<gusts value="8.72"/>
<direction value="11" code="N" name="North"/>
</wind>
<clouds value="0" name="clear sky"/>
<visibility value="10000"/>
<precipitation mode="no"/>
<weather number="800" value="cielo claro" icon="01n"/>
<lastupdate value="2025-09-25T04:05:09"/>
</current>


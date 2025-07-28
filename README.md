import requests

def get_weather(city):
    api_key = "e61519db46724aeafa7d94f56a3dafc5"
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
    try:
        response = requests.get(url)
        data = response.json()
        if data["cod"] != 200:            return None
        weather = {
            "City": city.title(),
        "Temperature": f"{data['main']['temp']} °C",
       "Description": data["weather"][0]["description"].title(),
            "Humidity": f"{data['main']['humidity']}%"
        }
        return weather
    except:
        return None

def save_to_file(weather):
    with open("weather_report.txt", "w") as file:
        for key, value in weather.items():
            file.write(f"{key}: {value}\n")

def main():
    while True:
        print("\n1. Get Weather\n2. Exit")
        choice = input("Choose option: ")
        if choice == "1":
            city = input("Enter city name: ")
            weather = get_weather(city)
            if weather:
                for key, value in weather.items():
                    print(f"{key}: {value}")
                if input("Save to file? (y/n): ").lower() == "y":
                    save_to_file(weather)
                    print("Saved to weather_report.txt")
            else:
                print("Error: City not found or API issue.")
        elif choice == "2":
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
1# day-21
python learning

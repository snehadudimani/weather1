import requests

# OpenWeatherMap API URL
api_url = "https://samples.openweathermap.org/data/2.5/forecast/hourly?q=London,us&appid=b6907d289e10d714a6e88b30761fae22"

def get_weather_data():
    response = requests.get(api_url)
    if response.status_code == 200:
        data = response.json()
        return data
    else:
        print("Failed to fetch weather data. Please try again later.")
        return None

def print_weather(data):
    for item in data['list']:
        dt_txt = item['dt_txt']
        weather_desc = item['weather'][0]['description']
        print(f"{dt_txt}: {weather_desc}")

def print_wind_speed(data):
    for item in data['list']:
        dt_txt = item['dt_txt']
        wind_speed = item['wind']['speed']
        print(f"{dt_txt}: Wind Speed - {wind_speed} m/s")

def print_pressure(data):
    for item in data['list']:
        dt_txt = item['dt_txt']
        pressure = item['main']['pressure']
        print(f"{dt_txt}: Pressure - {pressure} hPa")

def main():
    data = get_weather_data()

    if data:
        while True:
            print("\nChoose an option:")
            print("1. Get weather")
            print("2. Get Wind Speed")
            print("3. Get Pressure")
            print("0. Exit")
            option = input("Enter your choice: ")

            if option == '1':
                print_weather(data)
            elif option == '2':
                print_wind_speed(data)
            elif option == '3':
                print_pressure(data)
            elif option == '0':
                print("Exiting...")
                break
            else:
                print("Invalid option. Please choose again.")

if __name__ == "__main__":
    main()

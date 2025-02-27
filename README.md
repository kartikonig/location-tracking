# location-tracking
import requests

# Your IPinfo token
ipinfo_token = '57557a539fe104'
# Your ipstack token
ipstack_token = 'YOUR_IPSTACK_TOKEN'  # Replace with your actual ipstack token

# Function to get the user's IP address
def get_user_ip():
    response = requests.get('https://api.ipify.org?format=json')
    if response.status_code == 200:
        return response.json()['ip']
    else:
        raise Exception('Failed to retrieve user IP address')

# Function to get geolocation data from IPinfo
def get_ipinfo_data(ip):
    url = f'https://ipinfo.io/{ip}?token={ipinfo_token}'
    response = requests.get(url)
    if response.status_code == 200:
        return response.json()
    else:
        return None

# Function to get geolocation data from ipstack
def get_ipstack_data(ip):
    url = f'http://api.ipstack.com/{ip}?access_key={ipstack_token}'
    response = requests.get(url)
    if response.status_code == 200:
        return response.json()
    else:
        return None

# Get the user's IP address
user_ip = get_user_ip()

# Get geolocation data from IPinfo
ipinfo_data = get_ipinfo_data(user_ip)
if ipinfo_data:
    print("IPinfo Data:", ipinfo_data)
else:
    print("Failed to retrieve IPinfo data")

# Get geolocation data from ipstack
ipstack_data = get_ipstack_data(user_ip)
if ipstack_data:
    print("ipstack Data:", ipstack_data)
else:
    print("Failed to retrieve ipstack data")

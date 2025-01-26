
## Habit Tracker

This Python script allows you to track daily habits, specifically cycling distance in kilometers, using the Pixela API. The script lets you:

- ** Create a Pixela user account.**

- **Create a graph for tracking cycling habits.**

- **Add daily entries to the graph.**

- **Update existing entries.**

- **Delete entries from the graph.**

## Prerequisites

Before running the script, ensure you have the following:

Python 3 installed on your system.

The requests library installed. You can install it using:

bash `` pip install requests``

A Pixela account. This script will automatically create one if it doesn't exist.

## Setup

Clone or download the script:
Download this script to your local machine.

Set up your Pixela credentials:
Open the script and modify the following variables:

USERNAME = "your_username"
TOKEN = "your_secure_token"
GRAPH_ID = "your_graph_id"

Replace your_username with your desired Pixela username.

Replace your_secure_token with a unique, secure token.

Replace your_graph_id with an identifier for your graph (e.g., graph1).

Run the script:
Execute the script in your terminal or IDE:

python habit_tracker.py

## Features

1. Create a Pixela User Account

The script will send a POST request to the Pixela API to create a new user account using the specified USERNAME and TOKEN.

2. Create a Graph

The script defines a graph (e.g., for cycling habits) using the following parameters:

id: Unique graph ID.

name: Name of the graph (e.g., "Cycling Graph").

unit: Unit of measurement (e.g., kilometers).

type: Data type (e.g., float).

color: Graph color (e.g., ajisai).

3. Add Daily Entries

The script prompts you to input the distance cycled and sends a POST request to add this entry to your graph.

4. Update Entries

If you need to modify an entry, the script provides an option to update the data for a specific date.

5. Delete Entries

The script allows you to delete entries for a specific date from the graph.

Code Overview

Here is the complete Python script for the Habit Tracker:

import requests
from datetime import datetime

USERNAME = "your_username"
TOKEN = "your_secure_token"
GRAPH_ID = "your_graph_id"

pixela_endpoint = "https://pixe.la/v1/users"

user_params = {
    "token": TOKEN,
    "username": USERNAME,
    "agreeTermsOfService": "yes",
    "notMinor": "yes",
}

# ## POST: Create User
# response = requests.post(url=pixela_endpoint, json=user_params)
# print(response.text)

graph_endpoint = f"{pixela_endpoint}/{USERNAME}/graphs"

graph_config = {
    "id": GRAPH_ID,
    "name": "Cycling Graph",
    "unit": "Km",
    "type": "float",
    "color": "ajisai"
}

headers = {
    "X-USER-TOKEN": TOKEN
}

# ## POST: Create Graph
# response = requests.post(url=graph_endpoint, json=graph_config, headers=headers)
# print(response.text)

pixel_creation_endpoint = f"{pixela_endpoint}/{USERNAME}/graphs/{GRAPH_ID}"

today = datetime.now()
# print(today.strftime("%Y%m%d"))

pixel_data = {
    "date": today.strftime("%Y%m%d"),
    "quantity": input("How many kilometers did you cycle today? "),
}

response = requests.post(url=pixel_creation_endpoint, json=pixel_data, headers=headers)
print(response.text)

update_endpoint = f"{pixela_endpoint}/{USERNAME}/graphs/{GRAPH_ID}/{today.strftime('%Y%m%d')}"

new_pixel_data = {
    "quantity": input("How many kilometers did you cycle today? "),
}

## PUT: Update Entry
# response = requests.put(url=update_endpoint, json=new_pixel_data, headers=headers)
# print(response.text)

delete_endpoint = f"{pixela_endpoint}/{USERNAME}/graphs/{GRAPH_ID}/{today.strftime('%Y%m%d')}"

## DELETE: Delete Entry
# response = requests.delete(url=delete_endpoint, headers=headers)
# print(response.text)

Example Usage

Input your daily cycling distance when prompted:

How many kilometers did you cycle today? 5.2

View the response to confirm the entry was added:

{"message":"Success.","isSuccess":true}

Notes

The TOKEN must remain private to ensure the security of your Pixela account.

Customize the graph settings and endpoints as needed for other habits.

References

Pixela API Documentation

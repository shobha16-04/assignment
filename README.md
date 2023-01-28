# assignment 
Write a program to GET random data of an user and write it in a File named users.csv. Each GET request must have an interval time of 1 second and append the information in a comma separated format. You can use any open source mock rest api endpoints available on the internet or use Random Data API (https://random-data-api.com/documentation.
#Solution
This program will use the requests library to make a GET request to the https://randomuser.me/api/ website, which returns a JSON object containing random user information. The program then uses the csv library to write the user information to a file called 'users.csv' in a comma-separated format. The program uses a while loop to make the GET request every 1 second and append the new user information to the 'users.csv' file.
#Code
import csv
import time
import requests

def get_random_user():
    url = 'https://randomuser.me/api/'
    response = requests.get(url)
    return response.json()['results'][0]

def write_user_to_csv(user):
    with open('users.csv', 'a', newline='') as file:
        fieldnames = user.keys()
        writer = csv.DictWriter(file, fieldnames=fieldnames)

        if file.tell() == 0:
            writer.writeheader()
        
        writer.writerow(user)

while True:
    user = get_random_user()
    write_user_to_csv(user)
    time.sleep(1)

A. Write a program to read users.csv and create users-sorted.csv by applying sorting algorithm on firstName / Name / Username.
#Solution:=>  This program reads a csv file called 'users.csv' and creates a new csv file called 'users-sorted.csv' that is sorted based on the specified column ('firstName', 'Name', or 'UsersName'). The program uses the csv module to read and write the files, and the sorted() function to sort the users based on the specified column.
#code
import csv

def sort_users(file_name, sort_by):
    with open(file_name, 'r') as file:
        csv_reader = csv.DictReader(file)
        users = list(csv_reader)
    
    sorted_users = sorted(users, key=lambda x: x[sort_by])

    with open('users-sorted.csv', 'w', newline='') as file:
        fieldnames = sorted_users[0].keys()
        writer = csv.DictWriter(file, fieldnames=fieldnames)
        writer.writeheader()
        for user in sorted_users:
            writer.writerow(user)

sort_users('users.csv', 'firstName')
# or
# sort_users('users.csv', 'Name')
# or
# sort_users('users.csv', 'UsersName')

B. Write a program to Input Id or Username of an user and return the details of that user in the output of the program
#Solution:=> This program takes an input of user id or username from the user, then it reads the 'users.csv' file and searches for the user with the matching id or username. If a match is found, it returns the details of that user, otherwise it returns a message that no user was found with the specified id or username.

It uses the csv module to read the CSV file and it uses the DictReader to read the CSV as a dictionary, so that you can access the value of any column by its key name.
#Code
import csv

def get_user_by_id(user_id):
    with open('users.csv', 'r') as file:
        csv_reader = csv.DictReader(file)
        for user in csv_reader:
            if user['id']['value'] == user_id or user['username'] == user_id:
                return user
    return None

user_id = input("Enter user id or username: ")
user = get_user_by_id(user_id)

if user:
    print(user)
else:
    print(f"No user found with id/username: {user_id}")

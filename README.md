# assignment 
Write a program to GET random data of an user and write it in a File named users.csv. Each GET request must have an interval time of 1 second and append the information in a comma separated format. You can use any open source mock rest api endpoints available on the internet or use Random Data API (https://random-data-api.com/documentation.
#Solution
This program will use the requests library to make a GET request to the https://randomuser.me/api/ website, which returns a JSON object containing random user information. The program then uses the csv library to write the user information to a file called 'users.csv' in a comma-separated format. The program uses a while loop to make the GET request every 1 second and append the new user information to the 'users.csv' file.

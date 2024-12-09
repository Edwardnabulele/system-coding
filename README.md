import os
import socket
import requests
from datetime import date, datetime

# Function to display the menu
def show_menu():
    print("\nMenu:")
    print("1. Show current date and time")
    print("2. Backup webpage")
    print("3. Show IP address")
    print("4. Show home directory")
    print("5. Quit")

# Function to back up a webpage
def backup_webpage():
    try:
        url = input("Please enter your full URL webpage: ")

        response = requests.get(url)

        if response.status_code == 200:
            print(f"Successfully fetched the webpage: {url}")

            # Correct the string replacement part
            filename = url.replace("file:///H:/", "").replace("/", "_")  # This will clean up the URL to make it a valid filename.

            with open(filename, 'w', encoding='utf-8') as file:
                file.write(response.text)
            print(f"Webpage saved successfully as '{filename}'")
        else:
            print(f"Failed to fetch the webpage. HTTP Status code: {response.status_code}")
    
    except requests.exceptions.RequestException as e:
        print(f"An error occurred while trying to fetch the webpage: {e}")

# Main function that runs the program
def main():
    while True:
        show_menu()  # Display the menu
        
        choice = input("\nEnter your choice (1-5): ")
        
        if choice == "1":
            # Display current date and time
            my_date_today = date.today()
            print(f"Today's date is: {my_date_today}")
            my_datetime = datetime.now()
            print(f"Current date and time: {my_datetime}")
        
        elif choice == "2":
            backup_webpage()  # Call the function to back up a webpage
        
        elif choice == "3":
            # Show IP address
            hostname = socket.gethostname()
            myip = socket.gethostbyname(hostname)
            print("My IP address is: " + myip)
        
        elif choice == "4":
            # Show home directory
            homeDirectory = os.path.expanduser("~")
            print(f"Your home directory is: {homeDirectory}")
        
        elif choice == "5":
            print("Exiting program. Goodbye!")
            break  # Exit the loop and quit the program
        
        else:
            print("Invalid choice. Please enter a number between 1 and 5.")

# Call the main function to start the program
if __name__ == "__main__":
    main()

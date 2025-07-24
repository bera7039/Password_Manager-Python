# Password_Manager-Python
import json
import os

#function to save password
def save_password(website,username,password):
    data={
        website:{
            "username": username,
            "password":password
        }
    }
    #check if the json file exists and read it
    if os.path.exist("password.json"):
        with open("password.json","r") as file:
            try:
                existing_data=json.load(file)
            except json.JSONDecodeError:
                existing_data={}
    else:
        existing_data={}
    #update a date with new entry
    existing_data.update(data)
    
#write updated data to the JSON file
    with open("password.json","w") as file:
       json.dump(existing_data,file,indent=4)

    print("password successfully")
#function to retrieve password
def get_password(website):
    if not os.path.exist("password.json"):
        print("No password saved yet")
        return
        
    with open("password.json","r")as file:
        data=json.load(file)
      
    if website in data:
        print(f"\n website: {website}")
        print(f" username: {data[website]['username']}")
        print(f" password: {data[website]['password']}")
    else:
        print("No password found for this website")
#main menu
def main():
    while True:
          print("\n=== Password manager===")
          print("1. save a new password")
          print("2. retrieve a password")
          print("3.exit")

          choice=input("Enter your choice:")

          if choice == "1":
             website=input("Enter your website:")
             username=input("Enter the username/email:")
             password=input("Enter password:")
            
          elif choice == "2":
              website = input("Enter website name to retrieve: ")
              get_password(website)

          elif choice == "3":
            print("Exiting Password Manager. Stay safe!")
            break

          else:
            print("Invalid choice. Please enter 1, 2, or 3.")
#start the app
main()

                

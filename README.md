User Automation Script
Step 1. Setting Up:

The script defines locations for log and password files (LOGFILE and PASSWORD_FILE).
It checks if an input file is provided as a command-line argument. If not, it shows an error message and exits.
It creates the log and password files if they don't exist. Sets access permissions for the password file to be only readable and writable by the script itself (highly secure).

2. Generating Random Passwords:

This part defines a function named generate_random_password.
It takes an optional argument for password length (defaults to 10 characters).
The function uses special commands to generate a random string of characters containing uppercase and lowercase letters, numbers, and special symbols.

3. Creating a User:

This part defines a function named create_user. It takes username and group information as arguments.
It checks if the user already exists using getent passwd. If the user exists, a message is logged.
If the user doesn't exist, it creates the user using useradd and sets up a home directory (-m flag). Success is logged.
It converts the comma-separated groups string into an array for processing individual groups.
It iterates through each group in the array.
If the group doesn't exist, it creates the group using groupadd and logs the creation.
It adds the user to the group using usermod -aG. Success is logged.
The script sets up permissions for the user's home directory (read, write, and execute only for the user).
It generates a random password using the generate_random_password function with a length of 12 characters.
The script sets the user's password using chpasswd and stores the username and password pair in the password file (PASSWORD_FILE). Success is logged.

4. Processing the Input File:

The script reads the input file line by line.
Each line is expected to be in the format "username;groups" (separated by semicolon).
For each line, it extracts the username and groups using read with a delimiter of semicolon.
It calls the create_user function with the extracted username and groups to create the user with specified groups.

5. Finishing Up:

After processing the entire input file, the script logs a message indicating successful completion of the user creation process.
This script essentially automates user creation based on an input file, taking care of password generation, group management, and logging all actions for audit purposes.

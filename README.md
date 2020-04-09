# Python_Task2

import string
import random


def get_user_info():
    first_name = input("Enter your first name below: \n")
    last_name = input("Enter your last name below: \n")
    email = input("Enter your email address below: \n")

    info = [first_name, last_name, email]

    return info


def gen_password(info):
    characters = string.ascii_letters
    length = 5
    random_password = ''.join(random.choice(characters) for p in range(length))

    password = str(info[0][0:2] + info[1][-2:] + random_password)

    return password


status = True
directory = []

users = {}
user_count = 1

while status:
    info = get_user_info()
    password = gen_password(info)
    print(f"Suggested password: {password}")

    password_like = input("Do you like the suggested password? If yes, enter Y; if no, enter N and provide password: ")

    password_loop = True

    while password_loop:
        if password_like.upper() == 'Y':
            info.append(password)
            directory.append(info)
            break
        else:
            user_password = input("Enter password with at least 7 characters \n")

            password_len = True

            while password_len:

                if len(user_password) >= 7:
                    info.append(user_password)
                    directory.append(info)
                    users[user_count] = info

                    password_len = False

                    password_loop = False


                else:
                    print("Your password is too short")
                    user_password = input("Enter password with at least 7 characters ")

    new_user = input("Do you want to add a new user? Y or N: ")
    if new_user.upper() == 'N':
        status = False
        for item in directory:
            print(item)
    else:
        status = True
        user_count += 1

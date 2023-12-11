import os

inventory = {
    
    "Fried Chicken with Rice": 10,
    "Spaghetti": 20,
    "Fries": 15,
    "Chocolate Ice Cream": 30,
    "Burger": 25

}

is_discounted = False
order = []

def cls():
    os.system('cls' if os.name=='nt' else 'clear')

def welcome():
    print("Welcome to Sherly's Fast Food!")
    print()

def customer_ready():
    print("Ready to place your order? [Y/N]")
    print("")

    user_response = input("Type 'Y' if you're ready or 'N' to exit: ")
    print("")

    if user_response == 'Y' or user_response == 'y':
        print("Great! Let's get started with your order.")
        print("")
        cls()
    elif user_response == 'N' or user_response == 'n':
        print("No problem! Feel free to return when you're ready to order.")
        print("")
        customer_ready()
    else:
        print("Invalid response. Please type 'Y' if you're ready or 'N' to exit.")
        print("")
        customer_ready()

def ask_discount():
    global is_discounted
    is_discounted = False
    discount = input("Are you a Senior Citizen or PWD? Type [Y] for yes and [N] for no: ")
    print()

    if discount == 'Y' or discount == 'y':
        is_discounted = True
        print("Great! We will put a 20 percent discount on your order. Here in Sherly's, we care for you!")
        print("")
    elif discount == 'N' or discount == 'n':
        print("No problem! We will proceed without a discount.")
        print("")
    else:
        print("Invalid response. Please type 'Y' for yes or 'N' for no.")
        print("")
        ask_discount()

def show_menu():
    print("Menu:")
    print("")
    print("[1] Fried Chicken with Rice for Php 110.00")
    print("[2] Spaghetti for Php 50.00")
    print("[3] Fries for Php 50.00")
    print("[4] Chocolate Ice Cream for Php 30.00")
    print("[5] Burger for Php 45.00")
    print("")
    print("[6] Clear Order")
    print("[7] Show Order")
    print("[8] Edit Order")
    print("[0] Exit")
    print("")

def choose_menu():
    try:
        ch = int(input("Enter the number of the item you want to order: "))
        if ch >= 1 and ch <= 5:
            quantity = int(input("How many would you like to order? "))
        
        if ch == 1:
            item = "Fried Chicken with Rice"

            if inventory[item] > 0 and inventory[item] >= quantity:
                order.append([quantity, item, 110.00])
                inventory[item] -= quantity
            else:
                print("")
                print(f"{item} the desired quantity is not fully available. The remaining quantity is {inventory[item]}.")

        elif ch == 2:
            item = "Spaghetti"
            if inventory[item] > 0 and inventory[item] >= quantity:
                order.append([quantity, item, 50.00])
                inventory[item] -= quantity
            else:
                print("")
                print(f"{item} the desired quantity is not fully available. The remaining quantity is {inventory[item]}.")

        elif ch == 3:
            item = "Fries"
            if inventory[item] > 0 and inventory[item] >= quantity:
                order.append([quantity, item, 50.00])
                inventory[item] -= quantity
            else:
                print("")
                print(f"{item} the desired quantity is not fully available. The remaining quantity is {inventory[item]}.")

        elif ch == 4:
            item = "Chocolate Ice Cream"
            if inventory[item] > 0 and inventory[item] >= quantity:
                order.append([quantity, item, 30.00])
                inventory[item] -= quantity
            else:
                print("")
                print(f"{item} the desired quantity is not fully available. The remaining quantity is {inventory[item]}.")

        elif ch == 5:
            item = "Burger"
            if inventory[item] > 0 and inventory[item] >= quantity:
                order.append([quantity, item, 25.00])
                inventory[item] -= quantity
            else:
                print("")
                print(f"{item} the desired quantity is not fully available. The remaining quantity is {inventory[item]}.")

        elif ch == 6:
            order.clear()
            print("Your order has been cleared. You can start a new one.")
        elif ch == 7:
            sh_orders()
        elif ch == 8:
            ed_order()
        elif ch == 0:
            print("Thank you for ordering at Sherly's! Please come again!")
            exit()
        elif ch == 121212:
            admin_panel()
        else:
            print("Invalid response. Please enter a number from 0 to 7.")
            print("")
    except ValueError:
        print("Invalid input. Please enter a number.")
        print("")

def main():
    welcome()
    customer_ready()
    cls()
    ask_discount()
    cls()

    while True:
        show_menu()
        choose_menu()
        print("")

        while True:
            user_response = input("Would you like to make another action? [Y] if yes / [N] to proceed requesting an official receipt: ")
            print("")

            if user_response.lower() == 'y':
                break
            elif user_response.lower() == 'n':
                receipt()
                return
            else:
                print("Invalid response. Please type 'Y' or 'N'.")
                print("")

    receipt()

def receipt():
    total = 0
    subtotal = 0
    shcounter = 1

    cls()
    print("               SHERLY'S FAST FOOD               \n")
    print()
    print(" ---------------OFFICIAL RECEIPT---------------\n")
    print("Order Summary:\n")
    print("Quantity ---- Item ---- Price")

    for item in order:
        print(f"[{shcounter}] {item[0]} ---- {item[1]} ----- Php {item[2] * item[0]}")
        subtotal += item[2] * item[0]
        shcounter += 1
        print("")

    print(f"Subtotal: Php {subtotal}")

    if is_discounted:
        discount_text = "SC/PWD Discount - 20%"
        print(f"{discount_text}: (Php - {subtotal * 0.20})")
        total = subtotal * 0.80
        print(f"Total: Php {total}")
    else:
        total = subtotal
        print(f"Total: Php {total}")

    print("")
    print("Thank you for ordering at Sherly's! Please come again!")

def compute_discount(total):
    global is_discounted    
    if is_discounted:
        total *= (1 - .20)
    return total

def exit_program():
    cls()
    print("Thank you for ordering at Sherly's! Plese come again!")
    customer_ready()
    main()

def sh_orders():
    total = 0
    subtotal = 0
    shcounter = 1

    cls()
    print("        -------- CURRENT ORDER --------        \n")

    for item in order:
        print(f"[{shcounter}] {item[0]} ---- {item[1]} ----- Php {item[2] * item[0]}")
        subtotal += item[2] * item[0]
        shcounter += 1
        print("")

    print(f"Subtotal: Php {subtotal}")

    if is_discounted:
        discount_text = "SC/PWD Discount - 20%"
        print(f"{discount_text}: (Php - {subtotal * 0.20})")
        total = subtotal * 0.80
        print(f"Total: Php {total}")
    else:
        total = subtotal
        print(f"Total: Php {total}")

    print("")
    print("Confirm order? [Y/N]")
    print("")

    while True:
        user_response = input("Type 'Y' to confirm and request a receipt or 'N' to resume ordering: ")
        print("")

        if user_response.lower() == 'y':
            cls()
            receipt()
            break  # Exit the loop after confirming the order
        elif user_response.lower() == 'n':
            print("Going back to ordering.")
            print("")
            show_menu()
            break  # Exit the loop after resuming ordering
        else:
            print("Invalid response. Please type 'Y' or 'N'.")
            print("")

def ed_order():
    total = 0
    subtotal = 0
    shcounter = 1

    counter = 1
    ur1counter = 1
    ur2counter = 1
    ur3counter = 1
    
    cls()
    print("        -------- EDIT ORDER --------        \n")
    print("")

    for item in order:
        print(f"[{shcounter}] {item[0]} ---- {item[1]} ----- Php {item[2] * item[0]}")
        subtotal += item[2] * item[0]
        shcounter += 1
        print("")

    print(f"Subtotal: Php {subtotal}")

    if is_discounted:
        discount_text = "SC/PWD Discount - 20%"
        print(f"{discount_text}: (Php - {subtotal * 0.20})")
        total = subtotal * 0.80
        print(f"Total: Php {total}")
    else:
        total = subtotal
        print(f"Total: Php {total}")
    
    print("")
    print("What would you like to do?")
    print("[1] Remove Quantity")
    print("[2] Add Quantity")
    print("[3] Remove Item")
    print("[4] Exit")
    print("")

    user_response = input("Enter the number of the action you want to do: ")
    if user_response == '1':
        print("Which item would you like to modify?")
        print("")
        for item in order:
            print(f"[{ur1counter}] {item[0]} ---- {item[1]} ----- Php {item[2] * item[0]}")
            subtotal += item[2] * item[0]
            ur1counter += 1
        print("")
        try:
            removeresponse = int(input("Enter the number of the item you want to modify: "))
            print("")
            quantity = int(input("Enter the quantity of the item you want to remove: "))
            ordercount = len(order)

            if removeresponse <= ordercount:
                order[removeresponse-1][0] -= quantity
                if order[removeresponse-1][0] <= 0:
                    order.pop(removeresponse-1)
            else:
                print(f"Invalid response. Please enter a number from 1 to {ordercount}.")
                print("")
            ed_order()
        except ValueError:
            print("Invalid input. Please enter a number.")
            print("")
            ed_order()

    elif user_response == '2':
        print("Which item would you like to modify?")
        print("")
        for item in order:
            print(f"[{ur2counter}] {item[0]} ---- {item[1]} ----- Php {item[2] * item[0]}")
            subtotal += item[2] * item[0]
            ur2counter += 1

        print("")
        try:
            removeresponse = int(input("Enter the number of the item you want to modify: "))
            print("")
            quantity = int(input("Enter the quantity of the item you want to add: "))
            ordercount = len(order)

            if removeresponse <= ordercount:
                order[removeresponse-1][0] += quantity
                if order[removeresponse-1][0] <= 0:
                    order.pop(removeresponse-1)
            else:
                print(f"Invalid response. Please enter a number from 1 to {ordercount}.")
                print("")
            ed_order()
        except ValueError:
            print("Invalid input. Please enter a number.")
            print("")
            ed_order()
    
    elif user_response == '3':
        print("Which item would you like to remove?")
        print("")
        for item in order:
            print(f"[{ur3counter}] {item[0]} ---- {item[1]} ----- Php {item[2] * item[0]}")
            subtotal += item[2] * item[0]
            ur3counter += 1

        print("")
        try:
            removeresponse = int(input("Enter the number of the item you want to remove: "))
            print("")
            ordercount = len(order)

            if removeresponse <= ordercount:
                order.pop(removeresponse-1)
            else:
                print(f"Invalid response. Please enter a number from 1 to {ordercount}.")
                print("")
            ed_order()
        except ValueError:
            print("Invalid input. Please enter a number.")
            print("")
            ed_order()

    elif user_response == '4':
        show_menu()
    else:
        print("Invalid response. Please enter a number from 1 to 3.")
        print("")
        ed_order()

def admin_panel():
    cls()

    while True:
        print("Admin Panel:")
        print("")
        print("[1] View Inventory")
        print("[2] Add Quantity to Inventory")
        print("[3] Remove Quantity from Inventory")
        print("[4] Exit Admin Panel")
        print("")

        admin_choice = input("Enter your choice: ")

        if admin_choice == '1':
            print("Current Inventory:")
            for item, quantity in inventory.items():
                print(f"{item}: {quantity}")
            print("")
        elif admin_choice == '2':
            item_to_add = input("Enter the name of the item to add quantity: ")
            if item_to_add in inventory:
                add_quantity = int(input("Enter the quantity to add: "))
                inventory[item_to_add] += add_quantity
                print(f"{add_quantity} {item_to_add}(s) added to the inventory.\n")
            else:
                print(f"{item_to_add} not found in the inventory.\n")
        elif admin_choice == '3':
            item_to_remove = input("Enter the name of the item to remove quantity: ")
            if item_to_remove in inventory:
                remove_quantity = int(input("Enter the quantity to remove: "))
                if remove_quantity >= inventory[item_to_remove]:
                    del inventory[item_to_remove]
                else:
                    inventory[item_to_remove] -= remove_quantity
                print(f"{remove_quantity} {item_to_remove}(s) removed from the inventory.\n")
            else:
                print(f"{item_to_remove} not found in the inventory.\n")
        elif admin_choice == '4':
            break
        else:
            print("Invalid choice. Please enter a number from 1 to 4.\n")


main()


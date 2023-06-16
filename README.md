admin_keys = {"samchandu": "samchandu@1819"}
inven = {1: {'ItemName': 'Tandoori Chicken', 'FoodID': 1, 'Quantity': '100ml,250ml,4pieces', 'Price': 240, 'Stock': 14, 'Discount': '20%'},
        2: {'ItemName': 'Vegan Burger', 'FoodID': 2, 'Quantity': '1 Piece', 'Price': 320, 'Stock': 14, 'Discount': '40%'},
        3: {'ItemName': 'Truffle Cake', 'FoodID': 3, 'Quantity': '500gm', 'Price': 900, 'Stock': 14, 'Discount': '30%'}}
#nested dict
def add_new_item():
    itemname = input("Enter the Item name: ")
    foodid = int(input("Enter the item id: "))
    quantity = input("Enter the Quantity Value of item: ")
    price = int(input("Enter the price of the item: "))
    stock = int(input("Enter the stock value of item: "))
    dis_count = input("Enter the discount value: ")

    inven[itemid] = {
        "ItemName": itemname,
        "FoodID": foodid,
        "Quantity": quantity,
        "Price": price,
        "Stock": stock,
        "Discount": dis_count
    }
    print("The Item"+itemname+ "is successfully added")
    return inven


def edit_from_item():
    item = int(input("Enter the itemid which you want to edit: "))
    a = input("Enter the item name")
    b = int(input("Enter the price of item"))
    d = int(input("Enter the stock of the item"))
    e = input("Enter the quantity of the item")
    f = input("Enter the discount value: ")
    inven[item]["ItemName"] = a
    inven[item]["Price"] = b
    inven[item]["Stock"] = d
    inven[item]["Quantity"] = e
    inven[item]["Discount"] = f
    print("*****Edited item successfully*****")
    return inven

def show_inven():
    print("*****The list item should as follows:*****")
    for i in inven:
        print(inven[i]["FoodID"],'.',end=" ")
        print(inven[i]["ItemName"],end=" ")
        print('(',inven[i]["Quantity"],')',end=" ")
        print("INR", inven[i]["Price"],)
        print("Discount", inven[i]["Discount"])




def remove_item():
    d = int(input("Enter the Item id which you want to exit"))
    inven.pop(d)
    print("Remove item successfully ")
    return inven
import admin as ad
from user import User

uhh = User(str, str, str, str, str)

inp = int(input("Where You want to login select 1.Admin and 2.User and 3.Exit"))
if inp == 1:
    Username = input("Enter the username of admin: ")
    Password = input("Enter the password of admin: ")
    if aa.admin_keys[Username] == Password:
        print("*****You're successfully logged inn*****")
        admin_crawler = True
        while admin_crawler:
            adm_choice = int(input("Choose the options of admin panel 1.ADD NEW ITEM 2.EDIT ITEM 3.VIEW INVENTORY 4.REMOVE ITEM 5.EXIT"))
            if adm_choice == 1:
                aa.add_new_item()
            elif adm_choice == 2:
                aa.edit_from_item()
            elif adm_choice == 3:
                aa.show_inven()
            elif adm_choice == 4:
                aa.remove_item()
            elif adm_choice == 5:
                print(f"You're Exit to the admin panel{Username}")
                admin_crawler = False
            else:
                print("This is the wrong selection please select valid option")
    else:
        print("These are the wrong credentials! SORRY!!!")
elif inp == 2:
    print("Welcome to the user panel")
    username = input("Enter the username here: ")
    password = input("Enter the password here: ")
    if User.login(username, password):
        print(f"You are logged in successfully {username}")
        user_crawler = True
        while user_crawler:
            usr_choice = int(input(f"{username}, Enter the option 1.Place new order 2.Order history 3.Exit"))
            if usr_choice == 1:
                uhh.place_order()
            elif usr_choice == 2:
                print(f"Here is your order history, {username}")
                print(uhh.order_history)
            elif usr_choice == 3:
                user_crawler = False
                print("You're Successfully looged out")
            else:
                print("You choose the invalid option")
    else:
        print("These are the wrong credentials! SORRY!!!")
else:
    exit()

import admin as ad

#a=User(,,,,)#
#b=User(,,,)
#after a -login_info={"a":'a'}
#after b -login_info={"a":'a','b':'b'}

class User:
    login_info = {"samchandu": "samchandu@1819"}

    def __init__(self, name, phoneno, email, address, password):
        self.name = name
        self.number = phoneno
        self.email = email
        self.address = address
        self.password = password
        User.login_info[self.name] = self.password
        self.profile={"Name":name}
        self.order_history = {}

    @classmethod
    def login(cls, username, password):
        if cls.login_info.get(username) == password:
            print("You're are successfully logged in.....")
            return True
        else:
            print("SORRY! These are the Wrong Credentials")
            return False


    def place_order(self):
        print("What you want to order here in the Inventory")
        print(ad.show_inven())
        user_choice = int(input("If you want to order then select 1.YES 2.NO"))
        if user_choice == 1:
            n=int(input("Enter how many items do you want to Order"))
            x=0
            for i in range(n):

             itemid = int(input("Enter the Item id here: "))
             quan = int(input("Enter the quantity of the item: "))
             x += ad.inven[itemid]["Price"] * quan
            again_ask = input("Are you still want to order this Enter YES or NO")
            if again_ask == "YES":
                print(f'''Your item name is {ad.inven[itemid]["ItemName"]}''')
                print(f'''Price of your Item is {ad.inven[itemid]["Price"]}''')
                print(f"This is your quantity {quan}")
                print(f"It costs you {x}INR in total")
                print("You're all set for this order")
                self.order_history[itemid] = {
                    "Item Name": ad.inven[itemid]["ItemName"],
                    "Price": ad.inven[itemid]["Price"],
                    "Quantity": quan
                }
                final_stock = ad.inven[itemid]["Stock"] - quan
                ad.inven[itemid]["Stock"] = final_stock
                print("You're order is successfully placed")

            elif again_ask == "NO":
                print("This Order is cancelled!! You can look once more")
            else:
                print("Invalid choice")
        elif user_choice == 2:
            print("You select 2 option so we cancelled this")
        else:
            print("Enter the invalid choice")


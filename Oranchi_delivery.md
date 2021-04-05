# Unit3 project: Oranchi online delivery system

Table of Contents:

  1. [Planning (Criteria A)](https://github.com/kazuto-abe/Unit3/blob/main/Oranchi_delivery.md#criteria-a--planning)
  2. [Design (Criteria B)](https://github.com/kazuto-abe/Unit3/blob/main/Oranchi_delivery.md#criateria-b--design)
  3. [Development (Criteria C)](https://github.com/kazuto-abe/Unit3/blob/main/Oranchi_delivery.md#criteria-c--development)
  4. [Functionality (Criteria D)](https://github.com/kazuto-abe/Unit3/blob/main/Oranchi_delivery.md#criteria-d--functionality)
  5. [Evaluation (Criteria E)](https://github.com/kazuto-abe/Unit3/blob/main/Oranchi_delivery.md#criteria-e--evaluation)
  6. [Citation ](https://github.com/kazuto-abe/Unit3/blob/main/Oranchi_delivery.md#citation)
  
## Criteria A : Planning

### Context of the problem
  My customer, Caleb whom is my roommate, needs online delivery service for the local restaurant called "Oranchi-Syokudo". He currently goes to the restaurant on foot or by taking taxi, however that has been making him concerned since it approximately takes 40 minutes by walk from ISAK. Although he occationally grabs the cab for the shortcut, it for sure costs a lot (about 3000 yen for the round trip). An additional issue that my customer's been confronting is that he needs to find some native Japanese speakers to communicate with waiter - in particular when he'd like to reserve a couple of seats in advance. My target-user, therefore, wants an online service which encourages him to spend more money and plenty of time on meals rather than transportation so that he might be more inclined to confortably order Oranchi's dinner on campus.


### Proposed solution
  In order to address significant issues he has, my proposed solution is to build online delivery platform for the restaurant by using python and its unique module called kivy, which is an opensource multi-platform GUI development library. This library generally allows us to rapidly make prototypes with user-friendly instractions and design. This online platform has been introduced login/sign up function that easily organize each individual's account, which is basically done by SQL database. All user information, therefore, could be stored from the user text-input using SQL. Moreover, well-structured order page that is linked to one's user account is fully avairable for customers so that no one will be confused. Once they have done with ordering meals, the page redirects to the another page that shows total price of their meals and expected delivery date.

### TELOS study (feasibility report)

**Technical Feasiblity** - Is the project techincally possible?

As mentioned previously, this product is simply created by python which works on any sort of environment like computer so I would say techinal requirements are not high. 

**Economical Feasiblity** - Can the project be afforded? Will it increase profit?

Since all expencses through the app develoment are fully covered by UWC ISAK Japan, this project is feasible finanicially.
Futher, all process are done by our own computer with Pycharm so all essential item are prepared in advance.

**Legal Feasiblity** - Is the project legal?

This product is completly done in a legal way, so it indeed won't be problematic in the future. Moreover, this project should not be copy-righted since it will not be established for third-parties whom are outside of the school .

**Operational Feasiblity** - How will the current operation support the change?

As I mentioned, this product is mainly designed by python and kivy so that we, all developers and testers, readily maintain or modify our program on our own. Also the program is coded on computer but will be displayed on a phone for customers.

**Schedule Feasiblity** - Can the project be done in time?

All coding development and documentation are supporsed to be done by April 1st, which is pretty feasible since we are given approximately 3 weeks in order to polish evething from the beginning.

### Success criteria

1. The product contains login/sign up page.
2. All user/order information are safely stored.
3. Total price will be automatically calculated and shown on user's digital receipt.

### Sketches of the idea

![CamScanner 03-30-2021 22 24_1](https://user-images.githubusercontent.com/60457723/112996353-10a8dc80-91a7-11eb-9873-b9befb24bb4b.jpg)
Figure 1: A rough skech of the application platform which simplifies each components; login/register page, order page and bill page that shows user's receipt which includes total price of meals.

## Criateria B : Design
### System diagram

![systemdiagram_unit3 001](https://user-images.githubusercontent.com/60457723/113005679-a6486a00-91af-11eb-8f38-5f646730a376.jpeg)
Figure 2: A system diagram shows the flow of the program. All inputs are entered by users, and execute them using python and database and finally output some details on a digital receipt. This is done by UI interface designed by Kivy.

### UML diagram

![Screen Shot 2021-03-30 at 21 45 27](https://user-images.githubusercontent.com/60457723/112990690-4b0f7b00-91a1-11eb-8578-c38fe71539dd.png)<br>
Figure 3: A UML diagram that shows the relationship between User table and Order_input table, and each table contains variables with the particular data type (string or integer). Also it shows a couple of function names indicate what to execute throughout the program. 

### ER diagram

![Screen Shot 2021-03-30 at 21 56 28](https://user-images.githubusercontent.com/60457723/112992071-cf163280-91a2-11eb-89d7-c788976f3c07.png)
Figure 4: A ER diagram shows that each entities has several properties, which closely links to another table. In addition, it indicates primary key (id) and foreing key (user_id) that correspond to the user input which is stored in the database.


## Criteria C : Development

#### Main.py (python file)
```.py
#import all python modules and libraries at the beggining
from kivymd.app import MDApp
from kivymd.uix.label import MDLabel
from kivy.uix.behaviors import ButtonBehavior
from kivymd.uix.screen import MDScreen
import sqlite3
import hashlib, binascii, os


# class for the homescreen
class HomeScreen(MDScreen):
    #this function will instantly be running once user entered into the homescreen
    def on_enter(self, *args):
        # it shows welcome message with one's username
        self.ids.welcome_msg.text = f"Welcome to the order page, {LoginScreen.current_user_username} !"

    #this function will be excuted when user pushed the "order" button
    def try_order(self):
        #each properties are named here
        #all properties come from the user input
        menu = self.ids.menu_input.text
        quantity = self.ids.quantity_input.text
        address = self.ids.address_input.text
        phone = self.ids.phone_input.text
        current_user = LoginScreen.current_user

        if not current_user:
            # this happens if current user is None
            return "error"
        #connect to the database
        conn = sqlite3.connect('user.db')
        cur = conn.cursor()
        # return the error message if a user puts wrong name
        if not (menu == "karaage" or menu == "sashimi" or menu == "tenpura" or menu == "curry"):
            print("please put the name correctly")

        else:
            # insert all user inputs into the user table
            sql_order = f"insert into my_Order (my_menu, quantity, address, phone, user_id) values ('{menu}', '{quantity}', '{address}', '{phone}', '{current_user}');"
            cur.execute(sql_order)
            # execute sql
            conn.commit()
            conn.close()
            #precondition of the total price of menu inputs
            sum_price = 0

            if menu == "karaage":
                #this calculates the individual price with taxes
                karaage_price = 900 * int(quantity) * 1.08
                sum_price += karaage_price
                print(karaage_price)
            elif menu == "sashimi":
                sashimi_price = int(1200 * int(quantity) * 1.08)
                sum_price += sashimi_price
                print(sashimi_price)
            elif menu == "tenpura":
                tenpura_price = int(800 * int(quantity) * 1.08)
                sum_price += tenpura_price
                print(tenpura_price)
            elif menu == "curry":
                curry_price = int(850 * int(quantity) * 1.08)
                sum_price += curry_price
                print(curry_price)

            # redirect to the user's receipt screen
            HomeScreen.sum_price= sum_price
            self.parent.current = "BillScreen"




# class for the register screen
class RegisterScreen(MDScreen):


    def try_register(self):
        username = self.ids.username_input.text
        email = self.ids.email_input.text
        psw = self.ids.password_input.text
        # it requires them to enter passwords again
        psw_check = self.ids.password_check.text

        print(psw_check)
        # if password does not match with the previous input, it shows a message
        if psw != psw_check:
            print("passwords do not match")
        else:
            conn = sqlite3.connect('user.db')
            sql = "select * from User where email ='{email}';"
            cur = conn.cursor()
            cur.execute(sql)
            result = cur.fetchone()
            # it shows a message if an email is already created
            if result:
                print("Email is already exist/")
            else:
                sql = f"insert into User(email, password, username) values ('{email}', '{psw}', '{username}');"
                cur = conn.cursor()
                cur.execute(sql)
                print("User account is now created")
                conn.commit()
                conn.close()
                """Hash a password for storing."""
                salt = hashlib.sha256(os.urandom(60)).hexdigest().encode(
                    'ascii')  # hashing a random sequence with 60 bits: produces 256 bits or 64 hex chars
                pwdhash = hashlib.pbkdf2_hmac('sha256', psw.encode('utf-8'),
                                              salt, 100000)
                pwdhash = binascii.hexlify(
                    pwdhash)  # hashing the password with the salt producing 256 bits or 64 hex chars
                return (salt + pwdhash).decode('ascii')  # total length is 128 chars or 512 bits
                print(salt + pwdhash)





class ButtonLabel(ButtonBehavior, MDLabel):
    pass

# class for the login screen
class LoginScreen(MDScreen):
    current_user = None
    #current_user = {'id':1, 'name': "test", email:"example"}

    def verify_password(stored_password, provided_password):
        """Verify a stored password against one provided by user"""
        salt = stored_password[:64]
        stored_password = stored_password[64:]
        pwdhash = hashlib.pbkdf2_hmac('sha256',
                                      provided_password.encode('utf-8'),
                                      salt.encode('ascii'),
                                      100000)
        pwdhash = binascii.hexlify(pwdhash).decode('ascii')
        return pwdhash == stored_password
    # this will be done when user pushed the login button. This corresponds to main.kv;
    def try_login(self):
        email = self.ids.email_input.text
        psw = self.ids.password_input.text
        print(email, psw)

        conn = sqlite3.connect('user.db')
        sql = f"select * from User where password =  '{psw}' and email = '{email}'"
        cur = conn.cursor()
        cur.execute(sql)
        result = cur.fetchone()
        # result = cur.fetchall()
        print(result)
        conn.close()
        if result:
            id, username, password, email, registered_at = result
            print(f"login successful for user with id {id}")
            # it redirects to the home screen once user information are varified.
            self.parent.current = "HomeScreen"
            LoginScreen.current_user = id
            LoginScreen.current_user_username = username

            return result
        else:
            # show a message if user is not created yet
            print("User does not exist")

#class for the bill screen
class BillScreen(MDScreen):
    # once a page is redirected from order page, user will see the total price of meal.
    # this changes according to user's menu inputs
    def on_enter(self, *args):
        self.ids.total_price.text = f"Total price (including tax):  {HomeScreen.sum_price} !"

class MainApp(MDApp):
    def build(self):
        self.theme_cls.primary_palette = "Brown"

        return


MainApp().run()

```

#### Main.kv (kivy file)
```.py
ScreenManager:
    id: scr_manager
    #Here is to manage all screens with their names. Program will be excuted in order.
    LoginScreen:
        name: "LoginScreen"
    RegisterScreen:
        name: "RegisterScreen"
    HomeScreen:
        name: "HomeScreen"
    BillScreen:
        name:"BillScreen"

# This is a screen for the user receipt
<BillScreen>:
    # size of the entire screen
    BoxLayout:
        orientation: 'vertical'
        size: root.height, root.width

    # set the background image
    FitImage:
        source: "izakaya.jpeg"

    MDCard:
        size_hint: 0.8, 0.8
        elevation: 10
        pos_hint: {"center_x":.5, "center_y": 0.5}
        #determine whether a card is vertical or horizontal
        orientation: "vertical"

        BoxLayout:
            orientation: 'vertical'
            size_hint: 0.8, 0.5
            pos_hint: {"center_x": 0.5}

            #this is just for the line which visualizes the box layout
            #canvas.before:
                #Color:
                    #rgba: .5, .5, .5, 1
                #Line:
                    #width:2
                    #rectangle: self.x, self.y, self.width, self.height

            MDLabel:
                text: "Thanks for ordering !!"
                font_style: "H4"
                halign: "center"
            MDLabel:
                # each id connects to the main.py
                id: total_price
                #text: "Total price (including tax): "
                font_style: "H6"
                halign: "center"
            MDLabel:
                id: expected_date
                text: "Expected time: in 90 mins! "
                font_style: "H6"
                halign: "center"

            Image:
                source:'receipt.png'



#this is a screen for the register
<RegisterScreen>:
    BoxLayout:
        orientation: 'vertical'
        size: root.height, root.width

    FitImage:
        source: "izakaya.jpeg"

    MDCard:
        size_hint: 0.4, 0.6
        elevation: 10
        pos_hint: {"center_x":.5, "center_y": 0.5}
        orientation: "vertical"
        # by particulaly setting rgb color, the background color of MDCard changes to what I want it to be.
        # last parameter, 0.6, is to change its opacity
        md_bg_color:[255/255, 255/255, 255/255, 0.6]


        MDBoxLayout:
            id: content #id or name
            adaptive_height: True
            orientation: "vertical"
            padding: 50, 0
            MDLabel:
                text: "Sign up"
                font_style: "H6"
                halign: "center"

            #user input, type: text
            MDTextField:
                id: username_input
                hint_text: "Username"
                icon_left: "username"
                helper_text: "Invalid email"
                helper_text_mode: "on_error"
                required: True

            MDTextField:
                id: email_input
                hint_text: "Email"
                icon_left: "email"
                helper_text: "Invalid email"
                helper_text_mode: "on_error"
                required: True

            MDTextField:
                id: password_input
                hint_text: "password"
                icon_right: "eye-off"
                helper_text: "Invalid password"
                helper_text_mode: "on_error"
                #make this section mandatory
                required: True
                password: True

            MDTextField:
                id: password_check
                hint_text: "Re-enter password"
                icon_right: "eye-off"
                helper_text: "Invalid password"
                helper_text_mode: "on_error"
                required: True
                password: True


            MDRaisedButton:
                text: "Register"
                on_release:
                    #it executes try_register and goes to login screen at the same time once the button is pushed
                    root.try_register()
                    root.parent.current = "LoginScreen"





            MDBoxLayout:
                adaptive_height: True

<HomeScreen>:
    MDBoxLayout:
        orientation: 'vertical'
        size: root.height, root.width

    FitImage:
        source: "izakaya.jpeg"

    MDCard:
        size_hint: 0.8, 0.8
        elevation: 10
        pos_hint: {"center_x":.5, "center_y": 0.5}
        orientation: "vertical"
        md_bg_color:[255/255, 255/255, 255/255, 0.6]


        MDBoxLayout:
            orientation: "horizontal"

            MDBoxLayout:
                id: tenpura #id or name
                adaptive_height: True
                orientation: "vertical"
                size_hint: 0.4, 0.6
                pos_hint: {"x":0, "y":0.2}

                Image:
                    source: "tempra.png"
                    allow_stretch: True
                    center_x: self.parent.center_x
                    center_y: self.parent.center_y

                MDLabel:
                    text: "tenpura: ¥800"
                    halign: "center"




            MDBoxLayout:
                id: sashimi #id or name
                adaptive_height: True
                orientation: "vertical"
                size_hint: 0.4, 0.6
                pos_hint: {"x":0, "y":0.2}

                Image:
                    source: "sashimi.png"
                    allow_stretch: True
                    center_x: self.parent.center_x
                    center_y: self.parent.center_y
                MDLabel:
                    text: "sashimi: ¥1200"
                    halign: "center"



            MDBoxLayout:
                id: karaage #id or name
                adaptive_height: True
                orientation: "vertical"
                size_hint: 0.4, 0.6
                pos_hint: {"x":0, "y":0.2}

                Image:
                    source: "karaage.png"
                    allow_stretch: True
                    center_x: self.parent.center_x
                    center_y: self.parent.center_y
                MDLabel:
                    text: "karaage: ¥900"
                    halign: "center"



            MDBoxLayout:
                id: karaage #id or name
                adaptive_height: True
                orientation: "vertical"
                size_hint: 0.4, 0.6
                pos_hint: {"x":0, "y":0.2}

                Image:
                    source: "curry.png"
                    allow_stretch: True
                    center_x: self.parent.center_x
                    center_y: self.parent.center_y
                MDLabel:
                    text: "curry: ¥850"
                    halign: "center"



        MDBoxLayout:
            id: content #id or name
            adaptive_height: True
            orientation: "vertical"
            padding: 200,0

            MDLabel:
                id: welcome_msg
                text: "welcome"
                font_style: "H6"
                halign: "center"

            MDTextField:
                id: menu_input
                hint_text: "Menu"
                icon_left: "menu"
                helper_text_mode: "on_error"
                required: True

            MDTextField:
                id: quantity_input
                hint_text: "Quantity"
                icon_left: "quantity"
                helper_text_mode: "on_error"
                required: True

            MDTextField:
                id: address_input
                hint_text: "Address"
                icon_left: "address"
                helper_text_mode: "on_error"
                required: True

            MDTextField:
                id: phone_input
                hint_text: "Phone number"
                icon_left: "phone number"

            MDRaisedButton:
                text: "Order"
                halign: "center"

                on_release:
                    root.try_order()

            MDBoxLayout:
                adaptive_height: True
                ButtonLabel:
                    text: "Use another account"
                    halign: "right"
                    on_press:
                        print("here")
                        root.parent.current = "LoginScreen"
```

#### The code for the two database, which are excuted on the console
```.sql
create table my_Order(
    id integer primary key autoincrement not null,
    my_menu    varchar(50),
    quantity    integer varchar(3),
    address     varchar(50),
    phone   varchar(15),
    user_id integer,
    foreign key (user_id) references User(id)
);

create table User(
    id integer primary key autoincrement not null,
    username varchar (30),
    email varchar (30),
    password varchar (20),
    registered_at TIMESTAMP DEFAULT (datetime(CURRENT_TIMESTAMP,'localtime'))
);
```

![Screen Shot 2021-04-05 at 22 51 08](https://user-images.githubusercontent.com/60457723/113581134-b1910f00-9661-11eb-8dbe-f9da6ef7b97f.png)<br>
Figure5: ble database for users.


![Screen Shot 2021-04-05 at 22 51 01](https://user-images.githubusercontent.com/60457723/113581176-c1a8ee80-9661-11eb-825b-e5202f76d726.png)<br>
Figure6: able database for order information, which link to the user table (it connects by the foreign key called user_id).


## Criteria D : Functionality

Below is my functionality video↓
Video will be uploaded soon!

## Criteria E : Evaluation

### Alpha testing

|          Testing<br>phase          |                  Testing<br>section                  |                                  Success criteria                                 |                                                                                                                                                                                                              Procedure                                                                                                                                                                                                             | met?:  |
|:----------------------------------:|:----------------------------------------------------:|:---------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:------:|
| Unit testing                       | Register system for users<br>- error message         | The product contains login/sign up page                                           | Press the "register" button on the login page<br>=> the page redirects to the register screen<br>=> fill your username, email, password, and non-matching password (User-input)<br>=> see the text stating "passwords do not match" on the python console.(output)                                                                                                                                                                 | Yes    |
| Unit testing                       | Register system for users                            | The product contains login/sign up page                                           | Press the "register" button on the login page<br>=> the page redirects to the register screen<br>=> fill your username, email, password, and "matching" password (User-input)<br>=> press the register button at the buttom<br>=> see the message saying "User account is now created!"<br>=> all information will be sent to the user-database without an error message, then redirects to the login page (Registration is done). | Yes    |
| Unit testing                       | Login system for users<br>- error message            | The product contains login/sign up page                                           | Fill the random non-matching user information (username, password) which is not registered yet into the text boxes (User-input).<br>=> push the login button<br>=> see the message saying "User does not exist" on the python console. (output)                                                                                                                                                                                    | Yes    |
| Unit testing                       | Login system for users                               | The product contains login/sign up page                                           | Fill the matching user information which is already registered on the sign up page (User-input)<br>=> push the login button<br>=> see the stating "Login successful for user"(output)<br>=> it redirects to the main menu page for ordering meals.                                                                                                                                                                                 | Yes    |
| Unit testing                       | Order page for users<br>- displays username          | All user/order information are safely stored                                      | Once you logged into your account, you will see the username that you have entered.<br>It says "Welcome to the order page, [your username]" on the main screen as a title.                                                                                                                                                                                                                                                         | Yes    |
| Unit testing                       | Order page for users<br>- switch to another account  | All user/order information are safely stored                                      | Push the "Use another account" button at the right bottom corner (User-input)<br>=> see the message saying "logged out" on Pycharm console. (output)<br>=> it redirects to the login page                                                                                                                                                                                                                                          | Yes    |
| Unit testing                       | Order page for users<br>- error message              | All user/order information are safely stored                                      | Fill the menu-input which is not shown on a menu, quantity, address, and phone number.(User-input)<br>=> press the brown order button<br>=> see the waring stating "Please put a name correctly" on the python console.(Output)                                                                                                                                                                                                    | Yes    |
| Unit testing                       | Order page for users                                 | All user/order information are safely stored                                      | Fill the menu-input correctly, quantity, address, and phone number.(User-input)<br>=> press the order button<br>=> it redirects to the user-bill page (output)                                                                                                                                                                                                                                                                     | Yes    |
| Unit testing                       | User-bill page that shows receipts.<br>- Labels      | Total price will be automatically calculated and shown on user's digital receipt. | Once you have ordered meals, the order info is transferred to another database.<br>=> you see the all labels on the bill page (thanks message, total price, expected date and image).                                                                                                                                                                                                                                              | Yes    |
| Unit testing                       | User-bill page that shows receipts.<br>- Calculation | Total price will be automatically calculated and shown on user's digital receipt. | Total price will be correctly changed according to the user's input + taxes (0.8%, in this case).<br>=> it shows on a screen properly.                                                                                                                                                                                                                                                                                             | Yes    |
| Unit testing                       | GUI (Labels)                                         |                                                                                   | All labels, button-label, title are precisely labelled and clearly showing its meaning.                                                                                                                                                                                                                                                                                                                                            | Yes    |
| Unit testing                       | GUI (Buttons)                                        |                                                                                   | All buttons are capable to redirect to one particular page, and are pretty much user-friendly.(position, color, etc...)                                                                                                                                                                                                                                                                                                            | Yes    |
| Integration check<br>+ Code review | The program works perfectly,                         |                                                                                   | All program is working without any bugs and technical issues.                                                                                                                                                                                                                                                                                                                                                                      | Yes    |
| Code review                        | Comment                                              |                                                                                   | In the program, it neatly explains how each lines works.                                                                                                                                                                                                                                                                                                                                                                           | Yes    |
| Code review                        | Variable names                                       |                                                                                   | All variable names are readily understood, and make sense to everyone.                                                                                                                                                                                                                                                                                                                                                             | Yes    |
| Software check                     | Final check                                          |                                                                                   | All the success criteria are being met.                                                                                                                                                                                                                                                                                                                                                                                            | Yes    |
|                                    |                                                      |                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                    |        |

### Beta testing

### Limitation

### Further improvements



## Citation

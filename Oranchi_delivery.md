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

![Screen Shot 2021-03-30 at 21 45 27](https://user-images.githubusercontent.com/60457723/112990690-4b0f7b00-91a1-11eb-8578-c38fe71539dd.png)
Figure 3: A UML diagram that shows the relationship between User table and Order_input table, and each table contains variables with the particular data type (string or integer). Also it shows a couple of function names indicate what to execute throughout the program.

### ER diagram

![Screen Shot 2021-03-30 at 21 56 28](https://user-images.githubusercontent.com/60457723/112992071-cf163280-91a2-11eb-89d7-c788976f3c07.png)
Figure 4: A ER diagram shows that each entities has several properties, which closely links to another table. In addition, it indicates primary key (id) and foreing key (user_id) that correspond to the user input which is stored in the database.


## Criteria C : Development

#### Main.py (python file)
```.py
from kivymd.app import MDApp
from kivymd.uix.label import MDLabel
from kivy.uix.behaviors import ButtonBehavior
from kivymd.uix.screen import MDScreen
import sqlite3
import hashlib, binascii, os



class HomeScreen(MDScreen):
    def on_enter(self, *args):
        self.ids.welcome_msg.text = f"Welcome to the order page, {LoginScreen.current_user_username} !"

    def try_order(self):
        menu = self.ids.menu_input.text
        quantity = self.ids.quantity_input.text
        address = self.ids.address_input.text
        phone = self.ids.phone_input.text
        current_user = LoginScreen.current_user

        if not current_user:
            # this happens if current user is None
            return "error"
        conn = sqlite3.connect('user.db')
        cur = conn.cursor()
        if not (menu == "karaage" or menu == "sashimi" or menu == "tenpura" or menu == "curry"):
            print("please put the name correctly")

        else:
            sql_order = f"insert into my_Order (my_menu, quantity, address, phone, user_id) values ('{menu}', '{quantity}', '{address}', '{phone}', '{current_user}');"
            cur.execute(sql_order)
            conn.commit()
            conn.close()
            sum_price = 0

            if menu == "karaage":
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





class RegisterScreen(MDScreen):



    def try_register(self):
        username = self.ids.username_input.text
        email = self.ids.email_input.text
        psw = self.ids.password_input.text
        psw_check = self.ids.password_check.text

        print(psw_check)

        if psw != psw_check:
            print("passwords do not match")
        else:
            conn = sqlite3.connect('user.db')
            sql = "select * from User where email ='{email}';"
            cur = conn.cursor()
            cur.execute(sql)
            result = cur.fetchone()

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
            self.parent.current = "HomeScreen"
            LoginScreen.current_user = id
            LoginScreen.current_user_username = username

            return result
        else:
            print("User does not exist")

class BillScreen(MDScreen):
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

    LoginScreen:
        name: "LoginScreen"
    RegisterScreen:
        name: "RegisterScreen"
    HomeScreen:
        name: "HomeScreen"

    BillScreen:
        name:"BillScreen"


<BillScreen>:
    BoxLayout:
        orientation: 'vertical'
        size: root.height, root.width

    FitImage:
        source: "izakaya.jpeg"

    MDCard:
        size_hint: 0.8, 0.8
        elevation: 10
        pos_hint: {"center_x":.5, "center_y": 0.5}
        orientation: "vertical"

        BoxLayout:
            orientation: 'vertical'
            size_hint: 0.8, 0.5
            pos_hint: {"center_x": 0.5}

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









<LoginScreen>:
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
        md_bg_color:[255/255, 255/255, 255/255, 0.6]

        MDBoxLayout:
            id: content #id or name
            adaptive_height: True
            orientation: "vertical"
            padding: dp(15)
            spacing: dp(10)

            MDLabel:
                text: "Login"
                font_style: "H3"
                halign: "center"


            MDTextField:
                id: email_input
                hint_text: "Email"
                icon_left: "email"
                helper_text: "Invalid email"
                helper_text_mode: "on_error"
                required: True

            MDTextField:
                id: password_input
                hint_text: "Password"
                icon_right: "eye-off"
                helper_text: "Invalid password"
                helper_text_mode: "on_error"
                required: True
                password: True

            MDRaisedButton:
                text: "Log in"
                on_release:
                    root.try_login()

            MDBoxLayout:
                adaptive_height: True

                ButtonLabel:
                    text: "Register"
                    halign: "right"
                    on_press:
                        print("here")
                        root.parent.current = "RegisterScreen"


```


## Criteria D : Functionality

Below is my functionality video↓


## Criteria E : Evaluation

### Unit testing

### Alpha testing

### Beta testing

### Limitation

### Further improvements



## Citation

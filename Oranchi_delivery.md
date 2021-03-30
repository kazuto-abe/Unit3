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

1. The product contains login/sign up page which includes one's username, email and its password.
2. The product contains at least two database which are linking each other.
3. The program has neither bugs nor technical issues and executes correctly.
4. Total price will be automatically calculated and shown on user's digital receipt.

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

### Normalized table


## Criteria C : Development

#### Main.py (python file)
```.py

```

#### Main.kv (kivy file)
```.py

```


## Criteria D : Functionality

### Alpha testing

### Beta testing


## Criteria E : Evaluation

### Limitation

### Further improvements


## Citation

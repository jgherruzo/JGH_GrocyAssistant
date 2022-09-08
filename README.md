# JGH_GrocyAssistant
Develop a Grocy Assistant using NodeRed, Telegram

## 1. Introduction
### 1.1 Context
I would like to improve our control over our grocery. Track the evolution of our inventory and cost.

I found some problems with the efficiency of using barcodes, due to it required to choose the amount of each item in the webapp, and I didn't find how to add the cost, so, at the end, you need to go to Grocy and modify some info after each shopping task.

### 1.2 Goal
This proyect try to minimize the work required into grocy web app. To do that, a telegram bot will be developed in order to could load all the items you buy during the own buying process. In a similar way, consumption could be done throught telegram. Another options will be ask for an specific item info or ask for the shopping list.

Due to another familiar could consume or buy thing for your inventory and could not use telegram, Rhasppy will help to control this part using a voice recognition system. It will be developed in the future.

## 2. Define

### 2.1 Features
Grocy Assistant will have the next features:
- Consume product: you could specify how many units of an item you consume
- ask for item info: bot will tell you the inventory of the given product
- ask for the product list: bot get a list of the product with each id and name. You dont have to remember each id
- add any item to the shopping list: you could add manually all the units of an item you want
- buy a product: you could specify how many items you buy, where, at what prize and the end date
- specify the shop: you could specify what shop you go, so, from the shopping list, the command to buy each item will be generated automatically
- ask for shopping list: bot will add each item below the minimum limit to the list that contains the item added manually
- remove from the shopping list: You could remove it to not buy or just remove each time you buy it

#### 2.1.2 Consumption

This feature helps you to control stocks level. It works below the next command:

/c_idxunits

/c is the main command, it is used by a switch to control flow. After check that, Node red send to a function where id and units are splitted and grocy API call is build. Then a switch check if function result is correct and send info to the telegram msg builder.

#### 2.1.3 Info

This feature helps you to control check stocks level. It works below the next command:

/info_id

/info is the main command, it is used by a switch to control flow. After check that, Node red send to a function where id is checked and grocy API call is build. Then a switch check if function result is correct and send the API call. Then, API answer is extracted and it is send to the telegram builder

#### 2.1.4 Info

This feature helps you to check id and names. It works below the next command:

/get_p

/get is the main command, it is used by a switch to control flow. After check that, Node red send to a function where  grocy API call is build. After that, API call is done and the answer is sent to a function where the msg is prepared. Then it is sent to msg telegram builder.

#### 2.1.5 Add

This feature helps you add items to the shopping list. Also if you defined a minimum level, when Grocy add it to the shoppping list add just the minimum you define, but maybe you want to buy more units. It works below the next command:

/a_itemxunits

/a is the main command, it is used by a switch to control flow. After check that, Node red send to a function where  grocy API call is build. After that, it is checked if everything goes well and API call is done. Then the answer is sent to a function where the msg done is prepared. Then it is sent to msg telegram builder.

#### 2.1.6 Buy


IMPORTANTE añadir Generico en la lista de tiendas y lanzar el inject antes de usar el grocy assistant

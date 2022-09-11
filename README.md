# JGH_GrocyAssistant
Develop a Grocy Assistant using NodeRed, Telegram

## IMPORTANT
After using GA you need to create a telegram boot. I advise to create a group and including you rbot, using this group will increase the security of your bot.

If you would like to use GA you must add "Generico" as shop in your grocy. After that, you must manually add it clicking on inject node or just send command /shop_Generico

Search for "WARNING" node. They are close to a node where you must include some personal info: Grocy IP, Grocy API key or telegram chat id.

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

#### 2.1.4 Product list

This feature helps you to check id and names. It works below the next command:

/get_p

/get is the main command, it is used by a switch to control flow. After check that, Node red send to a function where  grocy API call is build. After that, API call is done and the answer is sent to a function where the msg is prepared. Then it is sent to msg telegram builder.

#### 2.1.5 Add

This feature helps you add items to the shopping list. Also if you defined a minimum level, when Grocy add it to the shoppping list add just the minimum you define, but maybe you want to buy more units. It works below the next command:

/a_itemxunits

/a is the main command, it is used by a switch to control flow. After check that, Node red send to a function where  grocy API call is build. After that, it is checked if everything goes well and API call is done. Then the answer is sent to a function where the msg done is prepared. Then it is sent to msg telegram builder.

#### 2.1.6 Buy

This feature helps you add items to the inventory from the shop:

/b_itemxunitsxprizexshopxdate

item id and units you buy are mandatory, while the other are just an option. If you dont specify, 0 cost and no due date will be specified.

#### 2.1.7 Shop

This feature helps you to define where shop you are. 

/shop_name

Once shop name is saved, when you call for shopping list, this fill all the item that you usually buy in that shop.

#### 2.1.8 Shopping list

This feature helps you to check your shopping list each time you want. 

/get_l

Once you send the command, Grocy assistant check all items below the minimum level you define and add it to the shopping list. Then it show to you.

For each item, GA check if this item is usually bougth in th eshop you specify and get to you the command /X_item_units_Shop. If the item is not from this shop, the command will be /X_item_units, so you could check if you buy this item in that shop or not.

If you don't usually buy, but, today wnat to do, just click on the command. GA will read /x and get you a buying command: /b_itemxunitsx0xshopx2999-12-12 so you could copy and modify prize and due date, making easier all the process 

#### 2.1.9 Replace

This feature helps you remove items from the shopping list:

/r_itemxunits

## 3. Analysis

#### 3.1 Product list

Each time I ask for product list, I click on info command to check inventory, so it will be faster to show inventory directly over product list

#### 3.2 Consumption

Consumption process is easy, however, it is not productive for item you consume regurarly. My advise is to use recipe for this kind of consumption and left manual command just for items that take long time to consume (i.e. aditives, milk, etc) and take a look of your inventory at least once per week.

#### 3.2 Buying

Each time we click on /x command over the shopping list, prize must be replaced and due date format broke the command, so even if you want to click directly over the command you cannot.

/x command must look for the las prize and date will be written as YYYYMMDD instead of YYYY-MM-DD in order to to broke the command.

## 4. Improvements

#### 4.1 Pending
- Date modification for buying process
- show inventory in the product list
- show prize in the automatic buy command
- Simplify NODERED flow
- 
#### 4.2 Implemented
- GA check product over date once per day and send a msg
- Replace items from shopping list each time they are bougth
- Shopping list show a shop list to make easier set the shop you are buying 

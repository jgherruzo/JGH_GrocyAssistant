# JGH_GrocyAssistant
Develop a Grocy Assistant using NodeRed, Telegram and Rhasppy

## 1. Introduction
### 1.1 Context
I would like to improve our control over our grocery. Track the evolution of our inventory and cost.

I found some problems with the efficiency of using barcodes, due to it required to choose the amount of each item in the webapp, and I didn't find how to add the cost, so, at the end, you need to go to Grocy and modify some info after each shopping task.

### 1.2 Goal
This proyect try to minimize the work required into grocy web app. To do that, a telegram bot will be developed in order to could load all the items you buy during the own buying process. In a similar way, consumption could be done throught telegram. Another options will be ask for an specific item info or ask for the shopping list.

Due to another familiar could consume or buy thing for your inventory and could not use telegram, Rhasppy will help to control this part using a voice recognition system.

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

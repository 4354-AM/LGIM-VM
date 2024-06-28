# LGIM-VM
This component is built using spring as it enables fast development of RESTful API.

## Design
There are three packages;

### model
This holds the POJO for the vending machine object. This stores its coin inventory (coins) in a hashmap where the key is the denomination (in pennies) and the value is the quantity, this is ordered descendingly based on the key as this allows the refund function to return as few coins as possible. There are getters and setters to the hashmap as well as an insert coin method which allows a single change to it with out rewriting the whole map.

### service
This is where the logic takes place, there are four methods here;
- getcoins to return the current coin inventory, I added this as it helped with testing.
- initCoins which is used to setup/rewrite the coin inventory.
- insrtCoin which is used to insert a single coin into the coin inventory.
- refund which is used to return an array of coins that sums to the parameter value passed in, this uses a greedy algorithm by iterating through the sorted map and using as many coins as possible. in the case of there not being enough coins it will return an array that sums as closely as it can and output a message to the console.

### controller
This is the rest controller and is used to run the above methods from a respective api request.

/init-coins -> initCoins

/insert-coin -> insrtCoin

/current-coins -> getcoins

/refund -> refund

## Install/Run/Test
I'd recommend extracting the folder and running it in your IDE of choice as this will enable you to see the console. 

Unfortunately, I didn’t have time to create a comprehensive test harness. However, you can still interact with the API using curl or Postman. Below are the details on how to get started.

The code will run on localhost:8080 and can be interacted with the extensions mentioned within controller, here are some example requests:

`localhost:8080/init-coins?one=10&two=10&five=10&ten=10&twenty=10&fifty=10&pound=10&twoPound=10`
This sets each coin in coin inventory to a quantity of 10.

`localhost:8080/current-coins`
This returns the current coin inventory

`localhost:8080/insert-coin?coin=100`
This inserts a single pound (100) coin into the coin inventory

`localhost:8080/refund?refundAmount=50`
This returns an array of coins to the value of 50p (provided there is enough quantity)



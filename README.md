# BOGAZICI UNIVERSITY CMPE 48A CLOUD COMPUTING PROJECT
### Blockchain Network that works on Google Cloud Platform Virtual Machines

First of all there are two main source while I am implementing this project. 

[Back-End and Front-End Implementation of Blockchain](https://medium.com/@MKGOfficial/build-a-simple-blockchain-cryptocurrency-with-python-django-web-framework-reactjs-f1aebd50b6c)
<br />[Google Cloud Platform Django Stack VM and Firewall Configurations](https://www.youtube.com/watch?v=NcgcN2t19ww)

----

<br /> <h3>Project Architecture Diagrams</h3>
<br />
<br />

![alt text](https://github.com/berkingurcan/djangoblock/blob/main/diagram.png?raw=true)

<br />
<br />
<br />

----

First, we need to create virtual machine instances on GCP(or other platforms) in order to run the blockchain. Since we deploy Django Project, we need to launch
Django Stack deployment tool while creating vm to easily run the project. Then we will apply same steps in the youtube video [above](https://www.youtube.com/watch?v=NcgcN2t19ww):
<br />

<h4> Step 1: Launch VM </h4>

> Launch Django Stack Virtual Machines
>> Allow https traffic


<br />
<h4> Step 2: Firewall Rules </h4>

> Create a firewall rule for Django Stack Virtual Machines with:
>> <li> Proper targets(djangostack vms) </li>
>> <li> Source IP Address 0.0.0.0/0 </li>
>> <li> tcp: 8001 or what you want also 3000 for front end if you want </li>

<br />
<h4> Step 3: Deploy and Run Project </h4>
<h6> Run your django blockchain project </h6>
<br />
Open SSH your VM

```
cd /var/www
sudo git clone https://github.com/berkingurcan/djangoblock.git
cd djangoblock
cd PyChain
sudo python3 manage.py runserver 0.0.0.0:8001
```
<br />
Then enter your vm's public ip address with proper port (for instance: 35.233.251.204:8001)
You will see "Disallowed Host at" error.
Then: first `control + c`

```
cd PyChain
vim settings.py
```

Then write your IP address in `ALLOWED_HOSTS = []`
In order to save and quit `:w !sudo tee %`
Then run again the project:

```
cd ..
sudo python3 manage.py runserver 0.0.0.0:8001
```

After that, please run other node similarly by applying these steps above. Then use `connect_node` method to connect nodes each other.

<br />
<h4>Step 4: Front End  </h4>

Please download latest versions of `node.js` and `npm`. And change directory to `frontend` after that:
```
npm install
sudo npm run start 0.0.0.0:3000
```
----

<h1>Blockchain as an API </h1>

I have used Python and Django in order to implement blockchain and API.


**Mine Block**
----
  Returns mined block as a json file.

* **URL**

  /mine_block

* **Method:**

  `GET`
*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{  response = {'message': 'Congratulations, you just mined a block!',
                    'index': block['index'],
                    'timestamp': block['timestamp'],
                    'nonce': block['nonce'],
                    'previous_hash': block['previous_hash'],
                    'transactions': block['transactions']}}`
                    
**Get Chain**
----
  Returns chain as a json file.

* **URL**

  /get_chain

* **Method:**

  `GET`
*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `  response = {'chain': blockchain.chain,
                    'length': len(blockchain.chain)}`
                    
                    
                    
**Consensus**
----
  Returns is blockchain valid as a json file.

* **URL**

  /is_valid

* **Method:**

  `GET`
*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{'message': 'All good. The Blockchain is valid.'}` or `{'message': 'Houston, we have a problem. The Blockchain is not valid.'}`
    
    
    
**Replace Chain**
----
  Replacing the chain by the longest chain if needed

* **URL**

  /replace_chain

* **Method:**

  `GET`
*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{'message': 'The nodes had different chains so the chain was replaced by the longest one.',
                        'new_chain': blockchain.chain}` or `{'message': 'Houston, we have a problem. The Blockchain is not valid.'}`
                        
                        
                        
                        
**Adding Transaction**
----
  Adding a new transaction to the Blockchain

* **URL**

  /add_transaction

* **Method:**

  `POST`
*  **URL Params**

  None

* **Data Params**

  `['sender', 'receiver', 'amount','time']`

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{'message': f'This transaction will be added to Block {index}'}`
 
* **Error Response:**

  * **Code:** 400 <br />
    **Content:** `'Some elements of the transaction are missing'`
    
                        
**Connect Node**
----
  Connect node to blockchain

* **URL**

  /connect_node

* **Method:**

  `POST`
*  **URL Params**

  None

* **Data Params**

  `http://[node ip:port]`

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{'message': 'All the nodes are now connected. The Sudocoin Blockchain now contains the following nodes:',
                    'total_nodes': list(blockchain.nodes)}`
 
* **Error Response:**

  * **Code:** 400 <br />
    **Content:** `"No nodes"`


                        
 ----
 
 <h1>Performance Evaluation </h1>
  
 
 HTTP Load testing and API testing with `Number of Threads(users): 120` , `Ramp-up period(seconds)`, `Loop Count:10` HTTP Request one node `GET METHOD: /mine_block` in order to test mining performance by using Apache JMeter.
 
 View Results Tree results which includes HTTP Requests' response results: load time, latency etc. are in the repository `test_result20.csv`. 
 
 ![alt text](https://github.com/berkingurcan/djangoblock/blob/main/test_result.png?raw=true)
  
 <br />
 
 Also Summary Report listener in the repository `test_summary20.csv`.
 
 ![alt text](https://github.com/berkingurcan/djangoblock/blob/main/test_summary.png?raw=true) 
                    
 <br />
 
 Lastly, you can see below Graph Results of HTTP request for mining performance analysis.
 
 ![alt text](https://github.com/berkingurcan/djangoblock/blob/main/test_graph.png?raw=true)
 
 ![alt text](https://github.com/berkingurcan/djangoblock/blob/main/test_graph2.png?raw=true)


<img width="1440" alt="Screen Shot 2022-01-26 at 14 44 30" src="https://user-images.githubusercontent.com/70534820/151158184-103559e5-3c5b-48c8-83fd-97dd616bb694.png">
<img width="1440" alt="Screen Shot 2022-01-26 at 14 40 19" src="https://user-images.githubusercontent.com/70534820/151158198-7c80e0de-69af-411f-8f06-037de71ed92a.png">
<img width="1440" alt="Screen Shot 2022-01-26 at 14 39 53" src="https://user-images.githubusercontent.com/70534820/151158211-de9593d0-1803-4ee0-8352-e20a7ddcf21f.png">



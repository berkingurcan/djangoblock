# BOGAZICI UNIVERSITY CMPE 48A CLOUD COMPUTING PROJECT
### Blockchain Network that works on Google Cloud Platform Virtual Machines

First of all there are two main source while I am implementing this project. 

[Back-End and Front-End Implementation of Blockchain](https://medium.com/@MKGOfficial/build-a-simple-blockchain-cryptocurrency-with-python-django-web-framework-reactjs-f1aebd50b6c)
<br />[Google Cloud Platform Django Stack VM and Firewall Configurations](https://www.youtube.com/watch?v=NcgcN2t19ww)


<br /> <h3>Project Architecture Diagrams</h3>
<br />
<br />

![alt text](https://github.com/berkingurcan/djangoblock/blob/main/diagram.png?raw=true)

<br />
<br />
<br />

First, we need to create virtual machine instances on GCP(or other platforms) in order to run the blockchain. Since we deploy Django Project, we need to launch
Django Stack deployment tool while creating vm to easily run the project. Then we will apply same steps in the youtube video [below](https://www.youtube.com/watch?v=NcgcN2t19ww):
<br />

<h5> Step 1: Launch VM </h5>

> Launch Django Stack Virtual Machines
>> Allow https traffic


<br />
<h5> Step 2: Firewall Rules </h5>

> Create a firewall rule for Django Stack Virtual Machines with:
>> <li> Proper targets(djangostack vms) </li>
>> <li> Source IP Address 0.0.0.0/0 </li>
>> <li> tcp: 8001 or what you want also 3000 for front end if you want </li>

<br />
<h5> Step 3: Run project </h5>
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
<br />
<h5>Step 4: Front End  </h5>





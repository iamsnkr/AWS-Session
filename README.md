# Deploying a Node Js Application on AWS EC2

### Testing the project locally

1. Clone this project
```
git clone https://github.com/verma-kunal/AWS-Session.git
```
2. Setup the following environment variables - `(.env)` file
```
DOMAIN= ""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY=""
SECRET_KEY=""
```
3. Initialise and start the project
```
npm install
npm run start
```

### Set up an AWS EC2 instance

1. Create an IAM user & login to your AWS Console
    - Access Type - Password
    - Permissions - Admin
2. Create an EC2 instance
    - Select an OS image - Ubuntu
    - Create a new key pair & download `.pem` file
    - Instance type - t2.micro
3. Connecting to the instance using ssh
```
ssh -i instance.pem ubunutu@<IP_ADDRESS>
```

### Configuring Ubuntu on remote VM

1. Updating the outdated packages and dependencies
```
sudo apt update
```
3. Install Git - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-22-04) 
4. Configure Node.js and `npm` - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04)

### Deploying the project on AWS

1. Clone this project in the remote VM
```
git clone https://github.com/verma-kunal/AWS-Session.git
```
2. Setup the following environment variables - `(.env)` file
```
DOMAIN= ""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY=""
SECRET_KEY=""
```
> For this project, we'll have to set up an [Elastic IP Address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) for our EC2 & that would be our `DOMAIN`

3. Initialise and start the project
```
npm install
npm run start
```

> NOTE - We will have to edit the **inbound rules** in the security group of our EC2, in order to allow traffic from our particular port

### Project is deployed on AWS 🎉



**Stripe Payment Setup for the Project**
https://docs.google.com/document/d/1n0DH0Snz_s3BCfUUXkGEo_Pmczuefy6MxnlJmAJf73s/edit?pli=1#heading=h.rvpoiok2fx0r
Step 1
Create a new account on Stripe and login to the dashboard.
Step 2
Once logged-in, make sure the Test Mode is on before moving forward with the next steps. That way, you won’t need to worry about any credit cards, payments etc. as we are just using this for development purposes.



Step 3
Head over to the Developers tab. (It is visible in the image above, besides the Test Mode toggle)


Step 4
In the Developers section, head over to the API Keys tab and there you’ll find your test publishable & secret api key that you can use with the project.
Again, make sure the test data toggle is switched on.


__________________________________________
Only required if you are creating new publishable & secret keys!!
Alright, in order to view the actual stripe payment page for the workshops (when you run the website locally), you’ll need to create new products in the Stripe dashboard.

Step 1
Head over the products tab on the dashboard and click on Add product




Step 2
Add the required product info. Name, Price, Description (optional). Make sure you select the one time option as shown below and click on Save product.


Step 3
On the next page, you’ll be able to see all the details for your product. The important thing over here is the API ID that we need, which we’ll input in our code.

Here is the file from the original source code that shows where this product api id would go!



So, the logic is, 1 product per workshop and according to that, you can create 2 more products in Stripe dashboard and input in there IDs to other workshop html files. (similar to the above process).

Additional Resource to refer
https://stripe.com/docs/development/get-started

Hope this makes things clear & now you are able to use Stripe payment with your app!

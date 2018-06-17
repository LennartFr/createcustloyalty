# createcustloyalty

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Pre-reqs

1. Operating Systems: Ubuntu Linux 14.04 / 16.04 LTS (both 64-bit), or Mac OS 10.12 or higher
1. Docker (Version 17.03 or higher)
1. npm (v5.x)
1. Node (version 8.9 or higher - note version 9 is not supported)

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Step 1 Install the Hyperledger Composer runtime components

1. npm install -g composer-cli
1. npm install -g composer-rest-server
1. npm install -g generator-hyperledger-composer

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Step 2 Clone the Github Repo

1. Clone the Customer Loyalty Program with Blockchain repo on your laptop. 
   In a terminal, run: git clone https://github.com/LennartFr/customer-loyalty-program
2. cd customer-loyalty-program/
3. npm install
   
   The composer archive create command in package.json will create a file called clp-network@0.0.1.bna.
   
   https://hyperledger.github.io/composer/latest/reference/composer.archive.create.html

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Step 3: Setup Hyperledger Fabric Locally

Prior to starting, we recommend removing all running containers, and all previously created Hyperledger Fabric chaincode images:

1. docker kill $(docker ps -q)
1. docker rm $(docker ps -aq)
1. docker rmi $(docker images dev-* -q) 
1. rm -rf ~/.composer.  This command will remove all composer cards

1. The fabric setup scripts will be in the /fabric-dev-servers directory. Start fabric and create peer admin card:

1. cd fabric-dev-servers/
1. ./downloadFabric.sh
1. ./startFabric.sh
1. ./createPeerAdminCard.sh

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

1. First, install the business network:
1. cd ../
1. composer network install --card PeerAdmin@hlfv1 --archiveFile clp-network@0.0.1.bna
1. Start the business network:
1. composer network start --networkName clp-network --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret 
1. adminpw --card PeerAdmin@hlfv1 --file networkadmin.card
1. Import the network administrator identity as a usable business network card:
1. composer card import --file networkadmin.card
1. Check that the business network has been deployed successfully, run the following command to ping the network:
1. composer network ping --card admin@clp-network
1. If the command returns successfully, your setup is complete.

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Run the app

1. cd web-app/
1. npm install
1. Start the application:

1. npm start
1. The application should now be running at: http://localhost:8000

# createcustloyalty

# Step 1

1. Install composer cli: npm install -g composer-cli
1. Install composer-rest-server: npm install -g composer-rest-server
1. Install generator-hyperledger-composer: npm install -g generator-hyperledger-composer

# Step 2

Clone the Customer Loyalty Program with Blockchain repo locally. 

In a terminal, run:
git clone https://github.com/LennartFr/customer-loyalty-program

cd customer-loyalty-program/
npm install
The composer archive create command in package.json has created a file called clp-network@0.0.1.bna.

Prior to starting, would recommend removing all running containers, and all previously created Hyperledger Fabric chaincode images:

docker kill $(docker ps -q)
docker rm $(docker ps -aq)
docker rmi $(docker images dev-* -q)
This command will remove all composer cards

rm -rf ~/.composer

The fabric setup scripts will be in the /fabric-dev-servers directory. Start fabric and create peer admin card:

cd fabric-dev-servers/
./downloadFabric.sh
./startFabric.sh
./createPeerAdminCard.sh


First, install the business network:
cd ../
composer network install --card PeerAdmin@hlfv1 --archiveFile clp-network@0.0.1.bna
Start the business network:
composer network start --networkName clp-network --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card
Import the network administrator identity as a usable business network card:
composer card import --file networkadmin.card
Check that the business network has been deployed successfully, run the following command to ping the network:
composer network ping --card admin@clp-network
If the command returns successfully, your setup is complete.


cd web-app/
npm install
Start the application:

npm start
The application should now be running at: http://localhost:8000

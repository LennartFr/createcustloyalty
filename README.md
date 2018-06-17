# createcustloyalty

# Pre-reqs

1. Operating Systems: Ubuntu Linux 14.04 / 16.04 LTS (both 64-bit), or Mac OS 10.12 or higher
1. Docker (Version 17.03 or higher)
1. npm (v5.x)
1. Node (version 8.9 or higher - note version 9 is not supported)

# Step 1

1. Install composer cli: npm install -g composer-cli
1. Install composer-rest-server: npm install -g composer-rest-server
1. Install generator-hyperledger-composer: npm install -g generator-hyperledger-composer

# Step 2

1. Clone the Customer Loyalty Program with Blockchain repo locally. 
1. In a terminal, run: git clone https://github.com/LennartFr/customer-loyalty-program
1. cd customer-loyalty-program/
1. npm install
1. The composer archive create command in package.json has created a file called clp-network@0.0.1.bna.

Prior to starting, would recommend removing all running containers, and all previously created Hyperledger Fabric chaincode images:

1. docker kill $(docker ps -q)
1. docker rm $(docker ps -aq)
1. docker rmi $(docker images dev-* -q)
1. This command will remove all composer cards

1. rm -rf ~/.composer

1. The fabric setup scripts will be in the /fabric-dev-servers directory. Start fabric and create peer admin card:

1. cd fabric-dev-servers/
1. ./downloadFabric.sh
1. ./startFabric.sh
1. ./createPeerAdminCard.sh

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

1. cd web-app/
1. npm install
1. Start the application:

1. npm start
1. The application should now be running at: http://localhost:8000

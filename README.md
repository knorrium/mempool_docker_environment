# mempool_docker_environment

This is a minimal working Docker environment that brings up romanz/electrs, bitcoind in regtest and a mariadb instance for mempool development

## Instructions

- Run `docker-compose up`
- Copy the sample config files to the cloned `backend` and `frontend` dirs
- Build and run the backend (`npm install`, `npm run build`, `npm run start`)
- Build and run the frontend in local dev mode (`npm install`, `npm run build`, `npm run serve`)

After the backend and frontend are running, go to `http://localhost:4200` and verify you see the genesis block:

![Genesis](screenshots/genesis.png?raw=true "Genesis")

## Generating blocks

- SH into the bitcoind container (`docker exec -it mempool_docker_environment_bitcoind_1 /bin/sh`)
- Create a new wallet (`./bitcoin-cli -rpcport=28444 -rpcuser=mempool -rpcpassword=mempool -regtest getnewaddress testwallet`)
- Generate a new address (`./bitcoin-cli -rpcport=28444 -rpcuser=mempool -rpcpassword=mempool -regtest getnewaddress`)
- Mine a few blocks (`./bitcoin-cli -regtest -rpcport=28444 -rpcuser=mempool -rpcpassword=mempool generatetoaddress 101 ADDRESS`)

You'll see the new blocks on the frontend:

![New blocks](screenshots/new_blocks.png?raw=true "New blocks")
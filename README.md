Ethereum Network Intelligence API
============
[![Build Status][travis-image]][travis-url] [![dependency status][dep-image]][dep-url]

This is the backend service which runs along with ethereum and tracks the network status, fetches information through JSON-RPC and connects through WebSockets to [eth-netstats](https://github.com/cubedro/eth-netstats) to feed information. For full install instructions please read the [wiki](https://github.com/ethereum/wiki/wiki/Network-Status).


## Prerequisite
* eth, geth or pyethapp
* node
* npm


## Installation on an Ubuntu EC2 Instance

Fetch and run the build shell. This will install everything you need: latest ethereum - CLI from develop branch (you can choose between eth or geth), node.js, npm & pm2.

```bash
bash <(curl https://raw.githubusercontent.com/cubedro/eth-net-intelligence-api/master/bin/build.sh)
```
## Installation as docker container (optional)

There is a `Dockerfile` in the root directory of the repository. Please read through the header of said file for
instructions on how to build/run/setup. Configuration instructions below still apply.

## Configuration

Configure the app modifying [processes.json](/eth-net-intelligence-api/blob/master/processes.json). Note that you have to modify the backup processes.json file located in `./bin/processes.json` (to allow you to set your env vars without being rewritten when updating).

```json
"env":
	{
		"NODE_ENV"        : "production", // tell the client we're in production environment
		"RPC_HOST"        : "localhost", // eth JSON-RPC host
		"RPC_PORT"        : "8545", // eth JSON-RPC port
		"LISTENING_PORT"  : "30303", // eth listening port (only used for display)
		"INSTANCE_NAME"   : "", // whatever you wish to name your node
		"CONTACT_DETAILS" : "", // add your contact details here if you wish (email/skype)
		"WS_SERVER"       : "wss://rpc.ethstats.net", // path to eth-netstats WebSockets api server
		"WS_SECRET"       : "see http://forum.ethereum.org/discussion/2112/how-to-add-yourself-to-the-stats-dashboard-its-not-automatic", // WebSockets api server secret used for login
		"VERBOSITY"       : 2 // Set the verbosity (0 = silent, 1 = error, warn, 2 = error, warn, info, success, 3 = all logs)
	}
```

## Run

Run it using pm2:

```bash
cd ~/bin
pm2 start processes.json
```

## Updating

To update the API client use the following command:

```bash
~/bin/www/bin/update.sh
```

It will stop the current netstats client processes, automatically detect your ethereum implementation and version, update it to the latest develop build, update netstats client and reload the processes.

[travis-image]: https://travis-ci.org/cubedro/eth-net-intelligence-api.svg
[travis-url]: https://travis-ci.org/cubedro/eth-net-intelligence-api
[dep-image]: https://david-dm.org/cubedro/eth-net-intelligence-api.svg
[dep-url]: https://david-dm.org/cubedro/eth-net-intelligence-api

## Run on a macbook
Command history (Jun 2018):
```
503  git clone https://github.com/buidldao/eth-net-intelligence-api.git
  504  cd eth-net-intelligence-api/
  505  c
  506  ls -la
  507  npm install
  508  c
  509  head package.json 
  510  cd ~/bin
  511  node ./app.js
  512  c
  513  sudo npm install -g pm2
  514  npm install -g pm2
  515  sudo npm install -g pm2
  516  bash netstatconf.sh 1 parity http://localhost:3000 "chosen_secret" > app.json
  517  c
  518  touch netstatconf.sh
  519  atom netstatconf.sh 
  520  chmod +x netstatconf.sh 
  521  bash netstatconf.sh 1 parity http://localhost:3000 "chosen_secret" > app.json
  522  cat app.js
  523  cat app.json
  524  c
  525  pm2
  526  c
  527  pm2 start app.json
  528  pm2 show 58510
  529  pm2 start app.json
  530  pm2 show 58647
  531  c
  532  ls -la
  533  sudo nano app.js
  534  sudo nano app.json
  535  c
  536  pm2 start app.json
  537  sudo nano app.json
  538  pm2 start app.json
  539  sudo nano app.json
  540  c
  541  pm2 start app.json
  542  pm2 show 58838
  543  sudo nano app.json
  544  pm2 start app.json
  545  pm2 show 58920
  546  sudo nano app.json
  547  pm2 start app.json
  548  sudo nano app.json
  549  c
  550  pm2 start app.json
  551  h
  552  c
  553  h

```

For a local parity network, modify ```app.json``` with port `8545` 

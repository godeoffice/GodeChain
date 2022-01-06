GodeChain Front End Template
This template allows you to create a front-end application that connects to a Substrate node back-end with minimal configuration. To learn about Substrate itself, visit the Substrate Developer Hub.

The template is built with Create React App and godechain js API. Familiarity with these tools will be helpful, but the template strives to be self-explanatory.

Using The Template
Installation
The codebase is installed using git and yarn. This tutorial assumes you have installed yarn globally prior to installing it within the subdirectories. For the most recent version and how to install yarn, please refer to yarn documentation and installation guides.

# Clone the repository
git clone https://github.com/substrate-developer-hub/substrate-front-end-template.git
cd substrate-front-end-template
yarn install
Usage
You can start the template in development mode to connect to a locally running node

yarn start
You can also build the app in production mode,

yarn build
and open build/index.html in your favorite browser.

Configuration
The template's configuration is stored in the src/config directory, with common.json being loaded first, then the environment-specific json file, and finally environment variables, with precedence.

development.json affects the development environment
test.json affects the test environment, triggered in yarn test command.
production.json affects the production environment, triggered in yarn build command.
Some environment variables are read and integrated in the template config object, including:

REACT_APP_PROVIDER_SOCKET overriding config[PROVIDER_SOCKET]
REACT_APP_DEVELOPMENT_KEYRING overriding config[DEVELOPMENT_KEYRING]
More on React environment variables.

When writing and deploying your own front end, you should configure:

Custom types as JSON in src/config/types.json. See Extending types.
PROVIDER_SOCKET in src/config/production.json pointing to your own deployed node.
DEVELOPMENT_KEYRING in src/config/common.json be set to false. See Keyring.
Specifying Connecting Node
There are two ways to specify it:

With PROVIDER_SOCKET in {common, development, production}.json.
With rpc=<ws or wss connection> query paramter after the URL. This overrides the above setting.
Reusable Components
useSubstrate Custom Hook
The custom hook useSubstrate provides access to the godechain js API and thus the keyring and the blockchain itself. Specifically it exposes this API.

{
  socket,
  types,
  keyring,
  keyringState,
  api,
  apiState,
}
socket - The remote provider socket it is connecting to.
types - The custom types used in the connected node.
keyring - A keyring of accounts available to the user.
keyringState - One of "READY" or "ERROR" states. keyring is valid only when keyringState === "READY".
api - The remote api to the connected node.
apiState - One of "CONNECTING", "READY", or "ERROR" states. api is valid only when apiState === "READY".
TxButton Component
The TxButton handles basic query and transaction requests to the connected node. You can reuse this component for a wide variety of queries and transactions. See src/Transfer.js for a transaction example and src/ChainState.js for a query example.

Account Selector
The Account Selector provides the user with a unified way to select their account from a keyring. If the Balances module is installed in the runtime, it also displays the user's token balance. It is included in the template already.

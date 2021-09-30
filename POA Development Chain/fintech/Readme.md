# Fintech, an out-of-the-box blockchain

In this tutorial, I will demonstrate using `geth`, the official Ethereum client, and how to run the PupperNet private network.

This network is configured for `15 second` block times and uses the Clique Proof of Authority consensus algorithm. This
will ensure fast and efficient testing, so no need to worry about your CPU. The chain ID is `333`.

The sealer node addresses are:

`0xA4Ce15aEFDdb06402Ef4dbd6791eC1911f25769a`
`0x2f6660BAd531c3f030dfE4305e4c0cC260c7EC72`

The account password for both nodes is `123`

This is the configuration from `fintech`:

![fintech](POA%20Development%20Chain/fintech/Screenshot%20folder/setting%20up%20the%20proof_of_authority.JPG)

## Install the geth node software

Download and install `geth` for your operating system here: <https://geth.ethereum.org/downloads/>

## Install the MyCrypto GUI wallet

Download and install the desktop version of the MyCrypto wallet here: <https://download.mycrypto.com/>

This wallet allows communicating with custom networks, which we will configure later.

## Run the first node and enable mining/sealing

`geth --datadir node1 --unlock "0xA4Ce15aEFDdb06402Ef4dbd6791eC1911f25769a" --mine --rpc`

We enable the `--rpc` flag on the first node to talk to it later. This defaults to port `8545`.

Windows users may also need to enable the `--allow-insecure-unlock` flag.

We need to unlock the node's account to enable it to sign blocks.

## Copy the enode address from this node

For example:
`enode://e74b8b1589637f4dee2daaf1b45441281bfbbd18444d339f8dcf771003a7dfd5b7dae20313ebfa3fa2a524811187a27fd40973a19ec3625a230304fb54e654a7@127.0.0.1:30303`

## Use the first node's enode address as the bootnode for the second node and run on a separate port

`./geth --datadir node2 --unlock "0x2f6660BAd531c3f030dfE4305e4c0cC260c7EC72" --mine --port 30304 --bootnodes "enode://e74b8b1589637f4dee2daaf1b45441281bfbbd18444d339f8dcf771003a7dfd5b7dae20313ebfa3fa2a524811187a27fd40973a19ec3625a230304fb54e654a7@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock`

Using the first node as a bootnode will enable the nodes to communicate with each other and discover new nodes later.

Windows users may also need to enable the `--ipcdisable` and `--allow-insecure-unlock` flags.

## Success!

You should now be mining/sealing blocks using the Proof of Authority algorithm! Now it's time to send a transaction.

## Send a test transaction

Open up MyCrypto and select `Change network` at the bottom left.

Select `Add Custom Node` and use `127.0.0.1:8545` to connect to the first node, add a name, use chain ID `333` and save.

Your configuration should look like this:

![custom-node](POA%20Development%20Chain/fintech/Screenshot%20folder/Setting_up_custom_node.JPG)

You should now be connected to the local blockchain.

Click on the `Keystore file` option to access the first node's wallet, and navigate to `node1/keystore` and select
the keystore file, then enter `testnetpassword` as the password.

You should now be able to send a transaction. Fill in the second node's account and send it one ETH.

![transaction-send](POA%20Development%20Chain/fintech/Screenshot%20folder/Confirming%20transaction.JPG)

Once confirmed, you can check the TX Status by clicking the button in the popup, or pasting the TX Hash into the TX Status section of the app.

![transaction-success](POA%20Development%20Chain/fintech/Screenshot%20folder/Successful%20Transaction%20Status.JPG)

Voila! You can now use the PupperNet blockchain for your local development!

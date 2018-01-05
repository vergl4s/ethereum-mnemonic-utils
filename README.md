Ethereum Mnemonic Key Utils
================================

Script to convert Ethereum mnemonic keys into regular private keys that can be consumed by regular wallets. Default parameters work for Ledger ETH wallets, but it *should* be able to support any wallet that uses BIP32 HD and BIP39 seed standards.

Modularity and extensibility were sacrificed to keep the code as simple and linear as possible. That way it should much easier for you to review this before running it :)

Logic adapted from https://github.com/satoshilabs/slips/blob/master/slip-0010/testvectors.py and https://github.com/trezor/python-mnemonic.

### Requirements

`pip install base58 ecdsa`

### Examples

#### Mnemonic key > private key

	$ echo "legal winner thank year wave sausage worth useful legal winner thank yellow" > myfile
    $ ./mnemonic_utils.py myfile


#### Mnemonic key > private key #2

    from mnemonic_utils import mnemonic_to_private_key
    private_key = mnemonic_to_private_key("legal winner thank year wave sausage worth useful legal winner thank yellow")


#### Private key > Mist keystore using eth-keyfile module

    import binascii
    import eth_keyfile
    json_keyfile = eth_keyfile.create_keyfile_json(binascii.unhexlify(private_key), b"any password")

#### Private key > Mist keystore using web3.py module

    import binascii
    from web3.auto import w3
    json_keyfile = w3.eth.account.privateKeyToAccount(binascii.unhexlify(private_key)).encrypt(b"any password")

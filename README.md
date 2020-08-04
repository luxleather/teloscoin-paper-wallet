# TELOSCOIN paper wallet
CLI tool for making nice looking printable TELOS paper wallets to hold your Teloscoins.

![PyPI - Python Version](https://img.shields.io/pypi/pyversions/Pillow?style=plastic) ![GitHub repo size](https://img.shields.io/github/repo-size/luxleather/teloscoin-paper-wallet?style=plastic) ![GitHub](https://img.shields.io/github/license/luxleather/teloscoin-paper-wallet?style=plastic)

![Showcase](https://github.com/luxleather/teloscoin-paper-wallet/blob/master/img/showcase.png)


Table of contents:
* [About this wallet](https://github.com/luxleather/teloscoin-paper-wallet#about-this-wallet)
    * [How private keys are generated](https://github.com/luxleather/teloscoin-paper-wallet#how-private-keys-are-generated)
    * [How public address are generated](https://github.com/luxleather/teloscoin-paper-wallet#how-public-address-are-generated)
* [Installation](https://github.com/luxleather/teloscoin-paper-wallet#installation)
    * [Windows](https://github.com/luxleather/teloscoin-paper-wallet#windows-users)
    * [Linux](https://github.com/luxleather/teloscoin-paper-wallet#linux-users)
* [Usage](https://github.com/luxleather/teloscoin-paper-wallet#usage)
* [How to print and fold](https://github.com/luxleather/teloscoin-paper-wallet#how-to-print-and-fold)
* [QA](https://github.com/luxleather/teloscoin-paper-wallet#qa)
* [Disclaimer](https://github.com/luxleather/teloscoin-paper-wallet#disclaimer)
___
## About this wallet

Easy to use python CLI tool that allows users to generate printable wallets for Teloscoin completely offline.

Teloscoin paper wallet is unofficial for now, and should be validated by experienced users. I will provide information on how this tool works, and why it is safe to use which I believe.

**If you find a bug, spot a lack of logic, or anything else that makes this tool not safe, please inform. Either I can fix the issue or delete this repo.**

While this tool is 'safe', it is notable that you should trust no one, especially in crypto. I would personally recommend testing a few keys that you do not intend to use by importing into wallet to make sure that they work fine. It is strongly encourage for you too look through the source code and make sure there are no obviously buggy/malicious parts. The code is fairly simple, anyone can look and see there are no online sources being used and there are no sending information to myself or anyone else, or just randomly choosing private keys from a list.

All the private keys and public addresses generated by this tool are generated using python built-in packages as well as the external known packages: ecdsa, base58, qrcode and PIL.

Credit for the idea of this tool going to repo: https://github.com/fortesp/bitcoinaddress/tree/dev

### How private keys are generated

This is the most important aspect of generating wallets. A wallet is only as secure as the private key support it. Private keys for most cryptocurrencies like BTC, ETH and LTC are all generated the same way using the SHA256 hashing protocol. The way the SHA256 hashing protocol was implemented was by using the python built-in package hashlib.

A WIF “Wallet Import Format” private key is a standard private key, but with a few added extras. Learn more about WIF private keys at (https://learnmeabitcoin.com/technical/wif).

Teloscoin paper wallet create uncompressed WIF private keys.

### How public address are generated

*Public key is unique number mathematically generated from a private key. The use of elliptical curve multiplication gives you a mathematical connection from your private key to your public key with two important properties:*

*1. It’s not known how to work backwards to get the private key*

*2. You can prove that you have the private key without giving it away*

Source (https://learnmeabitcoin.com/technical/public-key)

Teloscoin addresses are formed in the steps according to:

```private key > SECP256k1 elliptic curve > add extension b"04" > public key```

```public key > SHA256 > Ripemd160 > add extension b"26" > hash160 public key```

```hash160 public key > SHA256 > SHA256 > checksum```

```Teloscoin address = base58 encoding of hash160 public key + checksum```

Learn more: (https://learnmeabitcoin.com/technical/public-key-hash) and (https://learnmeabitcoin.com/technical/address)

## Installation

### Windows users

Download any Python3.x version from official python website (https://www.python.org/downloads/windows).

Make new folder on C:\Python3x and install Python in it (not mandatory).

Download Teloscoin paper wallet files from this repo and unpack it on the Desktop.

Run cmd.exe and enter into directory `C:\>cd Users\<username>\Desktop\teloscoin-paper-wallet-master`

Install required modules:

`C:\Users\<username>\Desktop\teloscoin-paper-wallet-master>py -m pip install -r requirements.txt`

Run file and create paper wallet:

`C:\Users\<username>\Desktop\teloscoin-paper-wallet-master>wallet.py`

### Linux users

Install any Python3.x version.

Download Teloscoin paper wallet files from this repo and unpack it on the Desktop.

Run Terminal and type: `cd /home/<username>/Desktop/teloscoin-paper-wallet-master`

Install pip:

`sudo apt install python-pip`

Install required modules:

`pip install -r requirements.txt`

Run file and create paper wallet:

`python3 wallet.py` (you must be in telos-paper-wallet-master folder)

## Usage

CLI will give you information about created address and paper wallet file which will be created in same folder and with a filename of the created address, of course with .PNG image file extension. This is for case you want to create several paper wallets, every of them will be named as address.

Note: After printing the wallet you need to delete created file/s and keep paper wallet/s only in physical form until you decide to spend.

**Important: You should always spend all the funds on a paper wallet, not part of it or you will lose the rest! If you spend a partial amount, the rest of the coins will go to a change address and the paper wallet will be empty. However most pc/mobile wallets will return change to a newly generated change address, which is not the same as the address on the paper wallet. Learn about change addresses (https://en.bitcoin.it/wiki/Change).**

## How to print and fold

Keep in mind that original Teloscoin paper wallet dimensions for print are 14cm width and 20cm height. Fold the printed wallet by shorter half first, then by longer half so that the address and private key are inside. This way the outside will have a home page with a logo and a back page with space for notes. The final dimensions of the folded wallet are 7x10 centimeters.

## QA

Can this tool be used for brute-forcing?

Fortunately this is only possible theoretically. If you were to use this tool trying to make a address/WIF key pair that have balance (already in use), it would take you a 2^45 years. For comparison age of the universe is 2^33.7 years. Explanation (https://bitcoin.stackexchange.com/a/3205).

Why there is no web application for this tool?

In short, to avoid the risks of hacking as much as possible. Using python and cli on a computer that is offline provides a good level of security when creating a wallet. Of course, this is true if your computer is virus/malware free.

## Disclaimer

Please use at your own risk, knowing what you are doing and test first by importing several keys into wallet to be sure everything work. Also test with small amounts of coins. Author of this tool will not be liable for any losses incurred due to improper use.

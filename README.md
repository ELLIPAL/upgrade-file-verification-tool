# upgrade-file-verification-tool
Verification tool of ELLIPAL hardware wallet upgrade files.  
ELLIPAL's anti-tamper mechanism is to sign the upgrade file hash via Bitcion signing process. This ensures it cannot be broken and is easy to be verified.

This standalone tool is based on the code of bitcoin-qt(https://github.com/bitcoin/bitcoin) for Bitcoin message signatures verification.

## Dependencies and Building

The only library this depends on is OpenSSL.  On Ubuntu or similar systems, the following should be sufficient to install dependencies and build:

    sudo apt-get install build-essential libssl-dev
    make

## Usage
    verifymessage  ELLIPLA-upgrade-Bitcoinaddress  signature-base64  hash

An example usage of the tool: 

    ./verifymessage 16VbmSZz1XMijBVsAJkNmZJfZBWWJUP9R2 H7BxtfVjSv3ogBktEhEDgeTPLP3XS4hltI/RJJu/C91yzaVPCJdpowUh2LqfD4uk9dX1P1KvJH4V50siIiO15Yg= A9AA0A3FA60486CB72FFE37C8A527DF3A3ED29B6CC1B91A3779C13DA44E964ED

## Understanding the upgrade processing

1. The *.bin format upgrade file released by ELLIPAL is an encrypted file. The sha256 hash value of the *.bin file is stored in in Hash.txt and and is used to detect that the *.bin file has not been tampered with.     

2. In order to ensure that the bin file and hash are not tampering at the same time, ELLIPAL applies the bitcoin signature to sign the hash. The content of signature（in base64 format) is saved in in Hash.txt, just following the hash. Anyone can verify the hash signature by ELLIPAL's bitcoin address(16VbmSZz1XMijBVsAJkNmZJfZBWWJUP9R2) to confirm if the BIN file was sent by ELLIPAL.    

3. Since we have applied standard Bitcoin signature, you can also verify the signature result by any tool you are familiar with.
4. The addresses used by ELLIPAL:  
```
    EC02[Titan]: 16aKCK1V63C8YQHdWCNiLvumhfJA7HHTKs  
    EC01 V1: 16VbmSZz1XMijBVsAJkNmZJfZBWWJUP9R2  
    EC01 V2：17NTNuG1sGoHz9iPgZFYAUYHBn9WqEsTDb  
```


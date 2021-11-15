# Vanity Accounts

Step one is to create the validator's account specifically the account that represents the identity of the validator.  You have already created an account to hold the SAFE, but that might be in an app or online.  
Your validator account will be in a "paper" wallet created as follows:
```bash
safecoin-keygen new -o id.json
```
The output will appear as follows:
```
Generating a new keypair

For added security, enter a BIP39 passphrase

NOTE! This passphrase improves security of the recovery seed phrase NOT the
keypair file itself, which is stored as insecure plain text

BIP39 Passphrase (empty for none):
Enter same passphrase again:

Wrote new keypair to id.json
===============================================================================
pubkey: 5SUyfGdCJXB6tJRkEHC9ScDjk4VpGsDM1cFmUuJfZ7PJ
===============================================================================
Save this seed phrase and your BIP39 passphrase to recover your new keypair:
common license enrich tilt afford summer drift cactus dolphin alone eternal pink
===============================================================================
```
So now and forever more your validator will be known as `5SUyfGdCJXB6tJRkEHC9ScDjk4VpGsDM1cFmUuJfZ7PJ` 
Here is where my verbiage starts to add value, just like you can ask your state government for a vanity license plate, you can generate a vanity pubkey!   For example you might want to name your validator Wally, can you do that? "Yes" is the answer:

```bash
safecoin-keygen grind --starts-with Wa11y:1 -o id.json
Searching with 8 threads for:
	1 pubkey that starts with 'Wa11y' and ends with ''
Searched 1000000 keypairs in 6s. 0 matches found.
Searched 2000000 keypairs in 13s. 0 matches found.
Searched 3000000 keypairs in 20s. 0 matches found.
    ...
Searched 17738000000 keypairs in 134260s. 0 matches found.
Wrote keypair to Wa11ysC4xguKmaSERxA9asHH6Bex2o3uWHFex1C27eu.json
```
Couple of points: First, yes that's "Wa11y" with two ones, because "1" and "l" because visual ambiguity is not allowed with public keys.  Second, I really did that and it took a *while*!!! More than 37 hours on my 8 core modern linux development box.

....Now you have a vanity public key and you are on your way to being a marketing genius!!!!  


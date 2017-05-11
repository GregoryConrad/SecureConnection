# SecureConnection
A class that allows for a secure connection (with a chosen dynamic amount of security) to be established between two different java applications.
# Usage
**Creating The Secure Connection / Key Creation**  
First, one party (Alice) has to generate a public key (this step can take quite some time, depending on the speed of the system):  
`SecureConnection alice = new SecureConnection();`  
`byte[] alicePubKey = alice.getPublicKey();`  
Then, that public key is sent over to the other party (Bob). Bob processes Alice's key, and creates his own public key:  
`SecureConnection bob = new SecureConnection();`  
`byte[] bobPubKey = bob.getPublicKey(alicePubKey);`  
Finally, Bob sends his newly created public key to Alice. Then, both parties have each other's public keys. They then process the other person's public key.  
- What Alice runs: `alice.processOtherPubKey(bobPubKey);`  
- What Bob runs: `bob.processOtherPubKey(alicePubKey);`  
That will provide for one layer for encryption when either Alice or Bob sends data to each other. The above steps must be repeated (using the same SecureConnection objects) for as many layers of encryption that is desired.

**Transmitting Information**  
After the secure connection has been established, Alice and Bob want to transmit information securely. I tried to make this as easy and possible.

*In the following example,*
- *`secureConnectionObject` was the `SecureConnection` object used during the key creation*
- *`send()` is a generic method to send information to the other party with*
- *`whatToSend` is a byte array featuring the message to send*
- *`whatWasSent` is a byte array featuring what was sent*

On sending a message: `send(secureConnectionObject.encrypt(whatToSend));`  
On receiving a message: `byte[] decryptedMessage = secureConnectionObject.decrypt(whatWasSent);`  

And that's it! I hope you find this useful.

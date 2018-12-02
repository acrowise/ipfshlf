### IPFS with Hyperledger Fabric

While digital or scanned documents are quitnessential for conducting business between multiple parties. Yet Blockchains are not ready for storing large documents and media files, This motivates us to find a complementary decentralized data store for peer to peer document exchange without compromising the foundatonal security and immutability that business requires in (Bid/Tenders, Medical Health Record, Bill of Landing) applications.

Here I will demonestrate how to combine IPFS as a data store for documents and media with blockchain particularly hyperledger fabric to achieve our goal.

**Disclaimer** : This is not a 101 for blockchain, Crypto, IPFS. Late night experiement not for production.

- First we install IPFS from [here](https://docs.ipfs.io/introduction/install/)
  
- Initialize 
  > `ipfs init`
- Run the daemon  
  > `ipfs daemon`
- Open another terminal and check the peers you are connected to 
  > `ipfs swarm peers`
- Display the IPFS readme file 
  > `ipfs cat /ipfs/QmYwAPJzv5CZsnA625s3Xf2nemtYgPpHdWEz79ojWnPbdG/readme`
- Curl IPFS to get a cat from the network 
  > `curl "https://ipfs.io/ipfs/ipfs/QmW2WQi7j6c7UgJTarActp7tDNikE4B2qXtFCfLPdsgaTQ"`

- Instal GNUGPG
  > `sudo apt-get install gnupg2`  
windows users can use [GP4WIN](https://www.gpg4win.org/)
- Generate asymmetric key on your first machine 
  > `gnu --generate-key` 
- Generate another asymmetric key on a second computer 
  > `gpg --generate-key`
- Export the public key of the second machine using 
  > `gpg --export --armor $SECOND_EMAIL > pubkey.asc`
- Import the public into the keyring of your first machine 
  > `gpg --import pubkey.asc`
- check new key is imported 
  > `gpg --list-keys`
- Encrypt a smaple document using the receipient public key 
  > `gpg --encrypt --recipient "$SECOND_PK_EMAIL" $DOCUMENTPATH`
- Add the encrypted document to ipfs 
  > `ipfs add $ENCRYPTEDDOCUMENTPATH`
- `putState` the document name and IPFS hash in a similar structure to the smart contract
   
```
type DocumentIPFS struct {
	DocumentName     string `json:"documentName"`
	IPFSHash string `json:"ipfsHash"`
	NextActionBy string `json:"nextActionBy"` 
	Status   string `json:"status"`
}
```
I let you figure out how to get your document back.  

Best.
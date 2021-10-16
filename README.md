# casper_gitcoin

## 1. Create and deploy a simple, smart contract with cargo casper and cargo test
* build the contract
![image](https://user-images.githubusercontent.com/87713875/136832708-4be1320d-1a40-45c3-8619-8a3845d9dbdb.png)

* test the contract
![image](https://user-images.githubusercontent.com/87713875/136832721-876a442b-6764-4cb1-aad4-8b710f1a4dd0.png)

* deploy on testnet
![image](https://user-images.githubusercontent.com/87713875/136832733-d682c9a9-f294-4f68-b673-55e81c89e61b.png)

* Check Deploy Status
![image](https://user-images.githubusercontent.com/87713875/136832747-05799eb6-b9e1-4f93-befb-318087242dee.png)

## 2. Complete one of the existing tutorials for writing smart contracts(counter)
* compile to WASM
![image](https://user-images.githubusercontent.com/87713875/136832783-d9862829-d85c-43dc-8255-668ce78b5168.png)
![image](https://user-images.githubusercontent.com/87713875/136832798-e2c5fc78-5c55-4fe6-a224-cf036208c6ea.png)
![image](https://user-images.githubusercontent.com/87713875/136832810-0d72e728-afda-4ef7-8ebb-cb7a2a0c405f.png)

* Deploy On Testnet
![image](https://user-images.githubusercontent.com/87713875/136832818-30a05bd2-d5d9-4f8d-a0c6-df24579c9f05.png)

* check status
![image](https://user-images.githubusercontent.com/87713875/136832832-b919bb69-ffd3-4024-9e07-b63525b3fa54.png)

* Get the NEW state-root-hash
![image](https://user-images.githubusercontent.com/87713875/136832863-94614a54-26d5-4bb1-a84c-48c8fcdc5a3a.png)

* Increment the Counter
![image](https://user-images.githubusercontent.com/87713875/136832873-19ae9d2a-d187-4733-ade3-cb2778fecf32.png)

* Increment the Counter Again
![image](https://user-images.githubusercontent.com/87713875/136832894-3d63ca50-c8e3-460e-aa09-a1ef86f0dee3.png)

* View the Final Network State
![image](https://user-images.githubusercontent.com/87713875/136832910-bef00dbd-a119-4509-9ddb-740abbecf075.png)

## 3.Demonstrate key management concepts by modifying the client in the Multi-Sig tutorial to address one of the additional scenarios(Scenario 2: Deploying with special keys)


* build the key-manager
![image](https://user-images.githubusercontent.com/87713875/136832972-030e0e7c-7e8f-43b7-8033-53fe9d4fa28b.png)


* Test the client
![image](https://user-images.githubusercontent.com/87713875/136832991-4ada40ab-4853-4f72-b1b7-597a5cfc7477.png)


* change the code 
```
const keyManager = require('./key-manager');
const TRANSFER_AMOUNT = process.env.TRANSFER_AMOUNT || 2500000000;

(async function () {
    
    // In this example the 2 additional accounts will be added to 
    // the mainAccount to perform deploys, but they will not be 
    // able to add another account. 
    
    // To achive the task, we will:
    // 1. Add first new key with weight 1 (first account).
    // 2. Set mainAccount's weight to 2.
    // 3. Set Keys Management Threshold to 2.

    let deploy;

    // 0. Initial state of the account.
    // There should be only one associated key (facuet) with weight 1.
    // Deployment Threshold should be set to 1.
    // Key Management Threshold should be set to 1.
    let masterKey = keyManager.randomMasterKey();
    let mainAccount = masterKey.deriveIndex(1);
    let firstAccount = masterKey.deriveIndex(2);

    console.log("\n0.1 Fund main account.\n");
    await keyManager.fundAccount(mainAccount);
    await keyManager.printAccount(mainAccount);
    
    console.log("\n[x]0.2 Install Keys Manager contract");
    deploy = keyManager.keys.buildContractInstallDeploy(mainAccount);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);

    // 1. Add first new key with weight 1 (first account).
    console.log("\n1. Add first new key with weight 1.\n");
    deploy = keyManager.keys.setKeyWeightDeploy(mainAccount, firstAccount, 1);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);
   
    // 2. Set mainAccount's weight to 2
    console.log("\n2. Set faucet's weight to 2\n");
    deploy = keyManager.keys.setKeyWeightDeploy(mainAccount, mainAccount, 2);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);
    
    // 3. Set Keys Management Threshold to 2.
    console.log("\n3. Set Keys Management Threshold to 2\n");
    deploy = keyManager.keys.setKeyManagementThresholdDeploy(mainAccount, 2);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);
    

 
 
})();

```

* run the client
![image](https://user-images.githubusercontent.com/87713875/136833019-0ec3d203-6e31-4131-9aef-65a77f806e16.png)


## 4.Learn to transfer tokens to an account on the Casper Testnet
* Direct transfer
![image](https://user-images.githubusercontent.com/87713875/136833047-c6e7663e-43ac-4e51-a86d-f100a4bf6abe.png)


* check transfer state
![image](https://user-images.githubusercontent.com/87713875/136833065-9d1700c8-36e3-4152-bfcf-e7a3dd332d8b.png)




## 5. Learn to Delegate and Undelegate on the Casper Testnet


* Delegate completed
![image](https://user-images.githubusercontent.com/87713875/136833083-6044ebf5-890c-4f74-8c09-64844f3a9cc2.png)


* Undelegate completed
![image](https://user-images.githubusercontent.com/87713875/136833097-2064ae24-b1fc-4bb8-abb8-596b84c19e43.png)


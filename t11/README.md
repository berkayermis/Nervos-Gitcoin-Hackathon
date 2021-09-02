## A screenshot of the accounts you created (account list) in ckb-cli.

![Screenshot from 2021-08-19 14-12-21](https://user-images.githubusercontent.com/67913214/130059291-218937f5-33b7-465c-8df6-c1abe53539e7.png)

## A link to the Layer 1 address you funded on the Testnet Explorer.

https://explorer.nervos.org/aggron/address/ckt1qyqw72rcmekhdea8jl56ahczkewmueyp96eq0vve0w

## A screenshot of the console output immediately after you have successfully submitted a CKByte deposit to your Tron account on Layer 2.

![Screenshot from 2021-08-19 14-56-02](https://user-images.githubusercontent.com/67913214/130064514-6cd96bd1-d321-4d32-9523-0b8b0c815f90.png)
![Screenshot from 2021-08-19 14-56-18](https://user-images.githubusercontent.com/67913214/130064519-8d650cd2-f4db-4a22-a4b6-4670e8acb4e4.png)
![Screenshot from 2021-08-19 14-56-30](https://user-images.githubusercontent.com/67913214/130064536-2a279faf-b1b3-4515-9906-4cfd5b75829d.png)

## A screenshot of the console output immediately after you have successfully issued a smart contract calls on Layer 2.

![Screenshot from 2021-09-02 19-24-16](https://user-images.githubusercontent.com/67913214/131881299-3ce9eb61-42a0-44b2-a092-e784511b1334.png)

![Screenshot from 2021-09-02 19-33-07](https://user-images.githubusercontent.com/67913214/131882540-f9a25657-0d76-4e0e-9092-a1ff18edbb88.png)


## The transaction hash from the console output (in text format).

```
0xaee5677cfc00fbde262caad2f0713c02fe8c62eaef0f88cf97874cf7e3dbd35c
```

## The contract address that you called (in text format).

```
0x76FD5635fcf346A43E393B0a122358A2f78FB755
```

## The ABI for contract you made a call on (in text format).

```
[
  {
    "inputs": [],
    "name": "nextId",
    "outputs": [
      {
        "internalType": "uint256",
        "name": "",
        "type": "uint256"
      }
    ],
    "stateMutability": "view",
    "type": "function"
  },
  {
    "inputs": [
      {
        "internalType": "uint256",
        "name": "",
        "type": "uint256"
      }
    ],
    "name": "players",
    "outputs": [
      {
        "internalType": "uint256",
        "name": "id",
        "type": "uint256"
      },
      {
        "internalType": "string",
        "name": "name",
        "type": "string"
      },
      {
        "internalType": "string",
        "name": "teamName",
        "type": "string"
      }
    ],
    "stateMutability": "view",
    "type": "function"
  },
  {
    "inputs": [
      {
        "internalType": "string",
        "name": "name",
        "type": "string"
      },
      {
        "internalType": "string",
        "name": "teamName",
        "type": "string"
      }
    ],
    "name": "add",
    "outputs": [],
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "inputs": [
      {
        "internalType": "uint256",
        "name": "idd",
        "type": "uint256"
      },
      {
        "internalType": "string",
        "name": "name",
        "type": "string"
      },
      {
        "internalType": "string",
        "name": "teamName",
        "type": "string"
      }
    ],
    "name": "update",
    "outputs": [],
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "inputs": [
      {
        "internalType": "uint256",
        "name": "id",
        "type": "uint256"
      }
    ],
    "name": "remove",
    "outputs": [],
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "inputs": [
      {
        "internalType": "uint256",
        "name": "id",
        "type": "uint256"
      }
    ],
    "name": "read",
    "outputs": [
      {
        "components": [
          {
            "internalType": "uint256",
            "name": "id",
            "type": "uint256"
          },
          {
            "internalType": "string",
            "name": "name",
            "type": "string"
          },
          {
            "internalType": "string",
            "name": "teamName",
            "type": "string"
          }
        ],
        "internalType": "struct Ballondor.player",
        "name": "",
        "type": "tuple"
      }
    ],
    "stateMutability": "view",
    "type": "function"
  }
]
```

## Your Tron address (in text format).

```
TRJFDKjuSjcjTCEurbw758UHEqxJVRQXRu
```

---
sidebar_position: 2
---

# Upgrading from Share Modal v2

This is a brief summary of how to move from the EVM Basic conditions used in the **[old Lit Share Modal](https://www.npmjs.com/package/lit-share-modal)** to the new Unified Access Control Condition format used in the new v3 build.  **[More information on Unified Access Control Conditions can be found here](https://developer.litprotocol.com/docs/AccessControlConditions/unifiedAccessControlConditions)**

There are two changes to be aware: first, the additions of a `chain` property within each individual condition of itself defines what kind of AuthSig is required to register it, and, second, a change in the syntax of the object passed to the `saveSigningConditions` method in the `litNodeClient`. 

### New `chain` property

Within the individual conditions, a new `chain` property has been added.  The share modal currently supports **Solana** and **EVM** chains, which use the values `'solRpc'` and `'ethereum'` to differentiate.

Previous (EVM only) Access Control Condition format:

```
const accessControlConditions = [
  {
    contractAddress: '0x3110c39b428221012934A7F617913b095BC1078C',
    standardContractType: 'ERC1155',
    chain,
    method: 'balanceOf',
    parameters: [
      ':userAddress',
      '9541'
    ],
    returnValueTest: {
      comparator: '>',
      value: '0'
    }
  }
]
```

New Unified Access Control Conditions format (for EVM):

```
const unifiedAccessControlConditions = [
  {
    chain: 'ethereum',
    contractAddress: '0x3110c39b428221012934A7F617913b095BC1078C',
    standardContractType: 'ERC1155',
    chain,
    method: 'balanceOf',
    parameters: [
      ':userAddress',
      '9541'
    ],
    returnValueTest: {
      comparator: '>',
      value: '0'
    }
  }
]
```

Note the addition of the `chain` property, which can also be used to denote **Solana** conditions:

```
const unifiedAccessControlConditions = [
  {
    conditionType: 'solRpc',
    method: ',
    params: [
      :userAddress'
    ],
    chain: 'solana',
    returnValueTest: {
      key: ',
      comparator: '=',
      value: '6XmeyeYtSd31Eby2syaRkpXKY2GMMd3n3MEwTM5B7riD'
    }
  }
]
```

Conditions from EVM chains can be combined with Solana using **AND/OR** operators: 

```
const unifiedAccessControlConditions = [
  {
    chain: 'ethereum',
    contractAddress: '0x3110c39b428221012934A7F617913b095BC1078C',
    standardContractType: 'ERC1155',
    chain,
    method: 'balanceOf',
    parameters: [
      ':userAddress',
      '9541'
    ],
    returnValueTest: {
      comparator: '>',
      value: '0'
    }
  }
  { operator: 'or' },
  {
    conditionType: 'solRpc',
    method: ',
    params: [
      :userAddress'
    ],
    chain: 'solana',
    returnValueTest: {
      key: ',
      comparator: '=',
      value: '6XmeyeYtSd31Eby2syaRkpXKY2GMMd3n3MEwTM5B7riD'
    }
  }
]
```

### `saveSigningCondition` syntax change

A separate AuthSig is required for each condition type included in a **Unified Access Control Conditions** array.

Previous (EVM only) Access Control Condition format:

```
var ethAuthSig = await LitJsSdk.checkAndSignAuthMessage({
  chain: "ethereum",
});

await litNodeClient.saveSigningCondition({
  accessControlConditions: accessControlConditions,
  authSig: ethAuthSig,
  resourceId,
});
```

The new format passes in a different AuthSig for each condition type under a specific property name.  Note too, the change from `accessControlConditions` to `unifiedAccessControlConditions`.  Here is an example of the new version:

```
var solAuthSig = await LitJsSdk.checkAndSignAuthMessage({
  chain: "solana",
});

var ethAuthSig = await LitJsSdk.checkAndSignAuthMessage({
  chain: "ethereum",
});

await litNodeClient.saveSigningCondition({
  unifiedAccessControlConditions,
  authSig: {
    solana: solAuthSig,
    ethereum: ethAuthSig, // note that the key here is "ethereum" for any and all EVM chains.  If you're using Polygon, for example, you should still have "ethereum" here.
  },
  resourceId,
});
```

**[More information on Unified Access Control Conditions can be found here](https://developer.litprotocol.com/docs/AccessControlConditions/unifiedAccessControlConditions)**

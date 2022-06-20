---
sidebar_position: 2
---

# Upgrading from Share Modal v2

This is a brief summary of how to move from the (EVM only) **Access Control Conditions** format used in the **[old Lit Share Modal](https://www.npmjs.com/package/lit-share-modal)** to the new **Unified Access Control Condition** format used in the new v3 build.  **[More information on Unified Access Control Conditions can be found here](https://developer.litprotocol.com/docs/AccessControlConditions/unifiedAccessControlConditions)**

There are two changes to be aware: first, the additions of a `chain` property within each individual condition of itself defines what kind of AuthSig is required to register it, and, second, a change in the syntax of the object passed to the `saveSigningConditions` method in the `litNodeClient`. 

### New `chain` property

Within the individual conditions, a new `chain` property has been added.  The share modal currently supports **Solana** and **EVM** chains, which use the values `'solRpc'` and `'evmBasic'` to differentiate.

Old (EVM only) **Access Control Conditions** format for checking a wallet with address 0x50e2dac5e78B5905CB09495547452cEE64426db2.

```
const accessControlConditions = [
  {
    contractAddress: '',
    standardContractType: '',
    chain: 'ethereum',
    method: '',
    parameters: [
      ':userAddress',
    ],
    returnValueTest: {
      comparator: '=',
      value: '0x50e2dac5e78B5905CB09495547452cEE64426db2'
    }
  }
]
```

New **Unified Access Control Conditions** format far same condition as above.  Note the addition of the `chain` property.

```
const unifiedAccessControlConditions = [
  {
    conditionType: 'evmBasic',
    chain: 'ethereum',
    contractAddress: '',
    standardContractType: '',
    method: '',
    parameters: [
      ':userAddress',
    ],
    returnValueTest: {
      comparator: '=',
      value: '0x50e2dac5e78B5905CB09495547452cEE64426db2'
    }
  }
]
```

The new format can also be used to denote **Solana** conditions.  Note the change of the chain condition to `'solRpc'`.  Here is an example of checking for a wallet with address 88PoAjLoSqrTjH2cdRWq4JEezhSdDBw3g7Qa6qKQurxA.

```
const unifiedAccessControlConditions = [
  {
    conditionType: 'solRpc',
    method: "",
    params: [
      ":userAddress"
    ],
    chain: 'solana',
    returnValueTest: {
      key: "",
      comparator: "=",
      value: "88PoAjLoSqrTjH2cdRWq4JEezhSdDBw3g7Qa6qKQurxA",
    },
  },
  }
]
```

Conditions from EVM chains can be combined with Solana using **AND/OR** operators.  This example checks for ownership of an EVM wallet of address 0x50e2dac5e78B5905CB09495547452cEE64426db2 **OR** ownership of a Solana wallet with address 6XmeyeYtSd31Eby2syaRkpXKY2GMMd3n3MEwTM5B7riD.

```
const unifiedAccessControlConditions = [
  {
    conditionType: 'evmBasic',
    contractAddress: '',
    standardContractType: '',
    chain: 'ethereum',
    method: '',
    parameters: [
      ':userAddress',
    ],
    returnValueTest: {
      comparator: '=',
      value: '0x50e2dac5e78B5905CB09495547452cEE64426db2'
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

Old (EVM only) **Access Control Condition** format:

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

New **Unified Access Control Conditions** format. The new format passes in a different AuthSig for each condition type under a specific property name.  Note too, the change from `accessControlConditions` to `unifiedAccessControlConditions`.  Here is an example of the new version:

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

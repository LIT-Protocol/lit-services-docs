---
sidebar_position: 2
---

# Updates

### 2022-6-29

- Removed `chain` property from `onUnifiedAccessControlConditionsSelected` and replaced it with `chains`, which is an
  array of all the chain types in a given set of conditions e.g. `['ethereum', 'solana', 'polygon', 'xdai']`.
- Added property `authSigTypes` to `onUnifiedAccesControlConditionsSelected` that will contain the types of authSigs
  that need to be passed into `saveSigningCondition.authSigs` and `getSignedToken.authSigs`.

### 2022-6-28

- Added ability to configure initial state capability by using props `injectInitialState`
  , `initialUnifiedAccessControlConditions`
  , `initialFlow`, `initialCondition`, and `initialState`.
---
sidebar_position: 2
---

# Updates

[//]: # (### Planned features.)

[//]: # ()

[//]: # (- ability to offer a store wide discount)

[//]: # (- letting merchants set a timeframe for the length of an offer)

### Recent Additions

<strong>8-9-2022</strong>
  <ul>
    <li>easily added app block allows users to connect their wallet in-page to see which offers they qualify for, as well as discounts they missed out on or have already redeemed</li>
    <li>app block can be customized through the shop editor to match your theme</li>
    <li>the number of times users can redeem an offer can be limited based on NFT ID for Ethereum and Polygon gates</li>
    <li>if users have more than one NFT that qualifies for an offer, they can choose which one to use</li>
    <li>the number of times users can redeem an offer can be limited based on wallet address for all EVM chains and Solana</li>
    <li>users and redemption status can be added, deleted, or edited</li>
    <li>products can be bundled together for package deals</li>
    <li>relevant information about the purchaser (wallet address, NFT ID, type of offer, etc...) is included in the draft order metadata for reference</li>
    <li>draft orders created with Lit Token Access can be easily located by searchable tags in the Shopify Orders menu</li>  
  </ul>

<strong>6-8-2022</strong>
<ul>
  <li>
  <strong>IMPORTANT!: </strong> if something breaks regarding this update please send a message with
  details regarding the steps taken, chain, token type, and anything else relevant to <strong>
  shopifysupport@litprotocol.com</strong>
  We've tested this thing to ensure it's backwards compatible and won't
  mess anything up, but we're exploring new feature territory and doing a significant update behind the
  scenes at the same time and odds are something could be funky. Let us know if that happens and we'll
  get on fixing it.
  </li>
  <li>
  <strong>Solana support is now a thing:</strong> We are happy to announce that Solana support is live
  in the Lit Token Gating app! The modal used to create the conditions has changed as well, and now
  offers significantly more capabilities than the previous version. A partial
  playground is available [here]('https://lit-share-modal-v3-playground.netlify.app') where you can experiment with the
  new features.
  Currently, there isn't a good way to permanently alter settings like default chain, but
  that will be coming soon.
  </li>
  <li>
  <strong>Update to Vite:</strong> behind the scenes, we've updated the app from NextJS to Vite.
  What does this mean for your store? Hopefully nothing, but it makes our lives easier and
  took a bit of time so we thought we'd say something about it.
  </li>
</ul>

<strong>5-9-2022</strong>

- <strong>Limit on number of redemptions per wallet</strong>: in
  the <strong>Create Token Access</strong>
  modal there is now an additional input that lets you dictate
  how many times a wallet can redeem a given offer. It is wallet
  based right now, so there is still the issue of someone taking
  an NFT, moving it to another wallet and checking out again. We
  will be adding a redemption limiter based on NFT ID in the
  future, but it's not quite ready yet.
- Redo styling for verification and redemption flow to fix the mobile view.

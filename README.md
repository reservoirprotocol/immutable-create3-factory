# Immutable CREATE3 factory

A fork of https://github.com/zeframlou/create3-factory which doesn't depend on any particular deployer. This is achieved by using a permissionless deployment method based on [Seaport's CREATE2 factory](https://github.com/ProjectOpenSea/seaport/blob/main/docs/Deployment.md#setting-up-factory-on-a-new-chain).

Anyone can deploy the Immutable CREATE3 factory at the canonical address `0x0000000000000A9eFE52e741bcB25da0E4438E71` on any chain by following the deployment instructions:

```bash
# Trigger the deployment
export RPC_URL=
export PRIVATE_KEY=
npx hardhat run --network current ./scripts/deploy.ts

# Optionally verify the contract
export ETHERSCAN_API_KEY=
npx hardhat --network current verify 0x0000000000000A9eFE52e741bcB25da0E4438E71
```

The exact deployment steps are mentioned in `./scripts/deploy.ts`:

1. Send 0.01 ETH to `KeylessCreate2Deployer`
2. Deploy `KeylessCreate2` via a pre-signed legacy (non-EIP155) transaction
3. Deploy `InefficientImmutableCreate2Factory` via `KeylessCreate2`
4. Deploy `ImmutableCreate2Factory` via `InefficientImmutableCreate2Factory`
5. Deploy `Create3Factory` via `ImmutableCreate2Factory`

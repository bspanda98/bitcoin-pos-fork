git clone https://github.com/bitcoin/bitcoin.git

# Rename all content of files over terminal
```
find . -type f -print0 | xargs -0 sed -i 's/BitCoin/NewCoin/g'
find . -type f -print0 | xargs -0 sed -i 's/bitcoin/newcoin/g'
find . -type f -print0 | xargs -0 sed -i 's/BITCOIN/NEWCOIN/g'
find . -type f -print0 | xargs -0 sed -i 's/btc/new/g'
find . -type f -print0 | xargs -0 sed -i 's/BTC/NEW/g'
find . -type f -print0 | xargs -0 sed -i 's/9696/3131/g'
find . -type f -print0 | xargs -0 sed -i 's/9697/3132/g'
```
# genesis setup
# src/chainparams.cpp
paste this at line no 21
```
void GenesisGenerator(CBlock genesis) {
    printf("Searching for genesis block...\n");

    uint256 hash;
    bool fNegative;
    bool fOverflow;
    arith_uint256 bnTarget;
    bnTarget.SetCompact(genesis.nBits, &fNegative, &fOverflow);

    while(true)
    {
        hash = genesis.GetHash();
        if (UintToArith256(hash) <= bnTarget)
            break;
        if ((genesis.nNonce & 0xFFF) == 0)
        {
            printf("nonce %08X: hash = %s (target = %s)\n", genesis.nNonce, hash.ToString().c_str(), bnTarget.ToString().c_str());
        }
        ++genesis.nNonce;
        if (genesis.nNonce == 0)
        {
            printf("NONCE WRAPPED, incrementing time\n");
            ++genesis.nTime;
        }
    }

    printf("block.nNonce = %u \n", genesis.nNonce);
    printf("block.GetHash = %s\n", genesis.GetHash().ToString().c_str());
    printf("block.MerkleRoot = %s \n", genesis.hashMerkleRoot.ToString().c_str());
}
```
#change pszTimestamp
#change  pchMessageStart 136,224,309
#change consensus.powLimit = uint256S("003fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff");
#change hashGenesisBlock 235,322
#change hashMerkleRoot 236,323
#change checkpointData = 
#change seeds
# src/chainparamsbase.cpp
chabge only numbers
#CBaseChainParams::MAIN
#CBaseChainParams::TESTNET
#CBaseChainParams::REGTEST


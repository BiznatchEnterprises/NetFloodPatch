# NetFloodPatch

Bitcoin core 10 - Network Flood Attack Patch 1



Edit net.cpp

Search for: SocketSendData(

====================================

CHANGE:

	const CSerializeData &data = *it;
  
	assert(data.size() > pnode->nSendOffset);

======================================

TO:
    
    const CSerializeData &data = *it;

                    //-------------------------------------------------------------------
                    // BATA CORE 10.4 NetFlood PATCH #1 - June 30, 2017 - Biznatch Enterprises
                    // Prevent Network Flooding trying to sync old wallets
                    // HIGH bandwidth use triggers verify CORE10 CHECKPOINT
                    // after active conntaction disconnection and removal if startheight is below checkpoint
                    //
                    if (pnode->nSendSize > 10000) { 
                        if (pnode->nRecvBytes > 10000) { 
                            if (pnode->nStartingHeight < 700000) { 
                                // remove from vNodes
                                vNodes.erase(remove(vNodes.begin(), vNodes.end(), pnode), vNodes.end());

                                // release outbound grant (if any)
                                 pnode->grantOutbound.Release();

                                // close socket and cleanup
                                pnode->CloseSocketDisconnect();
                            }
                        }
                    }
                    //-------------------------------------------------------------------

        assert(data.size() > pnode->nSendOffset);
        
=======================================  
        
make        



# Contribute to development

Please donate cryptocoins:

Bitcoin: 1F4TunADj7BMkYCpWKwsmtxixwdVG9WS1n
BitConnect: 8XZfQco6HjE7HhyHDmJEubQVKZLSP8jDUs
Litcoin: Lfo8x4dazSnoJwsXG4KG94r4UeDUCrJE3S
Peercoin: PJQndzQx8ZT8seHSMAKnLXSSX6muSq9kkF
Bata: BF7yRP194YfkRG2X3sRjqJWxbYkEMysn65
Dash: XtL8UPrZnfhwgq5dEJyTgi8MmjcxFM49qx
Stratis: SiEboTxzWn7XFp49Mi8vZKM5pYYN8RquTg
Pivx: DBrnFPRsviQKtKGqy1CGVeezVLxWMNDCzx
Zcoin: a9NvxHohyZ9croSxtxfwBTnrH5gsvnQcU5
Crypto Bullion: 5hV1b1Z1SowecPPbWtRDLhASKY4qM9ZYpb
GoldCoin: E3Rw5FP2mUBE5beGaiiWRbPVpqA5yrJhg7

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


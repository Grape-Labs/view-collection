const fetchWalletCollection = async () => { // TODO: add error handling
        const body = {
          method: "getTokenAccountsByOwner",
          jsonrpc: "2.0",
          params: [
            publicKey, // The Wallet Public Key we are querying (this can be obtained directly from useWallet() from the connected wallet / or manually setting this String value)
            { programId: "<Pubkey of the Token program ID that owns the accounts, as base-58 encoded string>" },
            { encoding: "jsonParsed", commitment: "processed" },
          ],
          id: "<Set your id here>", // an internal ID so you can reference the call you are making later on
        };
        
        const response = await fetch("https://solana-api.projectserum.com/", {
          method: "POST",
          body: JSON.stringify(body),
          headers: { "Content-Type": "application/json" },
        });
    
        const json = await response.json();
        try{
            const resultValues = json.result.value
            
            let walletCollection = new Array();
            let wallet = resultValues && resultValues?.map((collectionInfo: any) => {
                (+collectionInfo.account.data.parsed.info.tokenAmount.amount == 1) &&
                    (+collectionInfo.account.data.parsed.info.tokenAmount.decimals == 0) && 
                        walletCollection.push(collectionInfo);    
                        return collectionInfo;
            });
            return walletCollection;
        } catch(e){console.log(e);}
        return [];
    };

for github



-------------------------------------------------




----------------------------------------------------------
echo 'export CELESTIA_CHAIN='$CELESTIA_CHAIN >> $HOME/.bash_profile
echo 'export CELESTIA_NODENAME='${CELESTIA_NODENAME} >> $HOME/.bash_profile
echo 'export CELESTIA_WALLET='${CELESTIA_WALLET} >> $HOME/.bash_profile
source $HOME/.bash_profile

------------------------------------------------


-------------------------------------
cp $HOME/networks/mamaki/genesis.json $HOME/.celestia-app/config/

---------------------------------------
sed -i 's/mode = \"full\"/mode = \"validator\"/g' $HOME/.celestia-app/config/config.toml

---------------------------------------------
BOOTSTRAP_PEERS=$(curl -sL https://raw.githubusercontent.com/celestiaorg/networks/master/mamaki/bootstrap-peers.txt | tr -d '\n')

--------------------------------------------------
echo $BOOTSTRAP_PEERS

------------------------------------------------
sed -i.bak -e "s/^bootstrap-peers *=.*/bootstrap-peers = \"$BOOTSTRAP_PEERS\"/" $HOME/.celestia-app/config/config.toml

-----------------------------------------------------------
sed -i 's/timeout-commit = ".*/timeout-commit = "25s"/g' $HOME/.celestia-app/config/config.toml
sed -i 's/peer-gossip-sleep-duration *=.*/peer-gossip-sleep-duration = "2ms"/g' $HOME/.celestia-app/config/config.toml

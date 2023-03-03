# Nolus Protocol testnet.
[WebSite](https://nolus.io) \
[GitHub](https://github.com/Nolus-Protocol/nolus-core) \
[Official documentation](https://docs-nolus-protocol.notion.site/Run-a-Full-Node-7a92545223e7483bb4a02cce30b53aa8)
=
[EXPLORER 1](https://explorer.stavr.tech/nolus-testnet/staking) \
[EXPLORER 2](https://exp.utsa.tech/nolus-test)
=

- **Minimum hardware requirements**:

| Node Type |CPU | RAM  | Storage  | 
|-----------|----|------|----------|
| Testnet   |   2|  4GB | 120GB    |

## SnapShot guide
```python
# download the snapshot
wget http://95.31.16.222:18080/nolus20230303.tar.lz4

# if Nolus was already on your machine, stop your Nolus service
sudo systemctl stop nolusd
# AND make sure there is no process running that might try to write to the database
ps -ef | grep nolus

# make sure your nolus data directory is clean (let us assume <NOLUS_HOME> is your root Nolus directory)
# make sure to backup your priv_validator_state.json file before deleting the contents of the data directory
mv <NOLUS_HOME>/data/priv_validator_state.json <NOLUS_HOME>
rm -rf <NOLUS_HOME>/data/

# make sure you have lz4 installed
sudo apt-get install lz4

# decompress the archive
lz4 -c -d nolus20230303.tar.lz4  | tar -x -C <NOLUS_HOME>

# copy back the priv_validator_state.json file
rm <NOLUS_HOME>/data/priv_validator_state.json
mv <NOLUS_HOME>/priv_validator_state.json <NOLUS_HOME>/data/

# start the Nolus service 
sudo systemctl restart nolusd && journalctl -u nolusd -f -o cat

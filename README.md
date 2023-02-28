# nibiru-itn


https://nibiru.fi/blog/posts/007-itn-1.html

nibiru 벨리데이터 한국어 세팅입니다
테넷 itn-1 체인에서 시작했습니다.
1.  시스템 업데이트 및 nibid 설치
`sudo apt update && sudo apt upgrade --yes`
`curl -s https://get.nibiru.fi/@v0.19.2! | bash`
2. 체인 설정
`curl -s https://get.nibiru.fi/@v0.19.2! | bash`
`nibid keys add <key-name>` #지갑을 새로만드는것


#기존 지갑에서 불러오기 #니모닉으로
`nibid keys add wallet --recover --keyring-backend os `




#제네시스 파일다운 및 설정
`NETWORK=nibiru-itn-1
curl -s https://networks.itn.nibiru.fi/$NETWORK/genesis > $HOME/.nibid/config/genesis.json`

`NETWORK=nibiru-itn-1
sed -i 's|seeds =.*|seeds = "'$(curl -s https://networks.itn.nibiru.fi/$NETWORK/seeds)'"|g' $HOME/.nibid/config/config.toml
sed -i 's/minimum-gas-prices =.*/minimum-gas-prices = "0.025unibi"/g' $HOME/.nibid/config/app.toml
NETWORK=nibiru-itn-1
sed -i 's|enable =.*|enable = true|g' $HOME/.nibid/config/config.toml
sed -i 's|rpc_servers =.*|rpc_servers = "'$(curl -s https://networks.itn.nibiru.fi/$NETWORK/rpc_servers)'"|g' $HOME/.nibid/config/config.toml
sed -i 's|trust_height =.*|trust_height = "'$(curl -s https://networks.itn.nibiru.fi/$NETWORK/trust_height)'"|g' $HOME/.nibid/config/config.toml
sed -i 's|trust_hash =.*|trust_hash = "'$(curl -s https://networks.itn.nibiru.fi/$NETWORK/trust_hash)'"|g' $HOME/.nibid/config/config.toml`



#시작하기
`nibid start`

#싱크 된 이후 벨리데이터 생성하기
`nibid config chain-id nibiru-itn-1`

`nibid tx staking create-validator \
--amount 10000000unibi \
--commission-max-change-rate "0.1" \
--commission-max-rate "0.20" \
--commission-rate "0.1" \
--min-self-delegation "1" \
--details "put your validator description there" \
--pubkey=$(nibid tendermint show-validator) \
--moniker <your_moniker> \
--chain-id nibiru-itn-1 \
--gas-prices 0.025unibi \
--from <지갑이름>`

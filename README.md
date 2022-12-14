# Monitor-for-haqq-validator-node
1. Install node exporter on validator node
- Run command to download and install 
#wget -O install_exporters.sh https://raw.githubusercontent.com/kj89/cosmos_node_monitoring/master/install_exporters.sh && chmod +x install_exporters.sh && ./install_exporters.sh
- Configure:
bond_denom: aISLM
bench_prefix: haqq
rpc_port: 26657
grpc_port: 9090
- Enable prometheus:
#sed -i -e "s/prometheus = false/prometheus = true/" $HOME/.sei/config/config.toml

2. Install monitoring on other machine
- Run command to download and install monitoring (docker-compose)
#wget -O install_monitoring.sh https://raw.githubusercontent.com/kj89/cosmos_node_monitoring/master/install_monitoring.sh && chmod +x install_monitoring.sh && ./install_monitoring.sh
- Configure for telegram information
#cp $HOME/cosmos_node_monitoring/config/.env.example $HOME/cosmos_node_monitoring/config/.env
#nano $HOME/cosmos_node_monitoring/config/.env
TELEGRAM_ADMIN = id_of_telegram_user
TELEGRAM_TOKEN=token of new bot

#echo "export $(xargs < $HOME/cosmos_node_monitoring/config/.env)" > $HOME/.bash_profile
#source $HOME/.bash_profile
- Set information for validator node into docker configuration

#VALIDATOR_IP=NODE_IP    
#VALIDATOR_ADDR=VALIDATOR_ADDRESS  
#WALLET_ADDRESS=WALLER_ADDRESS  
#PROJECT_NAME=PROJECT_NAME  #haqq

#$HOME/cosmos_node_monitoring/add_validator.sh $VALIDATOR_IP $VALIDATOR_ADDR $WALLET_ADDRESS $PROJECT_NAME
Start docker-compose
#cd $HOME/cosmos_node_monitoring
#sudo docker-compose up -d

3. Configure on grafana.com
- First need register an account from grafana.com to get UID
<img width="416" alt="image" src="https://user-images.githubusercontent.com/103411238/190847878-e8219d36-6697-4693-b93c-8554ffe94037.png">
- Open http://125.212.225.201:9999	with default admin/admin to change password 
- Configure for Dashboard - Import - import id which register at first step
<img width="416" alt="image" src="https://user-images.githubusercontent.com/103411238/190847927-6afe1487-b321-4236-a9b0-d3e5ff45264d.png">
- Choose Prometheus 
<img width="415" alt="image" src="https://user-images.githubusercontent.com/103411238/190847939-2845d906-6313-434d-8a02-3f87ac4b8eca.png">
Then access to Dashboard
<img width="415" alt="image" src="https://user-images.githubusercontent.com/103411238/190847958-e1f198af-bd33-4589-9b2e-f6275551cff8.png">
Configure for outsource alarm to monitor (For this case use Telegram)
- Access Alerting - Alert rules and notifications
<img width="416" alt="image" src="https://user-images.githubusercontent.com/103411238/190847965-a1c65662-17d1-45fc-846b-f57c672b11fe.png">
- Choose Contact points - add new contact point
    - Input Name, contract point type (choose email or telegram or any method for you) 
    - Save contact points.   
    <img width="415" alt="image" src="https://user-images.githubusercontent.com/103411238/190847981-0210d22f-3f5d-46ea-9932-975f61d5eaeb.png">
- Choose Notification policies - Edit - Choose default contact point type
<img width="416" alt="image" src="https://user-images.githubusercontent.com/103411238/190847994-77cacf7b-3bdb-4a01-8364-2c67cc8f6678.png">

2. Configure for telegram
- Open chat with @userinfobot, run command /start to get telegram user information
<img width="416" alt="image" src="https://user-images.githubusercontent.com/103411238/190848008-fc7bfcbb-fdf3-416b-b2a4-38e221c4c96c.png">
- Open chat with @botfather to setup new bot:
  /start
  /newbot
  input name of bot
  get token
  <img width="415" alt="image" src="https://user-images.githubusercontent.com/103411238/190848019-195215e4-8906-47b6-a20b-ff1bc2f8de4b.png">
Take note for token to access HTTP API (this token will configure t Grafana.com
- On telegram bot haqq_pw to monitor alarm from validator node
<img width="416" alt="image" src="https://user-images.githubusercontent.com/103411238/190848035-dbb08a5f-d11f-4350-9157-e84ca3548ebd.png">

Source: Using URL
https://github.com/kj89/cosmos_node_monitoring
https://grafana.com/docs/grafana/latest/alerting/set-up/provision-alerting-resources/
For grafana URL monitor haqq validator node: http://125.212.225.201:9999/d/rYdddlPWk/haqq-phuongwoo-node-exporter-full?orgId=1&refresh=1m

# Dowmload
        sudo wget https://github.com/subspace/subspace/releases/download/gemini-2a-2022-sep-06/subspace-node-ubuntu-x86_64-gemini-2a-2022-sep-06 && sudo wget https://github.com/subspace/subspace/releases/download/gemini-2a-2022-sep-06/subspace-farmer-ubuntu-x86_64-gemini-2a-2022-sep-06

        sudo mv subspace-node-ubuntu-x86_64-gemini-2a-2022-sep-06 /usr/local/bin/subspace-node && sudo mv subspace-farmer-ubuntu-x86_64-gemini-2a-2022-sep-06 /usr/local/bin/subspace-farmer && sudo chmod +x /usr/local/bin/subspace*
# tạo systemd
     sudo tee /etc/systemd/system/subspace-node.service > /dev/null <<EOF
     [Unit]
     Description=Subspace Node 
     After=network.target

     [Service]
     User=root
     Type=simple
     ExecStart=/usr/local/bin/subspace-node --chain gemini-2a --execution wasm \
     --db-cache 1024 --max-runtime-instances 200 \
     --keep-blocks 1024 --pruning 1024 --validator --name <YOUR-NODE-NAME>
     Restart=on-failure
     LimitNOFILE=65535

     [Install]
     WantedBy=multi-user.target
     EOF

     sudo tee /etc/systemd/system/subspace-farmer.service > /dev/null <<EOF
     [Unit]
     Description=Subspaced Farm 
     After=network.target

     [Service]
     User=root
     Type=simple
     ExecStart=/usr/local/bin/subspace-farmer farm --reward-address <YOUR-WALLET-ADDRESS> --plot-size 100G
     Restart=on-failure
     LimitNOFILE=65535

     [Install] 
     WantedBy=multi-user.target
     EOF
# Run     
     sudo systemctl daemon-reload && sudo systemctl enable subspace-farmer.service && sudo systemctl enable subspace-node.service
     systemctl restart subspace-node.service 
     systemctl restart subspace-farmer.service 
     
     journalctl -u subspace-node.service -f -o cat
     journalctl -u subspace-farmer.service -f -o cat
# delete node
     sudo systemctl stop subspace-node.service subspace-farmer.service
     sudo systemctl disable subspace-node.service subspace-farmer.service
     rm -rf /root/.local/share/subspace-farmer/
     rm -rf /root/.local/share/subspace-node/
     rm -rf /etc/systemd/system/subspace-farmer.service /etc/systemd/system/subspace-node.service

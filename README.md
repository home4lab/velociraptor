# velociraptor

# download package
mkdir /etc/velociraptor

cd /etc/velociraptor

wget https://github.com/Velocidex/velociraptor/releases/download/v0.6.1-rc1/velociraptor-v0.6.1-rc2-linux-amd64

# make executable file
chmod +x velociraptor-v0.6.1-rc2-linux-amd64

# generate config file
./velociraptor-v0.6.1-rc2-linux-amd64 config generate > /etc/velociraptor/velociraptor.config.yaml

# create user admin
./velociraptor-v0.6.1-rc2-linux-amd64 --config /etc/velociraptor/velociraptor.config.yaml user add admin --role administrator

# start the frontend
./velociraptor-v0.6.1-rc2-linux-amd64 --config /etc/velociraptor/velociraptor.config.yaml frontend -v

# optional
install systemd service for velociraptor 

cp velociraptor-v0.6.1-rc2-linux-amd64 /usr/local/bin/velociraptor

vim /lib/systemd/system/velociraptor.service

    [Unit]
    Description=Velociraptor linux amd64
    After=syslog.target network.target
    
    [Service]Type=simple
    Restart=always
    RestartSec=120
    LimitNOFILE=20000
    Environment=LANG=en_US.UTF-8
    ExecStart=/usr/local/bin/velociraptor --config /etc/velociraptor/velociraptor.config.yaml frontend -v

    [Install]
    WantedBy=multi-user.target




systemctl daemon-reload

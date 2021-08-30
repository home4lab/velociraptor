# velociraptor

# download package
mkdir /etc/velociraptor

cd /etc/velociraptor

wget https://github.com/Velocidex/velociraptor/releases/download/v0.6.1-rc1/velociraptor-v0.6.1-rc2-linux-amd64

# make executable file
mv velociraptor-v0.6.1-rc2-linux-amd64 velociraptor
chmod +x velociraptor

# generate config file
./velociraptor config generate > /etc/velociraptor.config.yaml

# create user admin
./velociraptor --config /etc/velociraptor.config.yaml user add admin --role administrator

# start the frontend
./velociraptor --config /etc/velociraptor.config.yaml frontend -v

# enable self signed ssl
vim /etc/velociraptor.config.yaml

    nonce: B6yeXfJZ2Ss=
    **use_self_signed_ssl: true**
    writeback_darwin: /etc/velociraptor.writeback.yaml
    writeback_linux: /etc/velociraptor.writeback.yaml
    writeback_windows: $ProgramFiles\Velociraptor\velociraptor.writeback.yaml
    tempdir_windows: $ProgramFiles\Velociraptor\Tools


# optional
# create installation debian package for client and server
./velociraptor --config server.config.yaml debian client

./velociraptor --config server.config.yaml debian server
# install systemd service for velociraptor

cp velociraptor /usr/local/bin/

vim /lib/systemd/system/velociraptor.service

    [Unit]
    Description=Velociraptor linux amd64
    After=syslog.target network.target
    
    [Service]Type=simple
    Restart=always
    RestartSec=120
    LimitNOFILE=20000
    Environment=LANG=en_US.UTF-8
    ExecStart=/usr/local/bin/velociraptor --config /etc/velociraptor.config.yaml frontend -v

    [Install]
    WantedBy=multi-user.target




systemctl daemon-reload

systemctl enable --now velociraptor 

systemctl status velociraptor

# references
https://kifarunix.com/install-and-setup-velociraptor-on-ubuntu/

# top level corrensponds to the type of information that velociraptor collect:

File - Access the file system using the filesystem API

NTFS - Access the file system using raw NTFS parsing ( Windows Only )

Registry - Access the Windows Registry using the Registry API ( Windows Only )

Artifacts - A view of all artifacts collected from the client

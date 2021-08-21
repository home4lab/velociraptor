# velociraptor

# download package
mkdir velociraptor
cd velociraptor
wget https://github.com/Velocidex/velociraptor/releases/download/v0.6.1-rc1/velociraptor-v0.6.1-rc2-linux-amd64

# make executable file
chmod +x velociraptor-v0.6.1-rc2-linux-amd64

# generate config file
./velociraptor-v0.6.1-rc2-linux-amd64 config generate > /etc/velociraptor.config.yaml

# create user admin
./velociraptor-v0.6.1-rc2-linux-amd64 --config /tmp/velociraptor/velociraptor.config.yaml user add admin --role administrator

# start the frontend
./velociraptor-v0.6.1-rc2-linux-amd64 --config /tmp/velociraptor/velociraptor.config.yaml frontend -v

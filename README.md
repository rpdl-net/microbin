microbin was created by [Dániel Szabó](https://github.com/szabodanika/microbin), this is a fork.  
microbin was made available under the [BSD 3-Clause License](LICENSE).

## requirements
[rustup](https://rustup.rs/)

## installing in /opt/microbin
```
useradd microbin --system
cd opt; git clone https://github.com/rpdl-net/microbin.git
cd microbin
cargo build --release
chown -R microbin:microbin /opt/microbin
./target/release/microbin -p 8080
```

## example /etc/systemd/system/microbin.service

the following disables file upload and runs a bare-bones pastebin

```
[Unit]
Description=MicroBin
After=network.target

[Service]
Type=simple
Restart=always
User=microbin
WorkingDirectory=/opt/microbin/
ExecStart=/opt/microbin/target/release/microbin --hide-logo --hide-footer --hash-ids --no-eternal-pasta --no-file-upload --no-listing --title bin.rpdl.net --public-path https://bin.rpdl.net --wide --highlightsyntax --enable-burn-after --gc-days 7

[Install]
WantedBy=multi-user.target
```

change the [favicon](templates/assets/favicon.ico)
add reverse proxy in front and you're done.

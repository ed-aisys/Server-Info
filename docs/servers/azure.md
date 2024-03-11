# Proxy Server

In the Network Center of The Infomatics Forum, there are times when we need to use a proxy server to connect to Gala/Jazz. Here are some solutions:

## OpenVPN (Official Method)

To set up OpenVPN, please follow the instructions provided by the school of Infomatics:

- [OpenVPN - How and Why | Documentation](https://computing.help.inf.ed.ac.uk/openvpn)

You can download the configuration files from:

- [OpenVPN configuration files | Documentation](https://computing.help.inf.ed.ac.uk/openvpn-config-files)

Additionally, I highly recommend using the OpenVPN Connect client. You can download it from: [OpenVPN Connect - VPN For Your Operating System | OpenVPN](https://openvpn.net/client/)

If you are using MacOS M-Series Chips (Apple Silicon), OpenVPN may not work properly. In that case, you might need to execute the following command as an administrator:

```bash
sudo launchctl load /Library/LaunchDaemons/org.openvpn.client.plist
```

## Wireguard (Most Recommended for users in the UK, US, or other European countries)

I have set up an Azure Education Server in London, which acts as a reverse proxy tunnel. There is also a backup server in Strasbourg, making this method highly robust and stable.

Azure server IP: `172.167.229.23`

Ed-AISys Username: `aisys`

Ed-AISys Password: `fsJKRs99$PHFy!b`

I have created a sub-network using Wireguard:

- jazz IP: `192.168.168.3`
- gala IP: `192.168.168.4`

You can configure your SSH file as follows:

```text
Host azure
    HostName  172.167.229.23
    User aisys

Host wgjazz
    HostName 192.168.168.3
    User user
    ProxyJump azure

Host wggala
    HostName 192.168.168.4
    User user
    ProxyJump azure
```

After adding your public key to both gala, jazz, and azure, you will be able to successfully log in using the following command:

```
ssh wgjazz
ssh wggala
```

## CloudFlare Zero Tier (Recommended for users in China or other Asian countries)

This method serves as a backup plan in case the previous services are somehow unavailable. If that happens, you can try the following steps:

1. Open `gala.chivier.site` or `jazz.chivier.site`.
2. Use CloudFlare Zero Tier to log in.
> One-click deployment of Xray to heroku   
  
* Use[Xray](https://github.com/XTLS/Xray-core)+caddy Simultaneously deploy the WS-transferred vmess vless trojan shadowsocks socks and other protocols  
* Support tor network, and can start xray and caddy through custom network configuration file to configure various functions on demand  
* Support storage of custom files, directory and account password are AUUID, the client must use TLS connection  
  
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)  
  
### Server
Click the purple `Deploy to Heroku` above, it will jump to the heroku app creation page, fill in the app name, select the node, modify some parameters and AUUID as needed, and click the deploy below to create the app to start the deployment  
If there is an error, you can try a few more times. After the deployment is completed, Your app was successfully deployed will be displayed at the bottom of the page.  
  * Click on Manage App to access the Config Vars item under Settings **View and reset parameters**  
  * Click Open app to jump[welcome page](/etc/CADDYIndexPage.md)domain name is heroku Assign a domain name,The format is`appname.herokuapp.com`,for client  
  * The default protocol password is $UUID，WS path is $UUID-[vmess|vless|trojan|ss|socks]Format
  
### client
* **Be sure to replace all appname.herokuapp.com with the project domain name assigned by heroku**  
* **Be sure to replace all 8f91b6a0-e8ee-11ea-adc1-0242ac120002 with the AUUID set during deployment**  
  
<details>
<summary>Xray</summary>

```bash
* Client Downloads: https://github.com/XTLS/Xray-core/releases
* Agency Agreement: vmess or vless
* address: appname.herokuapp.com
* port: 443
* Default UUID: 8f91b6a0-e8ee-11ea-adc1-0242ac120002
* encryption: none
* Transfer Protocol: ws
* camouflage type: none
* path: /8f91b6a0-e8ee-11ea-adc1-0242ac120002-vless // default vmess use/$uuid-vmess,vless use/$uuid-vless
* underlying transport security: tls
```
</details>
  
<details>
<summary>Trojan-go</summary>

```bash
* Client Downloads: https://github.com/p4gefau1t/trojan-go/releases
{
    "run_type": "client",
    "local_addr": "127.0.0.1",
    "local_port": 1080,
    "remote_addr": "appname.herokuapp.com",
    "remote_port": 443,
    "password": [
        "8f91b6a0-e8ee-11ea-adc1-0242ac120002"
    ],
    "websocket": {
        "enabled": true,
        "path": "/8f91b6a0-e8ee-11ea-adc1-0242ac120002-trojan",
        "host": "appname.herokuapp.com"
    }
}
```
</details>
  
<details>
<summary>Shadowsocks</summary>

```bash
* Client Downloads: https://github.com/shadowsocks/shadowsocks-windows/releases/
* server address: appname.herokuapp.com
* port: 443
* password: password
* encryption: chacha20-ietf-poly1305
* plug-in: xray-plugin_windows_amd64.exe  //plug-in https://github.com/shadowsocks/xray-plugin/releases Download and unzip it to shadowsocks same directory
* Plugin options: tls;host=appname.herokuapp.com;path=/8f91b6a0-e8ee-11ea-adc1-0242ac120002-ss
```
</details>
  
<details>
<summary>CloudFlare Workers Example</summary>

```js
const SingleDay = "appname.herokuapp.com"
const DoubleDay = "appname.herokuapp.com"
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url = new URL(event.request.url);
        url. hostname = "appname.herokuapp.com";
        let request = new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
</details>
  
> [More tutorials from enthusiastic netizens PR](/tutorial)

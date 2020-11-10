# 01 - Install

## NodeJS-v15
````bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_15.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_15.x | bash -
apt-get install -y nodejs
````

## version
````bash
node -v
````
* 14.15.0

[<img src="https://i.imgur.com/RuVALaD.png">](https://i.imgur.com/RuVALaD.png)

---

## npm

* File
    * /usr/lib/node_modules/npm
````bash
npm -v
````
* 6.14.8

[<img src="https://i.imgur.com/DBoNdwL.png">](https://i.imgur.com/DBoNdwL.png)

### install

* It will create after that. **node_modules**
* **NB**: if you change the code, so **rm -rf node_modules**
````bash
npm install
````
[<img src="https://i.imgur.com/sIvUTds.png">](https://i.imgur.com/sIvUTds.png)
[<img src="https://i.imgur.com/2JTtmfz.png">](https://i.imgur.com/2JTtmfz.png)

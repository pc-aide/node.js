# pizza-luvrs-s3

## Prereq

* aws configure

## File

* pizza-luvrs - root folder

## s3 as repository

* we will use **//<BucketName.com**
* e.g: //demo-01-nodejs.s3.ca-central-1.amazonaws.com/

### ./templates

1. pizza.make.hbs
````hbs
<img src='//demo-01-nodejs.s3.ca-central-1.amazonaws.com/toppings/{{previewImage}}' />
<script src="//demo-01-nodejs.s3.ca-central-1.amazonaws.com/js/make.js"></script>
````

2. layout.hbs
````hbs
<link rel="stylesheet" href="//demo-01-nodejs.s3.ca-central-1.amazonaws.com/css/stylesheet.css" />
````

3. index.hbs
````hbs
<img src="//demo-01-nodejs.s3.ca-central-1.amazonaws.com/logo_header.png" class="logo" />
````

4. ./partials/**header.hbs**
````hbs
<img class="background" src="//demo-01-nodejs.s3.ca-central-1.amazonaws.com/header.png" />
<a href="/"><img class="logo" src="//demo-01-nodejs.s3.ca-central-1.amazonaws.com/logo_header.png" /></a>
````

### ./assets/js

1. make.js
````js
img.src = '//demo-01-nodejs.s3.ca-central-1.amazonaws.com/toppings/' + val.image
````

### ./data/mock_pizzas

* each tag img, input value of bucket (without protocol https)
* same thing for :
    * best_pizza.json
    * filthy_rich.json
    * foul_wizard.json
    * lazer_pie.json
    * meat_haters.json
    * red_foreve.json

### upload
* upload js:
````bash
aws s3 cp ./assets/js s3://BucketName/js --recursive --exclude ".DS_Store"
````

### lib
* file **imageStore.js**
````js
const fileStore = require('./imageStoreFile')
const s3Store = require('./imageStoreS3')

function save (name, base64String) {
  const imageData = base64String.split('data:image/png;base64,')[1]
  return s3Store.save(name, imageData)
}

module.exports = {
  save
}
````

* Create this file ./lib/**imageStoreS3.js**
````js
const AWS = require('aws-sdk')
const s3 = new AWS.S3()

module.exports.save = (name, data) => {
  return new Promise((resolve, rejet) => {
    const params = {
      Bucket: 'demo-01-nodejs',
      Key: `pizzas/${name}.png`,
      Body: Buffer.from(data, 'base64'),
      ContentEncoding: 'base64',
      ContentType: 'image/png'
    }

    s3.putObject(params, (err, data) => {
      if (err) {
       rejet(err)
      } else {
       resolve(`//demo-01-nodejs.s3.ca-central-1.amazonaws.com/${params.Key}`)
      }
    })
  })
}
````

### Testing
* login with cred or create new one account:
  * ryan:pass
  
* make pizza:
* then Create

[<img src="https://i.imgur.com/OH5q6fJ.png">](https://i.imgur.com/OH5q6fJ.png)
[<img src="https://i.imgur.com/W5lU1A0.png">](https://i.imgur.com/W5lU1A0.png)

#### s3
* check out inside our bucket
* folder: pizzas/...

[<img src="https://i.imgur.com/QmJLRLX.png">](https://i.imgur.com/QmJLRLX.png)
[<img src="https://i.imgur.com/i9hOUxB.png">](https://i.imgur.com/i9hOUxB.png)

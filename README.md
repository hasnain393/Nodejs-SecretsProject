# Nodejs-SecretsProject
https://www.npmjs.com/package/mongoose-encryption

#mongoose-encryption
step1:
npm install mongoose-encryption

step2:
var mongoose = require('mongoose');
var encrypt = require('mongoose-encryption');

step3:
//note a normal json object is okay if we are not doing any encryption 
but if we are doing something with schema then we have to make object of mongoose Scheme
var userSchema = new mongoose.Schema({
    name: String,
    age: Number,
	password:String
});

step 4:

*************method1**********

// Add any other plugins or middleware here. For example, middleware for hashing passwords

var encKey = process.env.SOME_32BYTE_BASE64_STRING;
var sigKey = process.env.SOME_64BYTE_BASE64_STRING;

userSchema.plugin(encrypt, { encryptionKey: encKey, signingKey: sigKey });

// This adds _ct and _ac fields to the schema, as well as pre 'init' and pre 'save' middleware,
// and encrypt, decrypt, sign, and authenticate instance methods

**********or method2***************
Secret String Instead of Two Keys
For convenience, you can also pass in a single secret string instead of two keys.

var secret = process.env.SOME_LONG_UNGUESSABLE_STRING;
//adding encrypt package as a plugin
userSchema.plugin(encrypt, { secret: secret });
//to encrypt certain field 
userSchema.plugin(encrypt, { secret: secret ,encryptedFields: ['password']});


User = mongoose.model('User', userSchema);
-------------------------------------------------------------------------------------------------------------------------
#dotenv  (.ENV)

STEP 1:

Install
# with npm 
npm install dotenv

STEP 2:

Usage
As early as possible in your application, require and configure dotenv.
place the beow code at very top of app.js

require('dotenv').config()

Step 3:

Create a .env file in the root directory of your project. 
Add environment-specific variables on new lines in the form of NAME=VALUE. For example:

DB_HOST=localhost
DB_USER=root
DB_PASS=s1mpl3
NAME=Hasnain

process.env now has the keys and values you defined in your .env file.

Step 4:

TO ACCESS IN app.js 

console.log(process.env.NAME)

const db = require('db')
db.connect({
  host: process.env.DB_HOST,
  username: process.env.DB_USER,
  password: process.env.DB_PASS
})

Step 5: 
create .gitignore file 

inside .gitignore file mention the file that wont be uploaded on git repository

.env
.env.test
node_modules/



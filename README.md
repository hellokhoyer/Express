# Express Handbook
---
নোডজেএস এ যারা ডেভেলপমেন্ট করেন তাদের জন্য অপরিহার্য এবং অত্যান্ত প্রয়োজনীয় ফ্রেমওয়ার্ক হচ্ছে এক্সপ্রেস। যারা এক্সপ্রেস নিয়ে কাজ করেন তাদের জন্য সম্পূর্ন গাইড হচ্ছে এই ডকটি। নিচের দেওয়া কুইক লিঙ্ক থেকে আপনি আপনার ইচ্ছামতো টপিকে জাম্প করতে পারেন।

## How can i help you?
- [সার্ভার তৈরি করা](#সার্ভার-তৈরি-করাঃ)
- [টেমপ্লেটিং](#টেমপ্লেটিংঃ)
- [Routing](#Routing)
- [Middleware](#middleware)\
    [❏ Third Party Middleware](#third-party-middleware) *আসছে*&nbsp;
    [❏ Error Handaling](#) *আসছে*&nbsp;
- [Static Assets Management](#) *আসছে*


#### সার্ভার তৈরি করাঃ
এক্সপ্রেসে আমরা খুব সহজেই লোকাল সার্ভার তৈরি করতে পারি। তার জন্য আপনার পিসিতে [নোডজেএস](https://nodejs.org/en/download/) ইন্সটল থাকতে হবে। এর ইন্সটল প্রসেস অন্যসব সাধারন সফটওয়্যারের মতোই। নোডজেস ইন্সটল হয়ে গেলে আপনার একটা টার্মিনাল অ্যাপ থাকতে হবে। কারন লোকাল পিসিতে অনেক সময় অনেক কমান্ড কাজ করে না। বিষেশ করে উইন্ডোজ ইউজার হলে। তবে ম্যাক বা লিনাক্সের ডিফল্ট টার্মিনালই এনাফ। টার্মিনাল হিসেবে আমার প্রথম পছন্দ [Cmder](http://cmder.net/) আপনি চাইলে [Git Bash](https://git-scm.com/downloads) ব্যবহার করতে পারেন। যেটাই ব্যবহার করেন ডাউনলোড করে নিন। 

**এবার আসি সার্ভার সেটাপ প্রসঙ্গেঃ** আপনি আপনার টার্মিনাল ওপেন করুন। এবং পছন্দের পাথ সিলেক্ট করুন। `cd pathname` কমান্ডের মাধ্যমে। গিট এর টার্মিনাল হলে ফোল্ডার এ গিয়ে `Git Bash Here` দিলেই সেই ডিরেক্টরিতে টার্মিনাল ওপেন হবে। আর Cmder হলে প্রথমেই Cmder ফোল্ডার টা আনজিপ করে ডেক্সটপে নিয়ে আসবেন। এতে করে কাজ করতে ঝামেলা হবে না। এর পর `cmder.exe` ওপেন করবেন। তার কারেন্ট পাথে ওপেন হবে। তো আপনার এক ফোল্ডার ব্যাক এ আসতে হবে। আগের ডিরেক্টরিতে ব্যাক আসতে `cd ..` কমান্ড ব্যবহার করবেন। এবার ডেস্কটপ থেকে আমরা কাজ শুরু করবো।

প্রথমে নতুন একটা ডিরেক্টরি ক্রিয়েট করবো।
`mkdir express-server`
> `mkdir` হচ্ছে make directory কমান্ড। আর স্পেস দিয়ে কি ডিরেক্টরি সেটা লিখলাম।

এবার ঐ ডিরেক্টরিতে আমরা যাবো। অর্থাৎ ডেক্সটপ থেকে `express-server` এ ঢুকবো।
`cd express-server`
> `cd` হচ্ছে চেঞ্জ ডিরেক্টরি।

এখন এই ডিরেক্টরিতে আমাদের সমস্থ কাজ করবো। তার আগে একটা ফাইল ক্রিয়েট করে নেবো। সার্ভার যে ফাইল থেকে রান হবে।
`touch server.js`
> touch কমান্ড দিয়ে ফাইল ক্রিয়েট করতে হয়।

ফাইল ক্রিয়েট হলো এখন আমরা নোড প্যাকেজ ম্যানেজার বা npm ইনিশিয়ালাইজ করবো।
`npm init`
> এখানে অনেকগুলো ইনফরমেশন এডিটের অপশন থাকবে। আপনি বুঝে থাকলে এডিট করবেন। না হলে এন্টার চেপে চেপে ইন্সটল করে ফেলবেন।

npm আমাদের ডিরেক্টরিতে ইন্সটল হয়েছে। এখন আমরা নোড কমান্ডের মাধ্যমে express ইন্সটল করবো এবং কিছু প্রয়োজনীয় প্যাকেজ ইন্সটল করবো।


`npm i express --S`
> `i` হচ্ছে ইন্সটল --S ফ্লাগ দিয়েছি `package.json` ফাইলের ডিপেনডেন্সিতে গিয়ে এক্সপ্রেস অ্যাড হওয়ার জন্য। দেওয়া বাধ্যতামূলক না।

`npm i -g nodemon`
> `nodemon` আমাদের সার্ভারকে অটোমেটিক রিস্টার্ট করবে কোডে কোনো চেঞ্জ আসলে। `-g` ফ্লাগ হচ্ছে এটা গ্লোবাল প্যাকেজ হিসেবে ইন্সটল করেছি।

প্যাকেজ ইন্সটল করা শেষ হলো। এবার আমরা ফাইলগুলোকে এডিটরে ওপেন করে কোডিং শুরু করবো।

`code .`
> `code` হচ্ছে vs code এর আইডেন্টিফায়ার। আপনি অ্যাটম ব্যবহার করলে (Atom) ব্রাকেট ব্যবহার করলে (Brackets) ব্যবহার করবেন। অথবা ম্যানুয়াল প্রসেসে ওপেন করতে পারেন। আর `.` হচ্ছে এক্সটেনশন। . যুক্ত যতো ফাইল আছে ওপেন হবে। এক কথায় সব ফাইল। কারন . ছাড়া এক্সটেনশন হয় না। :P

`server.js` ফাইল ওপেন করবো। এবং এক্সপ্রেস ইনক্লুড করে দিবো।
```javascript
var express = require('express');
```

এবার এক্সপ্রেস ফাংশনকে এক্সপ্রেশনে ( রেফারেন্স ) কনভার্ট করবো কাজের সুবিধার জন্য।
```javascript
const app = express();`
```
> `app` মানেই `express()`
এখন পোর্ট সেট করবো
```javascript
app.listen(3000);
```

কনসোলে সার্ভার রানিং কি না দেখার জন্য আরেকটা প্যারামিটার নিয়ে অ্যানোনিমাস ফাংশন ক্রিয়েট করা যাবে। এবং ঐ ফাংশনে লগ ম্যাসেজ লিখে দিলেন।

```javascript
app.listen(3000, function(){
    console.log("sever running on port : 3000");
});
```

এবার রেস্পন্স পাচ্ছে কি না দেখবো। টার্মিনালে `nodemon` কমান্ড দিলে দেখতে পাবো আমাদের ম্যাসেজটি আসছে। সার্ভার সেটাপ কমপ্লিট। তবে আমাদের ব্রাউজারের জন্য কোনো কাজ করা হয় নি।

এবার আমরা get method এর মাধ্যমে রেস্পন্স কালেক্ট করবো। এবং ব্রাউজারে রেন্ডার করবো।
```javascript
app.get('/', function(req, res){
   res.send("Hello world!");
});
```
> get method HTTP GET verb এর কাজ করে। আর প্রথম প্যারামিটার হচ্ছে রাউট বা পাথ। সহজ কথায় পেজ। `'/'` হচ্ছে হোমপেজ। রাউটিং সম্পর্কে জানা যাবে রাউটিং সেকশন এ। দ্বিতীয় প্যারামিটারে একটা কলব্যাক ফাংশন। যেটা আর্গুমেন্টে রিকোয়েস্ট এবং রেস্পন্স হ্যান্ডেল করে। যেহেতু আমরা ব্রাউজারে রেস্পন্স পাঠাতে চাচ্ছি তাই `res.send()` method ব্যবহার করেছি।

এবার পুরো কাজগুলো দেখে নিই।

```javascript
// 1. include express
var express = require('express');
// 2. store express express() into app variable
const app = express();
    // 4. Create a response for homepage
    app.get('/', function(req, res){
    res.send("Hello world!");
    });
// 3. Create server
app.listen(3000, function(){
    console.log("sever running on port : 3000");
});
```

এবার আমরা ব্রাউজারে দেখি। এই url এর মাধ্যমে।
`localhost:3000`
> 300 সার্ভার পোর্ট।
---

#### টেমপ্লেটিংঃ

টেমপ্লেট তৈরি করা যেকোনো ডাইনামিক এপ্লিকেশন এর একটা গুরুত্বপূর্ন অংশ। টেমপ্লেট বলতে সাধারন অর্থে একটা ফর্মা, ডাইসের মতো। আমাদের ডাটাগুলো কিভাবে রেন্ডার হবে এটা টেমপ্লেটে সেট করে দেবো। কোন যায়গায় কোন ইনফরমেশন সেট হবে। তো রাউটে (পেজে) টেমপ্লেট প্রিন্ট করার ভিভিন্ন ওয়ে আছে। আমরা প্রতিটা ওয়ে সম্পর্কে জানবো। 

**সরাসরি html কোড বা টেক্সট প্রিন্ট করতে `res.send()` মেথডঃ**
```javascript
    app.get('/', function(req, res){
    res.send("<h1>Hello world!</h1>");
    });
```
> এখন আমাদের রেস্পন্স `h1` এ প্রিন্ট হবে। 

**কোনো external html পেজ প্রিন্ট করতে `res.sendFile()` মেথডঃ**
যেহেতু আমরা এইচটিএমএল পেজ রেন্ডার করবো এখন আমাদের ফোল্ডারে শুধু `server.js` ফাইল আছে। নতুন একটা ফাইল ক্রিয়েট করে ফেলি। `index.html` নামে। এবং সেটা আমাদের হোম রাউটে রেন্ডার করবো।
```javascript
    app.get('/', function(req, res){
    res.sendFile("index.html");
    });
```
> এখন `index.html` ফাইল রেন্ডার হবে হোমপেজে। অর্থাৎ, ঐ ফাইলে যত মার্কাপ আছে তা প্রিন্ট হবে হোম রাউটে।

একই আরেকটা রাউট তৈরি করে আমরা আরেকটি টেমপ্লেট সেট করে দেই। আমি একটা about রাউট (মানে পেজ) তৈরি করবো। এবং সেই পেইজে `about.html` ফাইল রেন্ডার করবো।

```javascript
    app.get('/about', function(req, res){
    res.sendFile("about.html");
    });
```
> app.get() এর প্রথম প্যারামিটারে `/about` দিয়েছি কারন `about` নামক রাউটে `about.html` ফাইল রেন্ডার হবে। রাউট মানে হচ্ছে পাথ। তো এবার URL টি হবেঃ `locahost:3000/about` এই পেজে প্রিন্ট হবে `about.html` ফাইল।

এই মেথডগুলো জানলাম আমরা স্ট্যাটিক ফাইল কন্ট্রোলিং এর জন্য। কিন্ট ডাইনামিক অ্যাপ্লিকেশন তৈরি করতে গেলে html কোডে কন্ডিশন সেট করা যাবে না। হাতে লিখে প্রিন্ট করতে হবে। আর এর জন্য সমাধান হচ্ছে টেমপ্লেটিং ইঞ্জিন। টেমপ্লেটিং ইঞ্জিনের মাধ্যমে আমরা html কোডের মধ্যে কন্ডিশন সেট করতে পারবো। এর ইনক্লুড, ইনহেরিট ফিচারের মাধ্যমে আমরা টেমপ্লেট কে সিম্পল এবং ফাস্ট করতে পারবো। জনপ্রিয় একটা টেমপ্লেটিং ইঞ্জিন হচ্ছে `pug`। যেটা আগে Jade নামে পরিচিত ছিল। এর মাধ্যমে আমরা এক্সপ্রেসে কাজ করবো। তো এটা ব্যবহার করার আগে অবশ্যই ইন্টল করে নিতে হবে। নিচের কমান্ডটি টার্মিনালে রান করলেই ইন্সটল হয়ে যাবে।

`npm install pug -S`
> -S ফ্লাগ দিয়েছি ডিপেন্ডেন্সিতে অ্যাড করার জন্য।

তো কিছু সময় নিয়ে অ্যাপটি ইন্সটল হয়ে যাবে। এবার আমাদের `server.js` ফাইলে অ্যাড করে দিবো। তার জন্য `app.set() `method ইউজ করবো। তাহলে আমাদের এক্সপ্রেস অ্যাপের সাথে সেট হয়ে যাবে।

`app.set('view engine', 'pug');`
> কি হিসেবে সেট হবে প্রথম প্যারামিটার এ বলে দিলাম অর্থাৎ নাম। কি সেট হবে দ্বিতীয় প্যারামিটারে অর্থাৎ ভ্যালু।

তো এবার সেটাপ শেষ। তবে আরেকটু কাজ বাকি রয়েছে। view engine রেন্ডার করে views নামক ফোল্ডারে থাকা ফাইল। যেহেতু আমাদের views নামে কোনো ফোল্ডার নেই। তাই ক্রিয়েট করে নেবো। এবং একটা ফাইল ক্রিয়েট করবো `index.pug` নামে। এবার আমরা pug ফাইলে মার্কাপ অ্যাড করবো তার আগে pug এর মার্কাপ সম্পর্কে পরিচিত হয়ে নেই।


```pug
doctype html
html(lang="en")
  head
    title First Pug Template
  body
    h1 This Is My First Pug Page
  footer
    small Abul Khoyer
```
> pug হচ্ছে সিঙ্গেল মার্কাপ। সবকিছু একবার করে ব্যবহার করতে হয়। এবং পাশে স্পেস দিয়ে তার ভ্যালু দিতে হয়। এবং indent (ট্যাব প্রেস) করে প্যারেন্ট চাইল্ড ডিফাইন করতে হয়। অনেকটা স্পেস সেন্সেটিভ।  যেটা উপরের মার্কাপ খেয়াল করলে দেখতে পারবেন। হালকা কমন সেন্স নিয়ে HTML সেন্সে দেখবেন। :P

এবার এই পেজটাকে আমরা আমাদের Home রাউটে রেন্ডার করবো। আর টেমপ্লেট রেন্ডার করার মেথড হচ্ছে res.render();

```javascript
app.get('/', function (req, res) {
  res.render('index');
})
```
> .pug দিলে দিবেন না দিলে না দিবেন। উস্তাদ বুঝে নিবে। :P

এবার আসি কন্ডিশন সেট করার পালায়। আমরা চাচ্ছি একটা ভ্যারিয়েবল pug টেমপ্লেটে দিতে। এবং একেক পেইজে সেই ভ্যারিয়েবল এর মান একেকরকম হবে। তো করে নেই। pug এ ভ্যারিয়েবল সেট করতে ট্যাগ এর শেষে `=` দিয়ে ভ্যারিয়েবল নাম দিবেন।
```pug
doctype html
html(lang="en")
  head
    title First Pug Template
  body
    h1= welcomeText
  footer
    small Abul Khoyer
```
> variable নেম হচ্ছে `welcomeText`। যেটা একেক পেজে একেক রকম ওয়েলকাম দিবে।

এবার দুইটা রাউটে সেম টেমপ্লেট দিয়ে দুইরকম আউটপুট দেখাবো কিভাবে একটু দেখি।

```javascript
app.get('/one', function (req, res) {
  res.render('index', { welcomeText: 'Hello to one page' })
});

app.get('/another', function (req, res) {
  res.render('index', { welcomeText: 'Hello to another page' })
});
```
> একই মেথড তবে সেকেন্ড প্যারামিটারে একটা অবজেক্ট নিয়ে ভ্যারিয়েবলগুলো লিখবেন। একাধিক হলে কমা দিয়ে দিয়ে। কাজ করছে কিনা দেখে নিইঃ `localhost:3000/one` এবং `localhost:3000/another`

আরেকটা ঝামেলা হলো। আপনি চাচ্ছেন ভ্যারিয়েবল টা মাঝখানে কোনো যায়গায় রাখতে। সেক্ষেত্রে কিভাবে ভ্যারিয়েবল সেট করবেন? এর একটা সমাধান হচ্ছে `#{varible}` এভাবে ভ্যারিয়েবল স্টোর করা। অনেকটা টেমপ্লেট স্টিং এর মতো।

```pug
doctype html
html(lang="en")
  head
    title First Pug Template
  body
    h1 welcom, #{name}
  footer
    small Abul Khoyer
```
```javascript
app.get('/another', function (req, res) {
  res.render('index', { name: 'khoyer' })
});
```

এবার চাচ্ছি আরেকটু অ্যাডভান্সভাবে অরগানাইজ করতে। layout এর জন্য আলাদা টেমপ্লেট করবো। এবং সেখানে header, footer, section ইত্যাদি ইনক্লুড করবো। তো প্রথমে ফাইলগুলো ক্রিয়েট করে ফেলি।

`header.pug`
```pug
head
    title our first layout
```
`footer.pug`
```pug
footer
    small Abul Khoyer
```
এবার layout.pug ফাইল ক্রিয়েট করে ফাইলগুলো ইনক্লুড করি।
```pug
doctype html
html(lang="en")
    include header.pug
    body
        header
            h1 Hello #{name}
        block content
    include footer.pug
```
> এখানে block দিয়ে কন্টেন্ট দেওয়া হয়েছে। কারন এই যায়গাটাতে আমরা কন্টেন্ট পুশ করবো।

এবার দেখে নেই কিভাবে এই লেআউট আমরা অ্যাপ্লাই করবো me.pug এ।
```pug
extends layout.pug
block content
    div.content
        h2 Hello this is #{name}!
```
```javascipt
app.get('/me', function (req, res) {
  res.render('me', { name: 'khoyer' })
});
```


> এখানে extends এর মাধ্যমে layout ইনহেরিট করা হয়েছে। block এর যায়গাতে ইন্ডেন্ট (ট্যাব) করে আমাদের কন্টেন্ট দিয়ে দিয়েছি। যেটা লেআউটের ঐ ব্লকে যায়গা করে নিয়েছে।

এবার এই পেজটাকে আরেকটু ডাইনামিক করি। যদি এমন হতো নেম এর যায়গা দিয়েছি কিন্ত সেকেন্ড প্যারামিটারে নেম দেই নাই। তখন যায়গাটা বিচ্ছিরি দেখাতে। এই ব্যপারটা আমরা if else দিয়ে হ্যান্ডেল করতে পারি এরকমঃ

```pug
extends layout.pug
block content
    div.content
            if name
                h2 Hello this is #{name}!
            else
                Hello My guest!
```

```javascipt
app.get('/me', function (req, res) {
  res.render('me');
});
```
> এবার localhost:3000/me পেজ রান করলে দেখবেন else অংশটুকু রেন্ডার হবে।


আরও অনেকরকম itteration আছে। [pug](https://pugjs.org/language/iteration.html) এর অফিশিয়াল ডকুমেন্টেশনে। আর আপনি যদি html কোডে ফাস্ট হোন তাহলে [এইখান থেকে](https://html2jade.org/) html কে pug এ কনভার্ট করে নিবেন।

---
#### Routing:
রাউট নিয়ে আমরা উপরে ভাসা ভাসা কিছু আলোচনা করেছি ইতিমধ্যে। কিন্ত পুরো ধারনা দেওয়া হয় নি। রাউট হচ্ছে অনেকটা পাথ/ফোল্ডার/ডিরেক্টরি। অর্থাৎ কোন লোকেশনে আমাদের ইনফরমেশন প্রিন্ট করতে চাচ্ছি সেটা ডিফাইন করা। রাউটের সাথে আরও কিছু ব্যপার জড়িত আছে। কোন মেথডে কোন রাউটে এক্সেস করবো সেটাও ডিফাইন যায়। 

ফাংশনটা এরকমঃ `app.method(path, handler)`
> method হচ্ছে HTTP মেথড। path হচ্ছে লোকেশন। আর handler হচ্ছে একটা কলব্যাক ফাংশন। তো পুরো বিষয়টা এরকমঃ এই method এ এই path এ রেস্পন্স পাঠালে এই কাজ করো। কি করো সেটা বলে দেবো handler এ অর্থাৎ কলব্যাকে।

তো এই কাজগুলো করার জন্য HTTP মেথডগুলো জানা খুবই জরুরি। সংক্ষেপে বিষয়গুলো রিক্যাপ করছিঃ

`GET` (`app.get()`) : এই মেথডের কাজ হচ্ছে সার্ভারে ডাটা পাওয়ার জন্য রিকোয়েষ্ট পাঠানো। এবং প্রাপ্ত ডাটা আমরা রিপ্রেজেন্ট করি।

`POST` (`app.post()`) : এই মেথডের কাজ হচ্ছে সার্ভারে ডাটা সংরক্ষনের জন্য প্রেরন করা। যাতে পরবর্তিতে নির্দিষ্ট নামে ডাকলে আমরা খুজে পাই।

`PUT` (`app.put()`) : এই মেথডের কাজ হচ্ছে সার্ভারে রাখা ডাটাকে নতুন ডাটার মাধ্যমে রিপ্লেস বা মডিফাই করা।

`PATCH` (`app.patch()`) : এই মেথডের কাজ হচ্ছে সার্ভারে রাখা ডাটাকে সম্পুর্ন মডিফাই না করে কোনো একটা নির্দিষ্ট অংশকে মডিফাই করা।

`DELETE` (`app.delete()`) : এই মেথডের কাজ হচ্ছে সার্ভারে রাখা ডাটাকে সার্ভার থেকে মুছে দেওয়া।

এবার আমরা ভবিষ্যতে মেথডগুলো কাজে লাগাতে পারবো। তবে express এই মেথডগুলোকে কিভাবে হ্যান্ডেল করে সেটা জেনে নেই। যদিও আগে একবার জেনেছি এবং কাজ করেছি। তবে সবগুলো জানা হয় নি। এবং এর পিছনের লজিক বুঝিনি।

```javascript
//GET something
app.get('/', function (req, res) {
  res.send('GET request to homepage');
});
//POST something
app.post('/', function (req, res) {
  res.send('POST request to homepage');
});
//PUT something
app.put('/', function (req, res) {
  res.send('PUT request to homepage');
});
//PATCH something
app.patch('/', function (req, res) {
  res.send('PATCH request to homepage');
});

//DELETE something
app.delete('/', function (req, res) {
  res.send('DELETE request to homepage');
});
```
> উপরের উধাহরণগুলো দেখলে সহজেই আপনি বুঝতে পারবেন। এটা যেকোনো রাউটে কাজ করবে। আমি উধাহরনে শুধু হোম রাউটে দেখিয়েছি।

---
#### Middleware:
মিডলওয়্যার হচ্ছে এমন একটা কনসেপ্ট যা খুবই সহজ। আমরা যে রিকোয়েস্ট পাঠাই এবং রেস্পন্স আসে এই রিকোয়েস্ট এবং রেস্পন্স এর মধ্যাবস্থাকেই মিডলওয়্যার বলে। আর সহজভাবে বলা যায় আমরা যখন কাওকে ফোন বা ম্যাসেজ দিয়ে জিজ্ঞেস করি এই তুই কই। রিপ্লে লিখার আগে সে কোথায় আছে এটা চিন্তা করার সময়টাই মিডলওয়্যার। আর রিপ্লেটা হচ্ছে রেস্পন্স। তো এখানে **কোথায় আছিস?** হচ্ছে রিকোয়েস্ট। কই আছে না আছে এই চিন্তা করার সময়টা হচ্ছে মিডলওয়্যার। **এইখানে আছি** বলে দেওয়া হচ্ছে রেস্পন্স। তার মানে রিকোয়েস্ট এবং রেস্পন্স এর অদেখা অবস্থাটাই মিডলওয়্যার। তাহলে বুঝা গেলো আমরা যখনই রিকোয়েস্ট পাঠাই তখনই একটা মিডলওয়্যার ব্যবহার হয়। মিডলওয়্যার এর access আছে রিকোয়েস্ট অবজেক্ট এর মধ্যে।

দেখে নেই মিডলওয়্যার কিভাবে কাজ করেঃ
এর ব্যাসিক স্ট্রাকচার অনেকটা আমাদের পরিচিত। আমরা এর আগে একটা কলব্যাক ফাংশন ব্যবহার করেছি। যার মধ্যে দুইটা আর্গুমেনেট ছিল `req` এবং `res`।

```javascript
    app.get('/', function(req, res){
    res.send("Hello world!");
    });
```

এই সেম ফাংশনটাই আরেকটা ফাংশন আর্গুমেন্ট নিবে `next` নামে। `next` ফাংশনের কাজ হচ্ছে রেস্পন্স প্রসেসিং এর পরে আমাদের কাংখিত রাউটে এবং মেথডে ট্রিগার করা। তো দেখে নেই কিভাবে মিডলওয়্যার ইউজ করা যায়।


**পুরো অ্যাপ্লিকেশনে একটা মিডলওয়্যার ব্যবহার করতে হলেঃ**

```javascript
app.use(function(req, res, next){

});
```
> `app.use` সব মেথডে সব রাউটে এই মিডলওয়্যার কাজ করবে।

**নির্দিষ্ট কোনো রাউটে ব্যবহার করতে হলেঃ**

```javascript
app.use('/about', function(req, res, next){

});
```
> প্রথম প্যারামিটারে রাউটনেম লিখে দিয়েছি তাই এটা শুধু `about` রাউটের সব মেথডে কাজ করবে।


**নির্দিষ্ট রাউটে এবং নির্দিষ্ট রিকোয়েস্টে ব্যবহার করতে হলেঃ**

```javascript
app.get('/about', function(req, res, next){

});
```
> HTTP মেথড ডিক্লেয়ার করে দিয়েছি তাই এটা শুধু `about` রাউটের GET মেথডে কাজ করবে।

আমরা ইউজ করার মেথড জেনে নিলাম। কিন্ত মিডলওয়্যার রেস্পন্স বডির কাজ এখনো দেখা হয় নি। এই বিষয়গুলো জেনে নেই।

আমরা চাচ্ছি আমাদের পুরো অ্যাপ্লিকেশনজুড়ে একটা মিডলওয়্যার দিতে। সো, আমরা করে ফেলি।

```javascript
app.use(function(req, res, next){

});
```

এবার চাচ্ছি মিডলওয়্যারে একটা কনসোল ম্যাসেজ প্রিন্ট করতে যেটা রেস্পন্স পাঠানোর আগেই এক্সিকিউট হবে। কারন মিডলওয়ার রেস্পন্স পাঠানোর আগেই কাজ করে। কনসোল ম্যাসেজ লিখলাম।

```javascript
app.use(function(req, res, next){
    console.log("I'm executing before sending response to body");
});
```
> এবার URL হিট করুন। দেখবেন লোডিং হচ্ছে এবং সাথে সাথে টার্মিনালে কনসোল ম্যাসেজটি আসছে।

এটা করার পর একটা প্রবলেম হচ্ছে ব্রাউজারে বার বার বার রিলোড করার পরও পেজ লোড হচ্ছে না। আর এর কারন হচ্ছে `next()` ফাংশনটি কল না করা।

তো এবার এই ফাংশনের ভুমিকা জেনে নেওয়া যাকঃ
আমরা আগেই জেনেছি `next()` ফাংশনের কাজ হচ্ছে রেস্পন্স প্রসেসিং এর পরে আমাদের কাংখিত রাউটে এবং মেথডে ট্রিগার করা। তো এই ক্ষেত্রে আমাদের কাংখিত রাউট হচ্ছে সবগুলো এবং সব মেথডেই যাবে। তাই পেজই লোড হচ্ছে না।

এবার `next()` অ্যাড করে দিবো। এবং সাথে সাথেই দেখবো লোডিং সাক্সেসফুল। 

```javascript
app.use(function(req, res, next){
    console.log("I'm executing before sending response to body");
    next();
});
```
আশা করি মিডলওয়্যার বুঝা গেছে। এবার কিছু থার্ড পার্টি মিডলওয়্যার ব্যবহার করবো। আমাদের কাজের প্রয়োজনে।

##### Third Party Middleware:



*নতুন আপডেট আসবে আস্তে আস্তে। আপনি চাইলে ফর্ক করে রাখতে পারেন। প্রয়োজনীয় মনে হলে শেয়ার করবেন।*


>[⇮ মেনুতে ফিরে যান ⇮](#Express-Handbook)
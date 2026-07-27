# digital-marketing
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The chipest product</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Poppins,sans-serif;
}

body{
background:#f8f8f8;
color:#222;
}

html{
scroll-behavior:smooth;
}

/* HERO */

.hero{
height:100vh;
background:url('https://i.ibb.co/pvYy6TVs/IMG-20260725-WA0013.jpg') center/cover;
display:flex;
align-items:center;
justify-content:center;
text-align:center;
position:relative;
}

.hero::before{
content:'';
position:absolute;
inset:0;
background:rgba(0,0,0,.45);
}

.hero-content{
position:relative;
z-index:2;
color:#fff;
padding:20px;
}

.hero h1{
font-size:50px;
font-weight:700;
}

.hero p{
margin:15px 0;
font-size:20px;
}

.hero button{
padding:15px 35px;
border:none;
background:#ff5722;
color:#fff;
font-size:18px;
border-radius:40px;
cursor:pointer;
}

.hero button:hover{
background:#e64a19;
}

/* PRODUCTS */

.products{
padding:60px 20px;
}

.products h2{
text-align:center;
margin-bottom:30px;
font-size:32px;
}

.carousel{
display:flex;
overflow-x:auto;
gap:20px;
scroll-behavior:smooth;
padding-bottom:20px;
}

.carousel::-webkit-scrollbar{
display:none;
}

.card{
background:#fff;
min-width:270px;
border-radius:15px;
overflow:hidden;
box-shadow:0 8px 25px rgba(0,0,0,.1);
}

.card img{
width:100%;
height:200px;
object-fit:cover;
}

.card-body{
padding:15px;
}

.card h3{
margin-bottom:10px;
}

.price{
font-size:22px;
color:#ff5722;
font-weight:bold;
margin-bottom:15px;
}

.card button{
width:100%;
padding:12px;
background:#ff5722;
color:white;
border:none;
border-radius:8px;
cursor:pointer;
}

/* CART */

.cart-btn{
position:fixed;
right:20px;
bottom:90px;
width:65px;
height:65px;
border-radius:50%;
background:#ff5722;
color:#fff;
font-size:28px;
display:flex;
align-items:center;
justify-content:center;
cursor:pointer;
z-index:999;
box-shadow:0 10px 25px rgba(0,0,0,.2);
}

.cart-count{
position:absolute;
top:-5px;
right:-5px;
background:red;
width:24px;
height:24px;
display:flex;
align-items:center;
justify-content:center;
border-radius:50%;
font-size:13px;
}

.drawer{
position:fixed;
right:-420px;
top:0;
width:400px;
max-width:100%;
height:100%;
background:white;
transition:.4s;
box-shadow:-8px 0 30px rgba(0,0,0,.2);
padding:20px;
overflow:auto;
z-index:9999;
}

.drawer.open{
right:0;
}

.drawer h2{
margin-bottom:15px;
}

.cart-item{
margin-bottom:10px;
padding-bottom:10px;
border-bottom:1px solid #ddd;
}

input{
width:100%;
padding:12px;
margin-top:12px;
border:1px solid #ccc;
border-radius:8px;
}

.send-btn{
margin-top:15px;
width:100%;
padding:14px;
background:#28a745;
color:#fff;
border:none;
font-size:18px;
border-radius:8px;
cursor:pointer;
}

/* WhatsApp */

.whatsapp{
position:fixed;
bottom:15px;
right:20px;
width:65px;
height:65px;
background:#25D366;
border-radius:50%;
display:flex;
align-items:center;
justify-content:center;
font-size:34px;
text-decoration:none;
color:#fff;
box-shadow:0 8px 20px rgba(0,0,0,.2);
}

footer{
padding:25px;
text-align:center;
background:#111;
color:white;
margin-top:50px;
}
</style>

</head>
<body>

<section class="hero">

<div class="hero-content">

<h1>The chipest product</h1>

<p>Fresh Finds, Best Prices</p>

<button onclick="document.getElementById('products').scrollIntoView()">
Shop Now
</button>

</div>

</section>

<section class="products" id="products">

<h2>Our Products</h2>

<div class="carousel" id="carousel">

</div>

</section>

<div class="cart-btn" onclick="toggleCart()">
🛒
<div class="cart-count" id="count">0</div>
</div>

<div class="drawer" id="drawer">

<h2>Your Cart</h2>

<div id="cartItems"></div>

<h3 id="total"></h3>

<input id="name" placeholder="Customer Name">

<input id="phone" placeholder="Phone Number">

<button class="send-btn" onclick="sendOrder()">
Send Order
</button>

</div>

<a class="whatsapp"
href="https://wa.me/911234567890"
target="_blank">
💬
</a>

<footer>

© 2026 The chipest product

</footer>

<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>

<script>

emailjs.init("YOUR_PUBLIC_KEY");

const products=[

{
name:"Burger Combo",
price:99,
img:"https://i.ibb.co/JVSQLKs/IMG-4008.jpg"
},

{
name:"Street Food",
price:149,
img:"https://i.ibb.co/2Y6sZ2vF/ai-generated-street-menu-fast-food-on-the-table-professional-advertising-foodgraphy-photo.jpg"
},

{
name:"Fast Food Meal",
price:199,
img:"https://i.ibb.co/KPQ1MTR/fast-food-meal-with-burgers-hot-dog-fries-soda-9975-132268.jpg"
}

];

const carousel=document.getElementById("carousel");

products.forEach((p,i)=>{

carousel.innerHTML+=`

<div class="card">

<img src="${p.img}">

<div class="card-body">

<h3>${p.name}</h3>

<div class="price">₹${p.price}</div>

<button onclick="addCart(${i})">

Add to Cart

</button>

</div>

</div>

`;

});

let cart=[];

function addCart(i){

cart.push(products[i]);

updateCart();

}

function toggleCart(){

document.getElementById("drawer").classList.toggle("open");

}

function updateCart(){

document.getElementById("count").innerHTML=cart.length;

let html="";

let total=0;

cart.forEach(item=>{

html+=`

<div class="cart-item">

<b>${item.name}</b><br>

₹${item.price}

</div>

`;

total+=item.price;

});

document.getElementById("cartItems").innerHTML=html;

document.getElementById("total").innerHTML="Total : ₹"+total;

}

function sendOrder(){

if(cart.length==0){

alert("Cart is empty");

return;

}

const name=document.getElementById("name").value;

const phone=document.getElementById("phone").value;

if(name==""||phone==""){

alert("Fill customer details");

return;

}

let items="";

cart.forEach(c=>{

items+=${c.name} - ₹${c.price}\n;

});

emailjs.send(

"YOUR_SERVICE_ID",

"YOUR_TEMPLATE_ID",

{

customer_name:name,

customer_phone:phone,

order:items,

owner_email:"satyadevpanwar558@gmail.com"

}

)

.then(()=>{

alert("Order Sent Successfully");

cart=[];

updateCart();

document.getElementById("name").value="";

document.getElementById("phone").value="";

});

}

setInterval(()=>{

carousel.scrollBy({

left:300,

behavior:"smooth"

});

if(carousel.scrollLeft+carousel.clientWidth>=carousel.scrollWidth){

carousel.scrollTo({

left:0,

behavior:"smooth"

});

}

},3000);

</script>

</body>
</html>

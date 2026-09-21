<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<meta name="theme-color" content="#62d8f7">
<title>Spidy Entrepreneur</title>
<style>
*{box-sizing:border-box}
:root{
  --bg:#87e3ff;
  --header:#62d8f7;
  --card:#fff;
  --text:#073b4c;
  --accent:#00a8d6;
  --shadow:0 8px 25px rgba(0,100,130,.18);
}
body.dark{
  --bg:#071923;
  --header:#0c2c3a;
  --card:#102934;
  --text:#e9fbff;
  --accent:#40d9ff;
  --shadow:0 8px 25px rgba(0,0,0,.35);
}
body{
  margin:0;
  font-family:Arial,sans-serif;
  background:var(--bg);
  color:var(--text);
  transition:.3s;
}
header{
  text-align:center;
  padding:42px 15px;
  background:var(--header);
}
.logo{
  font-size:52px;
  font-weight:900;
  margin-bottom:5px;
}
header p{
  font-size:18px;
  margin:8px 0 20px;
}
.badge{
  display:inline-block;
  background:var(--card);
  color:var(--text);
  padding:9px 18px;
  border-radius:30px;
  font-weight:bold;
}
.controls{
  max-width:1100px;
  margin:25px auto 10px;
  padding:0 15px;
  display:flex;
  gap:10px;
  flex-wrap:wrap;
  justify-content:center;
}
input,select,button{
  border:0;
  border-radius:12px;
  padding:13px 16px;
  font-size:15px;
}
input,select{
  background:var(--card);
  color:var(--text);
  box-shadow:var(--shadow);
}
input{
  width:min(500px,100%);
}
button{
  background:var(--accent);
  color:white;
  font-weight:bold;
  cursor:pointer;
}
button:hover{
  transform:translateY(-2px);
}
.stats{
  max-width:1100px;
  margin:20px auto;
  padding:0 15px;
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:12px;
}
.stat{
  background:var(--card);
  padding:18px;
  border-radius:16px;
  text-align:center;
  box-shadow:var(--shadow);
}
.stat strong{
  display:block;
  font-size:27px;
}
.grid{
  max-width:1100px;
  margin:25px auto;
  padding:0 15px 30px;
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(240px,1fr));
  gap:18px;
}
.card{
  background:var(--card);
  border-radius:18px;
  padding:20px;
  box-shadow:var(--shadow);
  position:relative;
  transition:.25s;
  animation:appear .4s ease;
}
.card:hover{
  transform:translateY(-6px);
}
.number{
  position:absolute;
  right:15px;
  top:10px;
  font-size:30px;
  font-weight:bold;
  color:var(--accent);
  opacity:.35;
}
h2{
  margin:0 40px 15px 0;
  font-size:21px;
}
.card p{
  line-height:1.45;
  margin:8px 0;
}
.tag{
  display:inline-block;
  margin-top:8px;
  padding:5px 9px;
  border-radius:20px;
  background:#d9f7ff;
  color:#05627a;
  font-size:12px;
  font-weight:bold;
}
body.dark .tag{
  background:#164453;
  color:#8deaff;
}
.empty{
  text-align:center;
  padding:50px;
  font-size:20px;
  grid-column:1/-1;
}
footer{
  text-align:center;
  padding:30px;
  font-weight:bold;
}
@keyframes appear{
  from{opacity:0;transform:translateY(15px)}
  to{opacity:1;transform:translateY(0)}
}
@media(max-width:600px){
  .logo{font-size:38px}
  .stats{grid-template-columns:1fr}
}
</style>
</head>
<body>
<header>
  <div class="logo">🕷️ Spidy Entrepreneur 🚀</div>
  <p>Explore • Learn • Build • Grow</p>
  <div class="badge">67 BUSINESS IDEAS</div>
</header>
<div class="controls">
  <input id="search" type="search" placeholder="🔎 Search business ideas...">
  <select id="difficulty">
    <option value="all">All Difficulties</option>
    <option value="Easy">Easy</option>
    <option value="Medium">Medium</option>
    <option value="Hard">Hard</option>
  </select>
  <button onclick="toggleDark()">🌙 Dark Mode</button>
</div>
<div class="stats">
  <div class="stat">
    <strong>67</strong>
    Ideas
  </div>
  <div class="stat">
    <strong id="shown">67</strong>
    Showing
  </div>
  <div class="stat">
    <strong>🚀</strong>
    Build Your Future
  </div>
</div>
<div class="grid" id="grid"></div>
<footer>
  Spidy Entrepreneur • 67 Ideas • Explore. Learn. Build. 🚀
</footer>
<script>
const ideas = [
["Website Design Service","₹0–₹2,000","Easy","HTML, CSS","Local businesses"],
["Logo Design","₹0–₹1,000","Easy","Graphic design","Creators & shops"],
["Social Media Management","₹0–₹2,000","Easy","Social media","Small businesses"],
["Video Editing","₹0–₹3,000","Easy","Editing","Creators & brands"],
["Instagram Reels Service","₹0–₹2,000","Easy","Reels & editing","Local brands"],
["Content Writing","₹0","Easy","Writing","Websites & creators"],
["Online Tutoring","₹0–₹1,000","Easy","Teaching","Students"],
["Digital Notes","₹0","Easy","Research & design","Students"],
["Print-on-Demand","₹0–₹3,000","Medium","Design & marketing","Online shoppers"],
["Custom T-Shirt Design","₹1,000–₹5,000","Easy","Design","Students & creators"],
["Phone Case Designs","₹500–₹3,000","Easy","Design","Smartphone users"],
["Digital Invitations","₹0–₹1,000","Easy","Canva/design","Families & event planners"],
["Resume Design","₹0","Easy","Design & writing","Students & job seekers"],
["Presentation Design","₹0","Easy","PowerPoint/design","Students & businesses"],
["Photography Service","₹0–₹10,000","Medium","Photography","Families & businesses"],
["Product Photography","₹1,000–₹5,000","Medium","Photography","Online sellers"],
["Blogging","₹0–₹3,000","Medium","Writing & SEO","Online audience"],
["YouTube Channel","₹0–₹5,000","Medium","Video & communication","Viewers & brands"],
["Podcast Editing","₹0–₹3,000","Medium","Audio editing","Podcasters"],
["AI Automation Service","₹0–₹5,000","Medium","AI tools","Small businesses"],
["Chatbot Creation","₹0–₹5,000","Medium","AI & coding","Businesses"],
["Mobile App Development","₹0–₹5,000","Hard","Programming","Businesses & startups"],
["Game Development","₹0–₹5,000","Medium","Coding & design","Gamers"],
["Website Maintenance","₹0–₹2,000","Easy","Web development","Website owners"],
["SEO Service","₹0–₹3,000","Medium","SEO","Businesses"],
["Online Store Setup","₹0–₹5,000","Medium","E-commerce","Small sellers"],
["Digital Marketing","₹0–₹3,000","Medium","Marketing","Local businesses"],
["Email Marketing","₹0–₹2,000","Medium","Copywriting & marketing","Online businesses"],
["Influencer Management","₹0–₹2,000","Medium","Communication","Creators & brands"],
["Event Decoration","₹2,000–₹10,000","Medium","Creativity","Families & events"],
["Gift Hamper Business","₹2,000–₹10,000","Easy","Packaging","Gift buyers"],
["Handmade Jewelry","₹1,000–₹5,000","Easy","Crafting","Fashion shoppers"],
["Candle Making","₹2,000–₹8,000","Medium","Crafting","Home decor buyers"],
["Resin Art","₹2,000–₹8,000","Medium","Crafting","Art & gift buyers"],
["Custom Stickers","₹500–₹3,000","Easy","Design","Students & creators"],
["Art Commission Service","₹0–₹2,000","Medium","Drawing","Art lovers"],
["Pet Photography","₹0–₹5,000","Medium","Photography","Pet owners"],
["Pet Sitting","₹0–₹1,000","Easy","Pet care","Pet owners"],
["Home Cleaning Service","₹1,000–₹5,000","Easy","Cleaning","Households"],
["Car Wash Service","₹2,000–₹10,000","Easy","Cleaning","Vehicle owners"],
["Bike Washing Service","₹1,000–₹5,000","Easy","Cleaning","Bike owners"],
["Home Gardening Service","₹1,000–₹5,000","Easy","Gardening","Homeowners"],
["Plant Nursery","₹2,000–₹10,000","Medium","Gardening","Plant lovers"],
["Homemade Snacks","₹2,000–₹10,000","Medium","Cooking","Local customers"],
["Baking Business","₹3,000–₹15,000","Medium","Baking","Families & events"],
["Meal Prep Service","₹3,000–₹15,000","Medium","Cooking & planning","Busy families"],
["Custom Cakes","₹3,000–₹15,000","Medium","Baking & decorating","Celebrations"],
["Thrift Clothing Store","₹2,000–₹10,000","Medium","Fashion & marketing","Young shoppers"],
["Custom Embroidery","₹2,000–₹10,000","Medium","Embroidery","Fashion buyers"],
["Alteration Service","₹1,000–₹5,000","Medium","Sewing","Local customers"],
["Personal Shopping","₹0–₹2,000","Easy","Fashion & communication","Busy shoppers"],
["Study Planner Templates","₹0","Easy","Design","Students"],
["Notion Templates","₹0","Easy","Notion & design","Students & professionals"],
["Online Course Creation","₹0–₹5,000","Medium","Teaching & video","Online learners"],
["E-book Publishing","₹0–₹2,000","Easy","Writing","Readers"],
["Freelance Translation","₹0","Easy","Languages","Businesses & creators"],
["Virtual Assistant","₹0","Easy","Organization","Entrepreneurs"],
["Data Entry Service","₹0","Easy","Computer skills","Businesses"],
["Cloud Kitchen","₹10,000+","Hard","Cooking & operations","Food delivery customers"],
["Local Delivery Service","₹1,000–₹5,000","Medium","Logistics","Local shops"],
["Digital Menu Design","₹0–₹1,000","Easy","Design","Restaurants & cafes"],
["QR Code Service","₹0–₹1,000","Easy","Basic tech","Shops & events"],
["Local Business Listing Service","₹0","Easy","Online research","Local businesses"],
["Tech Support Service","₹0–₹3,000","Medium","Computer skills","Families & small businesses"],
["Custom Website Tools","₹0–₹5,000","Hard","Programming","Businesses & creators"],
["Freelance Coding","₹0–₹3,000","Medium","Programming","Startups & businesses"],
["Digital Product Store","₹0–₹2,000","Easy","Design & marketing","Online buyers"]
];
const grid=document.getElementById("grid");
const search=document.getElementById("search");
const difficulty=document.getElementById("difficulty");
const shown=document.getElementById("shown");
function render(){
  const term=search.value.toLowerCase();
  const level=difficulty.value;
  grid.innerHTML="";
  const filtered=ideas.filter((idea,index)=>{
    const text=idea.join(" ").toLowerCase();
    return text.includes(term) &&
           (level==="all" || idea[2]===level);
  });
  shown.textContent=filtered.length;
  if(filtered.length===0){
    grid.innerHTML='<div class="empty">😕 No business ideas found.</div>';
    return;
  }
  filtered.forEach((idea)=>{
    const originalNumber=ideas.indexOf(idea)+1;
    const card=document.createElement("div");
    card.className="card";
    card.innerHTML=`
      <div class="number">${originalNumber}</div>
      <h2>${idea[0]}</h2>
      <p><b>💰 Startup:</b> ${idea[1]}</p>
      <p><b>🎯 Difficulty:</b> ${idea[2]}</p>
      <p><b>🧠 Skills:</b> ${idea[3]}</p>
      <p><b>👥 Customers:</b> ${idea[4]}</p>
      <span class="tag">${idea[2]}</span>
    `;
    grid.appendChild(card);
  });
}
function toggleDark(){
  document.body.classList.toggle("dark");
  localStorage.setItem(
    "spidyDark",
    document.body.classList.contains("dark")
  );
}
if(localStorage.getItem("spidyDark")==="true"){
  document.body.classList.add("dark");
}
search.addEventListener("input",render);
difficulty.addEventListener("change",render);
render();
</script>
</body>
</html>
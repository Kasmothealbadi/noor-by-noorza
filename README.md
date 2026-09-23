# noor-by-noorza
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Your Jewelry Shop Name — Shop Online</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,500;0,600;1,500&family=Jost:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --ivory:#F7F2EA;
    --card:#FFFFFF;
    --ink:#241F1C;
    --ink-soft:#6B6259;
    --gold:#A8823D;
    --gold-deep:#8A6A2F;
    --wine:#6B2737;
    --wine-deep:#54202C;
    --line:#E7DFD2;
    --radius:2px;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    font-family:'Jost',sans-serif;
    background:var(--ivory);
    color:var(--ink);
    -webkit-font-smoothing:antialiased;
  }
  h1,h2,h3,.serif{font-family:'Cormorant Garamond',serif;}
  a{color:inherit;}
  button{font-family:inherit;cursor:pointer;}
  img{max-width:100%;display:block;}

  /* ---------- Header ---------- */
  header{
    padding:44px 20px 28px;
    text-align:center;
    border-bottom:1px solid var(--line);
  }
  header h1{
    font-size:clamp(32px,6vw,46px);
    font-weight:600;
    letter-spacing:.5px;
    margin:0 0 6px;
  }
  header p{
    margin:0;
    color:var(--ink-soft);
    font-size:15px;
    letter-spacing:.3px;
  }

  /* ---------- Category filter ---------- */
  .filters{
    display:flex;
    gap:10px;
    justify-content:center;
    flex-wrap:wrap;
    padding:22px 16px;
    max-width:900px;
    margin:0 auto;
  }
  .filters button{
    background:none;
    border:1px solid var(--line);
    color:var(--ink);
    padding:9px 20px;
    border-radius:999px;
    font-size:13.5px;
    letter-spacing:.3px;
    transition:background .2s,color .2s,border-color .2s;
  }
  .filters button.active,
  .filters button:hover{
    background:var(--ink);
    border-color:var(--ink);
    color:var(--ivory);
  }

  /* ---------- Product grid ---------- */
  .grid{
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:16px;
    padding:8px 16px 60px;
    max-width:1080px;
    margin:0 auto;
  }
  @media(min-width:640px){ .grid{grid-template-columns:repeat(3,1fr);gap:22px;padding:8px 30px 70px;} }
  @media(min-width:960px){ .grid{grid-template-columns:repeat(4,1fr);} }

  .card{
    background:var(--card);
    border:1px solid var(--line);
    display:flex;
    flex-direction:column;
  }
  .card-media{
    position:relative;
    aspect-ratio:1/1;
    overflow:hidden;
    background:#EFE8DC;
  }
  .card-media img{width:100%;height:100%;object-fit:cover;}
  .dots{
    position:absolute;
    bottom:8px;left:0;right:0;
    display:flex;
    justify-content:center;
    gap:5px;
  }
  .dots button{
    width:6px;height:6px;border-radius:50%;
    background:rgba(255,255,255,.6);
    border:1px solid rgba(0,0,0,.15);
    padding:0;
  }
  .dots button.active{background:var(--gold);}

  .card-body{padding:14px 14px 16px;display:flex;flex-direction:column;gap:6px;flex:1;}
  .card-cat{font-size:11px;letter-spacing:.4px;color:var(--gold-deep);}
  .card-name{font-size:19px;font-weight:600;line-height:1.25;}
  .card-price{font-size:15px;color:var(--ink-soft);margin-top:auto;}
  .add-btn{
    margin-top:10px;
    background:var(--wine);
    color:#fff;
    border:none;
    padding:10px 0;
    font-size:13.5px;
    letter-spacing:.4px;
    transition:background .2s;
  }
  .add-btn:hover{background:var(--wine-deep);}
  .add-btn.added{background:var(--gold-deep);}

  /* ---------- Cart button ---------- */
  .cart-fab{
    position:fixed;bottom:22px;right:22px;
    background:var(--ink);color:var(--ivory);
    border:none;border-radius:999px;
    padding:14px 20px;
    font-size:14px;
    display:flex;align-items:center;gap:8px;
    box-shadow:0 6px 18px rgba(0,0,0,.25);
    z-index:40;
  }
  .cart-fab span.count{
    background:var(--wine);
    border-radius:999px;
    min-width:20px;height:20px;
    display:inline-flex;align-items:center;justify-content:center;
    font-size:12px;
  }

  /* ---------- WhatsApp button ---------- */
  .wa-fab{
    position:fixed;bottom:22px;left:22px;
    background:#25D366;color:#fff;
    border-radius:999px;
    width:52px;height:52px;
    display:flex;align-items:center;justify-content:center;
    box-shadow:0 6px 18px rgba(0,0,0,.25);
    z-index:40;text-decoration:none;
  }
  .wa-fab svg{width:26px;height:26px;fill:#fff;}

  /* ---------- Cart drawer ---------- */
  .overlay{
    position:fixed;inset:0;background:rgba(20,16,12,.45);
    opacity:0;pointer-events:none;transition:opacity .25s;z-index:50;
  }
  .overlay.open{opacity:1;pointer-events:auto;}
  .drawer{
    position:fixed;top:0;right:0;bottom:0;
    width:min(420px,100%);
    background:var(--ivory);
    transform:translateX(100%);
    transition:transform .3s ease;
    z-index:51;
    display:flex;flex-direction:column;
  }
  .drawer.open{transform:translateX(0);}
  .drawer-head{
    padding:20px;border-bottom:1px solid var(--line);
    display:flex;justify-content:space-between;align-items:center;
  }
  .drawer-head h2{margin:0;font-size:26px;}
  .drawer-head button{background:none;border:none;font-size:22px;line-height:1;color:var(--ink);}
  .drawer-body{flex:1;overflow-y:auto;padding:16px 20px;}
  .drawer-empty{color:var(--ink-soft);text-align:center;padding:40px 0;}
  .line-item{
    display:flex;gap:12px;padding:14px 0;border-bottom:1px solid var(--line);
  }
  .line-item img{width:64px;height:64px;object-fit:cover;flex-shrink:0;}
  .li-info{flex:1;display:flex;flex-direction:column;gap:4px;}
  .li-name{font-size:15px;font-weight:500;}
  .li-price{font-size:13px;color:var(--ink-soft);}
  .qty-row{display:flex;align-items:center;gap:10px;margin-top:4px;}
  .qty-row button{
    width:24px;height:24px;border:1px solid var(--line);background:#fff;
    font-size:14px;line-height:1;
  }
  .qty-row .remove{border:none;background:none;color:var(--wine);font-size:12px;margin-left:auto;text-decoration:underline;}
  .drawer-foot{
    border-top:1px solid var(--line);padding:16px 20px 22px;
  }
  .total-row{display:flex;justify-content:space-between;font-size:18px;margin-bottom:14px;}
  .total-row .serif{font-size:24px;}
  .place-order-btn{
    width:100%;background:var(--wine);color:#fff;border:none;
    padding:13px 0;font-size:14px;letter-spacing:.4px;
  }
  .place-order-btn:hover{background:var(--wine-deep);}

  /* ---------- Checkout form ---------- */
  .checkout-form{display:flex;flex-direction:column;gap:12px;}
  .checkout-form label{font-size:13px;color:var(--ink-soft);display:block;margin-bottom:4px;}
  .checkout-form input,.checkout-form textarea{
    width:100%;padding:10px 12px;border:1px solid var(--line);
    background:#fff;font-family:inherit;font-size:14px;color:var(--ink);
  }
  .checkout-form textarea{resize:vertical;min-height:60px;}
  .back-link{background:none;border:none;color:var(--ink-soft);font-size:13px;text-decoration:underline;padding:0;margin-bottom:6px;align-self:flex-start;}

  .confirm-box{text-align:center;padding:30px 6px;}
  .confirm-box h3{font-size:24px;margin-bottom:10px;}
  .confirm-box p{color:var(--ink-soft);font-size:14px;line-height:1.5;margin-bottom:18px;}
  .confirm-box a.wa-link{
    display:inline-block;background:#25D366;color:#fff;padding:10px 22px;
    text-decoration:none;font-size:14px;border-radius:999px;
  }
  .error-msg{color:var(--wine);font-size:13px;}
  @media (prefers-reduced-motion:reduce){
    *{transition:none!important;}
  }
</style>
</head>
<body>

<header>
  <h1>Your Jewelry Shop Name</h1>
  <p>Handcrafted jewelry, delivered with care · Your City, State</p>
</header>

<nav class="filters" id="filters"></nav>
<main class="grid" id="grid"></main>

<button class="cart-fab" id="cartFab" aria-label="Open cart">
  🛍 Cart <span class="count" id="cartCount">0</span>
</button>

<a class="wa-fab" id="waFab" href="#" target="_blank" rel="noopener" aria-label="Chat on WhatsApp">
  <svg viewBox="0 0 24 24"><path d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.75.46 3.46 1.32 4.96L2.05 22l5.25-1.38a9.9 9.9 0 0 0 4.74 1.21h.01c5.46 0 9.9-4.45 9.9-9.91 0-2.65-1.03-5.14-2.9-7.01A9.82 9.82 0 0 0 12.04 2m0 1.67c2.34 0 4.54.91 6.2 2.56a8.73 8.73 0 0 1 2.56 6.2c0 4.56-3.72 8.28-8.79 8.28a8.2 8.2 0 0 1-4.19-1.14l-.3-.18-3.12.82.83-3.04-.2-.31a8.18 8.18 0 0 1-1.26-4.38c0-4.56 3.75-8.28 8.27-8.28m-4.7 4.27c-.16 0-.42.06-.64.3-.22.24-.85.83-.85 2.02 0 1.19.87 2.34.99 2.5.12.16 1.7 2.6 4.13 3.64.58.25 1.03.4 1.38.51.58.18 1.11.16 1.53.1.47-.07 1.43-.58 1.63-1.15.2-.56.2-1.04.14-1.14-.06-.1-.22-.16-.46-.28-.24-.12-1.43-.7-1.65-.79-.22-.08-.38-.12-.55.12-.16.24-.63.79-.77.95-.14.16-.28.18-.52.06-.24-.12-1.02-.38-1.94-1.2-.72-.64-1.2-1.43-1.34-1.67-.14-.24-.02-.37.1-.49.11-.11.24-.28.36-.42.12-.14.16-.24.24-.4.08-.16.04-.3-.02-.42-.06-.12-.55-1.34-.76-1.83-.2-.48-.4-.42-.55-.42h-.47z"/></svg>
</a>

<div class="overlay" id="overlay"></div>
<aside class="drawer" id="drawer">
  <div id="drawerContent"></div>
</aside>

<script>
/* ============ CONFIG — edit this section for your shop ============ */
const SHOP = {
  name: "Your Jewelry Shop Name",
  whatsappNumber: "91XXXXXXXXXX", // digits only, country code, no + or spaces
  formspreeId: "xjykrkno"
};

const PRODUCTS = [
  {id:"e1", name:"Aanya Drop Earrings", price:899, category:"Earrings",
   images:["https://kommodo.ai/i/364SFmmRRIXeyECO4fco","https://kommodo.ai/i/VC3xr1LYXusV9w4fiDZM","https://kommodo.ai/i/Uw3WxYZRHXfbAALMpPIe"]},
  {id:"e2", name:"Meher Hoop Earrings", price:749, category:"Earrings",
   images:["https://kommodo.ai/i/SBI38KCc4I8XobIqXjyk","https://kommodo.ai/i/rasugHRV5p3ceVH02I8s","https://kommodo.ai/i/Ir0r0XFHrz9p3ngwr3f6"]},
  {id:"e3", name:"Zara Chandbali Earrings", price:1099, category:"Earrings",
   images:["https://kommodo.ai/i/sRFxffaJCGx6Y5OOZLXL","https://kommodo.ai/i/Xy0obwDP2ix3dgjS9y2p","https://kommodo.ai/i/flFCOXIqrAdp3CV8Q9BN"]},
  {id:"e4", name:"Naina Stud Earrings", price:599, category:"Earrings",
   images:["https://kommodo.ai/i/B4avLObgdDzCplZ1qQgP","https://kommodo.ai/i/RileTHfbsYjcjZNkHQdq","https://kommodo.ai/i/2LT8dr6uy5a91xoty0kM"]},
  {id:"e5", name:"Ishaani Jhumka Earrings", price:949, category:"Earrings",
   images:["https://kommodo.ai/i/d6QVyuteOK0sxH2Xsel2","https://kommodo.ai/i/7W92IkCcWMLaY3Jezxxs","https://kommodo.ai/i/L23Y4Kic5Ld012Lfu4Ll"]},
  {id:"e6", name:"Kavya Dangle Earrings", price:849, category:"Earrings",
   images:["https://kommodo.ai/i/ugqLsRRVvnt67OKZ4cKZ","https://kommodo.ai/i/1781BeqOEtFuD42emRYs","https://kommodo.ai/i/Pt81hIgnzO5fXWghI1C0"]},
  {id:"n1", name:"Anaya Layered Necklace", price:1499, category:"Necklaces",
   images:["https://kommodo.ai/i/aT1JsFB5PDyGRLcTX2fr","https://kommodo.ai/i/ZqD7MQqgQF1tebif6gUh","https://kommodo.ai/i/8eMhhrlHZZnRHOsVjD2T"]},
  {id:"b1", name:"Riya Chain Bracelet", price:699, category:"Bracelets",
   images:["https://kommodo.ai/i/UG1vreUDS7ltHrVjfbjh","https://kommodo.ai/i/fLRsT0uqz2pIk3Vv69uO","https://kommodo.ai/i/keivoryjTCDeQSE5hRYp"]},
  {id:"b2", name:"Tara Charm Bracelet", price:799, category:"Bracelets",
   images:["https://kommodo.ai/i/ut8S1B6Rkx6oHTkaqcHy","https://kommodo.ai/i/MK4l3PdfC60IYJLeH17G","https://kommodo.ai/i/yJxPUYipWtIUNXx1vsqz"]},
  {id:"b3", name:"Diya Cuff Bracelet", price:649, category:"Bracelets",
   images:["https://kommodo.ai/i/7s2cDLt2jIPz5hA6rcG9","https://kommodo.ai/i/0iieIlwRg4kQdx2p9kwf","https://kommodo.ai/i/zIXd0OPf8UdX9QHx39Ku"]},
  {id:"b4", name:"Kiara Beaded Bracelet", price:549, category:"Bracelets",
   images:["https://kommodo.ai/i/a8qkFzZRGo1oTjm1HnLq","https://kommodo.ai/i/ITgxxkAuKuYafQkm0NLq","https://kommodo.ai/i/CkFrAYB7X5pUSLnt7Mnj"]}
];
/* ==================================================================== */

document.title = SHOP.name + " — Shop Online";
document.querySelector("header h1").textContent = SHOP.name;
document.getElementById("waFab").href = "https://wa.me/" + SHOP.whatsappNumber;

let cart = {};
try{ cart = JSON.parse(localStorage.getItem("jshop_cart") || "{}"); }catch(e){ cart = {}; }
let activeCategory = "All";
const activeImgIndex = {};

function saveCart(){ try{ localStorage.setItem("jshop_cart", JSON.stringify(cart)); }catch(e){} }
function cartCount(){ return Object.values(cart).reduce((s,q)=>s+q,0); }
function money(n){ return "₹" + n.toLocaleString("en-IN"); }

/* ---------- Filters ---------- */
const categories = ["All", ...new Set(PRODUCTS.map(p=>p.category))];
const filtersEl = document.getElementById("filters");
categories.forEach(cat=>{
  const b = document.createElement("button");
  b.textContent = cat;
  if(cat===activeCategory) b.classList.add("active");
  b.onclick = ()=>{ activeCategory = cat; renderFilters(); renderGrid(); };
  filtersEl.appendChild(b);
});
function renderFilters(){
  [...filtersEl.children].forEach(b=>b.classList.toggle("active", b.textContent===activeCategory));
}

/* ---------- Grid ---------- */
const gridEl = document.getElementById("grid");
function renderGrid(){
  gridEl.innerHTML = "";
  const list = activeCategory==="All" ? PRODUCTS : PRODUCTS.filter(p=>p.category===activeCategory);
  list.forEach(p=>{
    if(activeImgIndex[p.id]===undefined) activeImgIndex[p.id]=0;
    const card = document.createElement("div");
    card.className = "card";
    const idx = activeImgIndex[p.id];
    card.innerHTML = `
      <div class="card-media">
        <img src="${p.images[idx]}" alt="${p.name}" loading="lazy">
        ${p.images.length>1 ? `<div class="dots">${p.images.map((_,i)=>`<button data-i="${i}" class="${i===idx?'active':''}" aria-label="View image ${i+1}"></button>`).join("")}</div>` : ""}
      </div>
      <div class="card-body">
        <div class="card-cat">${p.category}</div>
        <div class="card-name">${p.name}</div>
        <div class="card-price">${money(p.price)}</div>
        <button class="add-btn" data-id="${p.id}">Add to Cart</button>
      </div>`;
    card.querySelectorAll(".dots button").forEach(dot=>{
      dot.onclick = ()=>{ activeImgIndex[p.id] = parseInt(dot.dataset.i); renderGrid(); };
    });
    const addBtn = card.querySelector(".add-btn");
    addBtn.onclick = ()=>{
      cart[p.id] = (cart[p.id]||0)+1;
      saveCart(); updateCartCount();
      addBtn.textContent = "Added ✓";
      addBtn.classList.add("added");
      setTimeout(()=>{ addBtn.textContent="Add to Cart"; addBtn.classList.remove("added"); }, 900);
    };
    gridEl.appendChild(card);
  });
}

function updateCartCount(){
  document.getElementById("cartCount").textContent = cartCount();
}

/* ---------- Drawer ---------- */
const overlay = document.getElementById("overlay");
const drawer = document.getElementById("drawer");
const drawerContent = document.getElementById("drawerContent");

function openDrawer(){ renderCartView(); overlay.classList.add("open"); drawer.classList.add("open"); }
function closeDrawer(){ overlay.classList.remove("open"); drawer.classList.remove("open"); }
document.getElementById("cartFab").onclick = openDrawer;
overlay.onclick = closeDrawer;

function renderCartView(){
  const items = Object.entries(cart).map(([id,qty])=>({p:PRODUCTS.find(p=>p.id===id), qty})).filter(x=>x.p);
  const total = items.reduce((s,x)=>s+x.p.price*x.qty,0);
  drawerContent.innerHTML = `
    <div class="drawer-head"><h2 class="serif">Your Cart</h2><button id="closeDrawer" aria-label="Close">×</button></div>
    <div class="drawer-body">
      ${items.length===0 ? '<div class="drawer-empty">Your cart is empty.</div>' :
        items.map(x=>`
        <div class="line-item" data-id="${x.p.id}">
          <img src="${x.p.images[0]}" alt="${x.p.name}" loading="lazy">
          <div class="li-info">
            <div class="li-name">${x.p.name}</div>
            <div class="li-price">${money(x.p.price)} × ${x.qty} = ${money(x.p.price*x.qty)}</div>
            <div class="qty-row">
              <button class="dec">−</button>
              <span>${x.qty}</span>
              <button class="inc">+</button>
              <button class="remove">Remove</button>
            </div>
          </div>
        </div>`).join("")}
    </div>
    <div class="drawer-foot">
      <div class="total-row"><span>Total</span><span class="serif">${money(total)}</span></div>
      <button class="place-order-btn" id="placeOrderBtn" ${items.length===0?"disabled":""}>Place Order</button>
    </div>`;
  document.getElementById("closeDrawer").onclick = closeDrawer;
  drawerContent.querySelectorAll(".line-item").forEach(row=>{
    const id = row.dataset.id;
    row.querySelector(".inc").onclick = ()=>{ cart[id]++; saveCart(); updateCartCount(); renderCartView(); };
    row.querySelector(".dec").onclick = ()=>{ cart[id]--; if(cart[id]<=0) delete cart[id]; saveCart(); updateCartCount(); renderCartView(); };
    row.querySelector(".remove").onclick = ()=>{ delete cart[id]; saveCart(); updateCartCount(); renderCartView(); };
  });
  if(items.length>0){
    document.getElementById("placeOrderBtn").onclick = renderCheckoutForm;
  }
}

function renderCheckoutForm(){
  drawerContent.innerHTML = `
    <div class="drawer-head"><h2 class="serif">Checkout</h2><button id="closeDrawer" aria-label="Close">×</button></div>
    <div class="drawer-body">
      <button class="back-link" id="backToCart">← Back to cart</button>
      <form class="checkout-form" id="orderForm">
        <div><label for="cname">Full name *</label><input id="cname" required></div>
        <div><label for="cphone">Phone number *</label><input id="cphone" type="tel" required></div>
        <div><label for="caddr">Delivery address *</label><textarea id="caddr" required></textarea></div>
        <div><label for="cnote">Special instructions (optional)</label><textarea id="cnote"></textarea></div>
        <p class="error-msg" id="orderError" style="display:none;"></p>
        <button type="submit" class="place-order-btn" id="submitBtn">Submit Order</button>
      </form>
    </div>`;
  document.getElementById("closeDrawer").onclick = closeDrawer;
  document.getElementById("backToCart").onclick = renderCartView;
  document.getElementById("orderForm").onsubmit = submitOrder;
}

async function submitOrder(e){
  e.preventDefault();
  const name = document.getElementById("cname").value.trim();
  const phone = document.getElementById("cphone").value.trim();
  const addr = document.getElementById("caddr").value.trim();
  const note = document.getElementById("cnote").value.trim();
  const errEl = document.getElementById("orderError");
  const btn = document.getElementById("submitBtn");
  errEl.style.display = "none";

  const items = Object.entries(cart).map(([id,qty])=>({p:PRODUCTS.find(p=>p.id===id), qty})).filter(x=>x.p);
  const total = items.reduce((s,x)=>s+x.p.price*x.qty,0);
  const summaryLines = items.map(x=>`${x.p.name} — ${money(x.p.price)} × ${x.qty} = ${money(x.p.price*x.qty)}`).join("\n");
  const orderSummary =
`ORDER FROM ${SHOP.name.toUpperCase()}
----------------------------------
${summaryLines}
----------------------------------
GRAND TOTAL: ${money(total)}

CUSTOMER DETAILS
Name: ${name}
Phone: ${phone}
Address: ${addr}
Instructions: ${note || "None"}`;

  btn.disabled = true; btn.textContent = "Submitting...";
  try{
    const res = await fetch(`https://formspree.io/f/${SHOP.formspreeId}`, {
      method:"POST",
      headers:{ "Accept":"application/json", "Content-Type":"application/json" },
      body: JSON.stringify({
        customer_name:name, customer_phone:phone, customer_address:addr,
        instructions:note || "None", order_total:money(total),
        order_summary:orderSummary
      })
    });
    if(res.ok){
      cart = {}; saveCart(); updateCartCount();
      renderConfirmation(name);
    }else{
      throw new Error("Submission failed");
    }
  }catch(err){
    errEl.textContent = "Something went wrong sending your order. Please try again, or message us directly on WhatsApp.";
    errEl.style.display = "block";
    btn.disabled = false; btn.textContent = "Submit Order";
  }
}

function renderConfirmation(name){
  drawerContent.innerHTML = `
    <div class="drawer-head"><h2 class="serif">Order Placed</h2><button id="closeDrawer" aria-label="Close">×</button></div>
    <div class="drawer-body">
      <div class="confirm-box">
        <h3 class="serif">Thank you, ${name.split(" ")[0] || "there"}!</h3>
        <p>Order placed! ${SHOP.name} will contact you on WhatsApp to confirm.</p>
        <a class="wa-link" href="https://wa.me/${SHOP.whatsappNumber}" target="_blank" rel="noopener">Chat on WhatsApp</a>
      </div>
    </div>`;
  document.getElementById("closeDrawer").onclick = ()=>{ closeDrawer(); renderGrid(); };
}

renderGrid();
updateCartCount();
</script>
</body>
</html>

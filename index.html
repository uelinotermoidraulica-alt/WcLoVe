import { firebaseConfig, firebaseEnabled } from "./firebase-config.js";

let auth, db, storage, user = null;
let reviews = [];
let currentPosition = null;
let map, markersLayer;

const $ = (id) => document.getElementById(id);

async function initFirebase(){
  if(!firebaseEnabled){
    $("statusText").textContent = "Modalità locale: collega Firebase per database online";
    loadLocal();
    renderAll();
    return;
  }

  const { initializeApp } = await import("https://www.gstatic.com/firebasejs/10.12.5/firebase-app.js");
  const { getAuth, GoogleAuthProvider, signInWithPopup, signOut, onAuthStateChanged } = await import("https://www.gstatic.com/firebasejs/10.12.5/firebase-auth.js");
  const { getFirestore, collection, addDoc, getDocs, query, orderBy, serverTimestamp } = await import("https://www.gstatic.com/firebasejs/10.12.5/firebase-firestore.js");
  const { getStorage, ref, uploadBytes, getDownloadURL } = await import("https://www.gstatic.com/firebasejs/10.12.5/firebase-storage.js");

  window.firebaseApi = { GoogleAuthProvider, signInWithPopup, signOut, collection, addDoc, getDocs, query, orderBy, serverTimestamp, ref, uploadBytes, getDownloadURL };
  const app = initializeApp(firebaseConfig);
  auth = getAuth(app); db = getFirestore(app); storage = getStorage(app);

  onAuthStateChanged(auth, async (u)=>{
    user = u;
    updateUserUI();
    await loadFirebase();
  });
}

function initMap(){
  map = L.map("map").setView([45.4642, 9.19], 13);
  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
    maxZoom: 19,
    attribution: "© OpenStreetMap"
  }).addTo(map);
  markersLayer = L.layerGroup().addTo(map);
}

function setView(name){
  document.querySelectorAll(".view").forEach(v=>v.classList.remove("active"));
  $("view-"+name).classList.add("active");
  document.querySelectorAll(".bottom-nav button").forEach(b=>b.classList.toggle("active", b.dataset.view===name));
  if(name==="home" && map) setTimeout(()=>map.invalidateSize(), 200);
}

function stars(n){ return "⭐".repeat(Number(n||0)); }
function yn(v){ return v==="yes" ? "Sì" : v==="no" ? "No" : "Non so"; }

function renderAll(){
  renderMap();
  renderList();
  renderGallery();
  renderRanking();
  updateUserUI();
}

function renderMap(){
  if(!markersLayer) return;
  markersLayer.clearLayers();
  reviews.forEach(r=>{
    if(r.lat && r.lng){
      const marker = L.marker([r.lat, r.lng]).addTo(markersLayer);
      marker.bindPopup(`<b>${escapeHtml(r.placeName)}</b><br>${stars(r.rating)}<br>${escapeHtml(r.cityName||"")}`);
    }
  });
}

function renderList(){
  const box = $("bathroomList");
  if(!reviews.length){ box.innerHTML = `<div class="item">Nessun bagno recensito.</div>`; return; }
  box.innerHTML = reviews.map(r=>`
    <article class="item">
      <h3>${escapeHtml(r.placeName)}</h3>
      <div class="meta">${stars(r.rating)} · ${escapeHtml(r.cityName||"")} · ${escapeHtml(r.userName||"Utente")}</div>
      <p>${escapeHtml(r.comment||"")}</p>
      <div class="chips">
        <span class="chip">Pulizia ${r.cleanliness}/5</span>
        <span class="chip">Carta: ${yn(r.toiletPaper)}</span>
        <span class="chip">Sapone: ${yn(r.soap)}</span>
        <span class="chip">Disabili: ${yn(r.accessible)}</span>
        <span class="chip">Fasciatoio: ${yn(r.changingTable)}</span>
      </div>
    </article>`).join("");
}

function renderGallery(){
  const imgs = reviews.filter(r=>r.photoUrl);
  $("gallery").innerHTML = imgs.length ? imgs.map(r=>`<img src="${r.photoUrl}" alt="${escapeHtml(r.placeName)}">`).join("") : `<div class="item">Nessuna foto caricata.</div>`;
}

function renderRanking(){
  const counts = {};
  reviews.forEach(r=>{
    const name = r.userName || "Utente";
    counts[name] = (counts[name]||0)+1;
  });
  const rows = Object.entries(counts).sort((a,b)=>b[1]-a[1]);
  $("rankingList").innerHTML = rows.length ? rows.map(([name,count],i)=>`
    <div class="item"><b>${i+1}. ${escapeHtml(name)}</b><div class="meta">${count} recensioni · 🏅 Ispettore WC</div></div>
  `).join("") : `<div class="item">Nessuna classifica disponibile.</div>`;
}

function updateUserUI(){
  const logged = !!user;
  $("loginBtn").classList.toggle("hidden", logged);
  $("logoutBtn").classList.toggle("hidden", !logged);
  $("profileBox").classList.toggle("hidden", logged);
  $("loggedBox").classList.toggle("hidden", !logged);
  if(logged){
    $("userPhoto").src = user.photoURL || "";
    $("userName").textContent = user.displayName || "Utente";
    $("userEmail").textContent = user.email || "";
    const count = reviews.filter(r=>r.uid === user.uid).length;
    $("reviewCount").textContent = `${count} recensioni pubblicate`;
  }
}

async function login(){
  if(!firebaseEnabled){ alert("Prima collega Firebase nel file firebase-config.js"); return; }
  const { GoogleAuthProvider, signInWithPopup } = window.firebaseApi;
  await signInWithPopup(auth, new GoogleAuthProvider());
}

async function logout(){
  if(!firebaseEnabled) return;
  await window.firebaseApi.signOut(auth);
}

async function loadFirebase(){
  if(!firebaseEnabled){ loadLocal(); renderAll(); return; }
  const { collection, getDocs, query, orderBy } = window.firebaseApi;
  const snap = await getDocs(query(collection(db,"reviews"), orderBy("createdAt","desc")));
  reviews = snap.docs.map(d=>({id:d.id, ...d.data()}));
  renderAll();
}

function loadLocal(){
  reviews = JSON.parse(localStorage.getItem("wcLoveReviews") || "[]");
}

function saveLocal(review){
  reviews.unshift(review);
  localStorage.setItem("wcLoveReviews", JSON.stringify(reviews));
  renderAll();
}

async function saveReview(review, file){
  if(firebaseEnabled && user){
    const { collection, addDoc, serverTimestamp, ref, uploadBytes, getDownloadURL } = window.firebaseApi;
    review.uid = user.uid;
    review.userName = user.displayName || "Utente";
    review.userEmail = user.email || "";
    review.createdAt = serverTimestamp();

    if(file){
      const path = `photos/${Date.now()}-${file.name}`;
      const sref = ref(storage, path);
      await uploadBytes(sref, file);
      review.photoUrl = await getDownloadURL(sref);
    }
    await addDoc(collection(db,"reviews"), review);
    await loadFirebase();
  } else {
    review.userName = "Utente locale";
    review.createdAt = new Date().toISOString();
    if(file) review.photoUrl = await fileToDataUrl(file);
    saveLocal(review);
  }
}

function fileToDataUrl(file){
  return new Promise((res,rej)=>{
    const reader = new FileReader();
    reader.onload=()=>res(reader.result);
    reader.onerror=rej;
    reader.readAsDataURL(file);
  });
}

function getPosition(){
  return new Promise((resolve,reject)=>{
    navigator.geolocation.getCurrentPosition(resolve,reject,{enableHighAccuracy:true,timeout:12000});
  });
}

function escapeHtml(str){
  return String(str ?? "").replace(/[&<>"']/g, m=>({ "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#039;" }[m]));
}

document.addEventListener("DOMContentLoaded", async ()=>{
  initMap();
  await initFirebase();

  document.querySelectorAll(".bottom-nav button").forEach(btn=>btn.addEventListener("click",()=>setView(btn.dataset.view)));
  $("loginBtn").onclick = login;
  $("profileLoginBtn").onclick = login;
  $("logoutBtn").onclick = logout;
  $("refreshBtn").onclick = ()=> firebaseEnabled ? loadFirebase() : (loadLocal(), renderAll());

  $("nearMeBtn").onclick = async ()=>{
    try{
      const pos = await getPosition();
      currentPosition = {lat:pos.coords.latitude,lng:pos.coords.longitude};
      map.setView([currentPosition.lat,currentPosition.lng],16);
      L.marker([currentPosition.lat,currentPosition.lng]).addTo(markersLayer).bindPopup("Sei qui").openPopup();
    }catch(e){ alert("GPS non disponibile o permesso negato."); }
  };

  $("usePositionBtn").onclick = async ()=>{
    try{
      const pos = await getPosition();
      currentPosition = {lat:pos.coords.latitude,lng:pos.coords.longitude};
      $("formMsg").textContent = "Posizione GPS acquisita.";
    }catch(e){ $("formMsg").textContent = "GPS non disponibile."; }
  };

  $("cityBtn").onclick = async ()=>{
    const city = $("cityInput").value.trim();
    if(!city) return;
    const res = await fetch(`https://nominatim.openstreetmap.org/search?format=json&q=${encodeURIComponent(city)}`);
    const data = await res.json();
    if(data[0]) map.setView([Number(data[0].lat), Number(data[0].lon)], 14);
  };

  $("reviewForm").addEventListener("submit", async (e)=>{
    e.preventDefault();
    $("formMsg").textContent = "Salvataggio...";
    const review = {
      placeName:$("placeName").value.trim(),
      cityName:$("cityName").value.trim(),
      rating:Number($("rating").value),
      cleanliness:Number($("cleanliness").value),
      toiletPaper:$("toiletPaper").value,
      soap:$("soap").value,
      accessible:$("accessible").value,
      changingTable:$("changingTable").value,
      comment:$("comment").value.trim(),
      lat:currentPosition?.lat || null,
      lng:currentPosition?.lng || null
    };
    const file = $("photoInput").files[0] || null;
    await saveReview(review, file);
    e.target.reset();
    $("formMsg").textContent = "Recensione salvata.";
    setView("bagni");
  });
});

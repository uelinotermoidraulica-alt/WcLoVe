<!doctype html>
<html lang="it">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <meta name="theme-color" content="#e85b92" />
  <title>WC LoVe</title>
  <link rel="manifest" href="manifest.json" />
  <link rel="stylesheet" href="styles.css" />
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
</head>
<body>
  <div id="app">
    <header class="topbar">
      <div class="brand">
        <div class="wc-logo">
          <div class="wc-text">WC</div>
          <div class="wc-heart">♡</div>
        </div>
        <div>
          <h1>WC LoVe</h1>
          <p id="statusText">App per recensire bagni</p>
        </div>
      </div>
      <button id="loginBtn" class="ghost-btn">Login Google</button>
      <button id="logoutBtn" class="ghost-btn hidden">Esci</button>
    </header>

    <main>
      <section id="view-home" class="view active">
        <div class="search-panel">
          <button id="nearMeBtn" class="primary-btn">Trova bagni vicino a me</button>
          <div class="city-search">
            <input id="cityInput" type="search" placeholder="Ricerca città" />
            <button id="cityBtn">Cerca</button>
          </div>
        </div>
        <div id="map"></div>
      </section>

      <section id="view-bagni" class="view">
        <div class="section-head">
          <h2>Bagni recensiti</h2>
          <button id="refreshBtn" class="small-btn">Aggiorna</button>
        </div>
        <div id="bathroomList" class="list"></div>
      </section>

      <section id="view-add" class="view">
        <form id="reviewForm" class="card form-card">
          <h2>Recensisci un bagno</h2>

          <label>Nome luogo
            <input id="placeName" required placeholder="Bar, ristorante, stazione..." />
          </label>

          <label>Città
            <input id="cityName" placeholder="Città" />
          </label>

          <label>Voto generale
            <select id="rating">
              <option value="5">⭐⭐⭐⭐⭐</option>
              <option value="4">⭐⭐⭐⭐</option>
              <option value="3">⭐⭐⭐</option>
              <option value="2">⭐⭐</option>
              <option value="1">⭐</option>
            </select>
          </label>

          <div class="grid2">
            <label>Pulizia
              <select id="cleanliness">
                <option value="5">Ottima</option><option value="4">Buona</option>
                <option value="3">Normale</option><option value="2">Scarsa</option><option value="1">Pessima</option>
              </select>
            </label>
            <label>Carta igienica
              <select id="toiletPaper">
                <option value="yes">Presente</option><option value="no">Assente</option><option value="unknown">Non so</option>
              </select>
            </label>
            <label>Sapone
              <select id="soap">
                <option value="yes">Presente</option><option value="no">Assente</option><option value="unknown">Non so</option>
              </select>
            </label>
            <label>Accessibilità disabili
              <select id="accessible">
                <option value="yes">Sì</option><option value="no">No</option><option value="unknown">Non so</option>
              </select>
            </label>
            <label>Fasciatoio
              <select id="changingTable">
                <option value="yes">Sì</option><option value="no">No</option><option value="unknown">Non so</option>
              </select>
            </label>
            <label>Foto
              <input id="photoInput" type="file" accept="image/*" />
            </label>
          </div>

          <label>Commento
            <textarea id="comment" rows="4" placeholder="Scrivi la recensione"></textarea>
          </label>

          <div class="actions">
            <button type="button" id="usePositionBtn" class="secondary-btn">Usa posizione GPS</button>
            <button type="submit" class="primary-btn">Salva recensione</button>
          </div>
          <p id="formMsg" class="msg"></p>
        </form>
      </section>

      <section id="view-gallery" class="view">
        <h2>Galleria immagini</h2>
        <div id="gallery" class="gallery"></div>
      </section>

      <section id="view-ranking" class="view">
        <h2>Classifica utenti</h2>
        <div id="rankingList" class="list"></div>
      </section>

      <section id="view-profile" class="view">
        <div class="card profile-card">
          <div id="profileBox">
            <h2>Profilo</h2>
            <p>Accedi con Google per salvare recensioni online.</p>
            <button id="profileLoginBtn" class="primary-btn">Login Google</button>
          </div>
          <div id="loggedBox" class="hidden">
            <img id="userPhoto" class="avatar" alt="Profilo" />
            <h2 id="userName"></h2>
            <p id="userEmail"></p>
            <div class="badge">🏅 Badge: Ispettore WC</div>
            <p id="reviewCount"></p>
          </div>
        </div>
      </section>
    </main>

    <nav class="bottom-nav">
      <button data-view="bagni">🚻<span>Bagni</span></button>
      <button data-view="home" class="active">🗺️<span>Mappa</span></button>
      <button data-view="add">➕<span>Recensisci</span></button>
      <button data-view="ranking">🏆<span>Classifica</span></button>
      <button data-view="profile">👤<span>Profilo</span></button>
    </nav>
  </div>

  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script type="module" src="firebase-config.js"></script>
  <script type="module" src="app.js"></script>
</body>
</html>

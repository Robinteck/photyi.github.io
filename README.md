<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Roulette Indie Games</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #1e1e2f, #3a3a5f);
      color: white;
      text-align: center;
    }

    h1 {
      margin-top: 40px;
    }

    #roulette {
      margin: 40px auto;
      width: 300px;
      height: 300px;
      border-radius: 50%;
      border: 10px solid #fff;
      overflow: hidden;
      position: relative;
      animation: spin 0s ease-in-out;
    }

    .cover {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    #result {
      margin-top: 20px;
      font-size: 1.2em;
    }

    button {
      padding: 15px 30px;
      font-size: 1em;
      background-color: #ff5c5c;
      border: none;
      border-radius: 8px;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    button:hover {
      background-color: #ff2c2c;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(1440deg); }
    }
  </style>
</head>
<body>

  <h1>🎮 Tirage au sort - Jeux Indépendants</h1>
  <div id="roulette">
    <img id="cover" class="cover" src="" alt="Cover du jeu">
  </div>
  <div id="result"></div>
  <button onclick="spinRoulette()">🎲 Tirer un jeu</button>

  <script>
    let games = [];

    fetch("indie_games.json")
      .then(response => {
        if (!response.ok) {
          throw new Error("Fichier JSON introuvable");
        }
        return response.json();
      })
      .then(data => {
        games = data;
      })
      .catch(error => {
        console.error("Erreur de chargement du fichier JSON :", error);
      });

    function spinRoulette() {
      const roulette = document.getElementById("roulette");
      roulette.style.animation = "spin 2s ease-in-out";

      setTimeout(() => {
        roulette.style.animation = "none";
        if (games.length === 0) return;

        const selected = games[Math.floor(Math.random() * games.length)];
        document.getElementById("cover").src = selected.cover;
        document.getElementById("result").innerHTML = `<strong>${selected.title}</strong><br>Note Metacritic : ${selected.metacritic}`;
      }, 2000);
    }
  </script>

</body>
</html>

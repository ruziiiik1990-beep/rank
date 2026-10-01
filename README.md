<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Рейтинг турнира</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

    body { margin: 0; padding: 20px; background: #0f111a; color: #fff; font-family: 'Inter', sans-serif; }

    .rating-container {
      max-width: 1000px; margin: 0 auto;
      background: rgba(16,18,28,0.85);
      border-radius: 14px; padding: 24px;
      border: 1px solid rgba(255,255,255,0.1);
      box-shadow: 0 8px 32px rgba(0,0,0,0.4);
    }

    .rating-title {
      text-align: center; color: #ffd700;
      font-size: 28px; font-weight: 800; text-transform: uppercase;
      letter-spacing: 2px; margin-bottom: 24px;
      text-shadow: 0 2px 10px rgba(255,215,0,0.5);
    }

    table.rating-table {
      width: 100%; border-collapse: collapse;
      color: #e0e0e0; font-size: 15px;
    }
    .rating-table th {
      padding: 16px 12px; text-align: left; color: #aaa;
      font-weight: 700; border-bottom: 1px solid rgba(255,255,255,0.1);
    }
    .rating-table td {
      padding: 12px 12px; border-bottom: 1px solid rgba(255,255,255,0.08);
    }
    .rating-table tr:last-child td { border-bottom: none; }
    .rating-table tr:hover { background: rgba(255,255,255,0.03); }

    .rank-cell { font-weight: 700; color: #ffd700; width: 50px; }
    .team-name-cell { display: flex; align-items: center; gap: 10px; }
    .team-avatar {
      width: 32px; height: 32px; border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-weight: 700; font-size: 14px; color: #fff;
    }
    .west-team .team-avatar { background: linear-gradient(135deg, #4a90d9, #6fb3ff); }
    .east-team .team-avatar { background: linear-gradient(135deg, #e07845, #ff8a65); }

    .stat-wins { color: #66bb6a; font-weight: 700; }
    .stat-losses { color: #ff6b6b; font-weight: 700; }
    .stat-maps { color: #aaa; }

    .admin-controls-rating {
      margin-top: 20px; text-align: center;
    }
    .btn-admin {
      padding: 10px 24px; border: none; border-radius: 8px;
      background: linear-gradient(135deg, #0a2a6b, #1a4a8b);
      color: #fff; font-weight: 600; cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .btn-admin:hover { transform: translateY(-2px); box-shadow: 0 4px 14px rgba(10,42,107,0.4); }

    @media (max-width: 768px) {
      .rating-container { padding: 16px; }
      .rating-table th, .rating-table td { padding: 8px 6px; font-size: 13px; }
      .team-name-cell { flex-direction: column; align-items: flex-start; }
      .team-avatar { margin-bottom: 4px; }
    }
  </style>
</head>
<body>

<div class="rating-container">
  <h1 class="rating-title">Рейтинг турнира</h1>
  <table class="rating-table">
    <thead>
      <tr>
        <th class="rank-cell">#</th>
        <th>Команда</th>
        <th>Победы</th>
        <th>Поражения</th>
        <th>Карты</th>
      </tr>
    </thead>
    <tbody id="ratingBody">
      <!-- Сюда JS будет вставлять строки -->
    </tbody>
  </table>

  <div class="admin-controls-rating">
    <input type="password" id="adminPassRating" placeholder="Админ-пароль" style="padding:10px; width:200px; border-radius:6px; border:1px solid #444; background:#1a1a2e; color:#fff; margin-right:10px;">
    <button class="btn-admin" onclick="toggleAdminRating()">Войти как админ</button>
  </div>
</div>

<!-- Firebase -->
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-database-compat.js"></script>
<script>
(function() {
  var firebaseConfig = {
    apiKey: "AIzaSyCNQ0WFAiQjnISQjXJnHoln-wI64G2BqWs",
    authDomain: "ak4ak-d948e.firebaseapp.com",
    databaseURL: "https://ak4ak-d948e-default-rtdb.firebaseio.com",
    projectId: "ak4ak-d948e",
    storageBucket: "ak4ak-d948e.firebasestorage.app",
    messagingSenderId: "787151252619",
    appId: "1:787151252619:web:05eff65dc74b01d6e8f88e",
    measurementId: "G-DBB4YBNF2Q"
  };
  firebase.initializeApp(firebaseConfig);
  var db = firebase.database();

  var ADMIN_PASSWORD = '12$sacreD';
  var isAdmin = false;

  // Конфигурация команд и их принадлежность к конференциям
  var teamConfig = {
    'Команда A': { name: 'Команда A', conf: 'west' },
    'Команда B': { name: 'Команда B', conf: 'west' },
    'Команда C': { name: 'Команда C', conf: 'west' },
    'Команда D': { name: 'Команда D', conf: 'west' },
    'Команда E': { name: 'Команда E', conf: 'east' },
    'Команда F': { name: 'Команда F', conf: 'east' },
    'Команда G': { name: 'Команда G', conf: 'east' },
    'Команда H': { name: 'Команда H', conf: 'east' }
  };

  function toggleAdminRating() {
    var p = document.getElementById('adminPassRating').value;
    if (!isAdmin) {
      if (p === ADMIN_PASSWORD) {
        isAdmin = true;
        document.getElementById('adminPassRating').value = '';
        alert('Админ-режим включён!');
        renderRating();
      } else { alert('Неверный пароль!'); }
    } else {
      isAdmin = false;
      alert('Админ-режим выключен.');
      renderRating();
    }
  }

  function loadMatchesAndRender() {
    db.ref('playoff/matches').once('value').then(function(snap) {
      var matches = snap.val() || {};
      renderRating(matches);
    });
  }

  function renderRating(matches) {
    var tbody = document.getElementById('ratingBody');
    tbody.innerHTML = '';

    // Считаем статистику по командам
    var stats = {};
    for (var mid in matches) {
      var m = matches[mid];
      if (!m) continue;
      var left = m.left || [];
      var right = m.right || [];
      var winner = m.winner;

      // Для простоты считаем, что если winner есть, то это победа стороны
      if (winner === 'left') {
        addTeamStat(left[0] || 'Unknown', 1, 0); // упрощённо: берём первого как представителя команды
        addTeamStat(right[0] || 'Unknown', 0, 1);
      } else if (winner === 'right') {
        addTeamStat(left[0] || 'Unknown', 0, 1);
        addTeamStat(right[0] || 'Unknown', 1, 0);
      }
    }

    function addTeamStat(teamName, wins, losses) {
      if (!stats[teamName]) stats[teamName] = { wins: 0, losses: 0 };
      stats[teamName].wins += wins;
      stats[teamName].losses += losses;
    }

    // Преобразуем в массив и сортируем: больше побед, меньше поражений
    var list = Object.keys(stats).map(function(name) {
      return { name: name, w: stats[name].wins, l: stats[name].losses };
    }).sort(function(a, b) {
      if (b.w !== a.w) return b.w - a.w;
      return a.l - b.l;
    });

    list.forEach(function(item, idx) {
      var rank = idx + 1;
      var confClass = (teamConfig[item.name] && teamConfig[item.name].conf === 'west') ? 'west-team' : 'east-team';
      var avatarChar = item.name ? item.name.charAt(0).toUpperCase() : '?';

      var row = document.createElement('tr');
      row.innerHTML = `
        <td class="rank-cell">${rank}</td>
        <td class="team-name-cell ${confClass}">
          <div class="team-avatar">${avatarChar}</div>
          ${escapeHtml(item.name)}
        </td>
        <td><span class="stat-wins">${item.w}</span></td>
        <td><span class="stat-losses">${item.l}</span></td>
        <td class="stat-maps">—</td>
      `;
      tbody.appendChild(row);
    });
  }

  function escapeHtml(t) {
    if (!t) return '';
    return String(t).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#039;");
  }

  loadMatchesAndRender();
})();
</script>
</body>
</html>

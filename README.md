<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Рейтинг турнира</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

    body {
      margin: 0;
      padding: 0;
      background: transparent;
      font-family: 'Inter', sans-serif;
    }

    .rating-container {
      max-width: 600px;
      margin: 32px auto;
      padding: 20px;
      background: transparent;
      border: none;
      box-shadow: none;
    }

    .rating-title {
      color: #4a9eff;
      font-size: 20px;
      font-weight: 700;
      margin-bottom: 16px;
      text-transform: uppercase;
      letter-spacing: 1px;
      text-align: center;
    }

    .rating-table-wrapper {
      display: flex;
      justify-content: center;
      overflow-x: auto;
      margin: 0 auto;
    }

    .rating-table {
      width: 100%;
      min-width: 520px;
      border-collapse: collapse;
      color: #fff;
    }

    .rating-table th,
    .rating-table td {
      padding: 10px 14px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      text-align: left;
      vertical-align: middle;
      background: transparent;
    }

    .rating-table th {
      font-weight: 700;
      color: rgba(255, 255, 255, 0.9);
      text-transform: uppercase;
      font-size: 12px;
      letter-spacing: 0.5px;
      background: transparent;
    }

    .rating-table tbody tr:last-child td {
      border-bottom: none;
    }

    .pos-cell {
      width: 40px;
      text-align: center;
      font-weight: 800;
      font-size: 16px;
      color: rgba(255, 255, 255, 0.5);
    }
    .pos-cell.first { color: #ffd700; font-size: 18px; }
    .pos-cell.second { color: #C0C0C0; font-size: 17px; }
    .pos-cell.third { color: #CD7F32; font-size: 16px; }

    .name-cell {
      font-weight: 600;
      font-size: 15px;
    }
    .name-cell.first { color: #ffd700; font-weight: 800; }
    .name-cell.second { color: #C0C0C0; font-weight: 800; }
    .name-cell.third { color: #CD7F32; font-weight: 800; }

    .champ-cell,
    .finalist-cell,
    .points-cell {
      text-align: center;
    }

    .champ-cell {
      width: 90px;
      font-weight: 700;
      font-size: 15px;
    }
    .champ-cell.first { color: #ffd700; }
    .champ-cell.second { color: #C0C0C0; }
    .champ-cell.third { color: #CD7F32; }

    .finalist-cell {
      width: 90px;
      font-weight: 700;
      font-size: 15px;
    }
    .finalist-cell.first { color: #ffd700; }
    .finalist-cell.second { color: #C0C0C0; }
    .finalist-cell.third { color: #CD7F32; }

    .points-cell {
      width: 100px;
      font-weight: 700;
      color: #ffd700;
      font-size: 18px;
    }
    .points-cell.zero { color: rgba(255, 215, 0, 0.3); font-size: 14px; }

    .points-logo {
      width: 20px;
      height: 20px;
      border-radius: 50%;
      vertical-align: middle;
      margin-left: 6px;
    }

    .rating-empty {
      text-align: center;
      color: rgba(255, 255, 255, 0.3);
      font-size: 14px;
      padding: 24px;
      font-style: italic;
    }

    .rating-note {
      text-align: center;
      color: rgba(255, 255, 255, 0.4);
      font-size: 12px;
      margin-top: 12px;
    }

    .admin-section {
      text-align: center;
      margin-top: 20px;
      display: flex;
      justify-content: center;
      gap: 10px;
      flex-wrap: wrap;
    }
    .admin-section input {
      padding: 12px 18px;
      border: 1px solid rgba(255, 255, 255, 0.2);
      border-radius: 8px;
      background: rgba(0, 0, 0, 0.3);
      color: #fff;
      font-size: 14px;
      width: 200px;
      font-family: 'Inter', sans-serif;
    }
    .admin-section input::placeholder { color: rgba(255, 255, 255, 0.4); }
    .btn-admin {
      padding: 12px 26px;
      font-size: 14px;
      font-weight: 700;
      color: #fff;
      background: linear-gradient(135deg, #0a2a6b, #1a4a8b);
      border: 2px solid rgba(255, 255, 255, 0.3);
      border-radius: 50px;
      cursor: pointer;
      font-family: 'Inter', sans-serif;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .btn-admin:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 22px rgba(10, 42, 107, 0.6);
    }
    .btn-reset {
      padding: 10px 24px;
      font-size: 14px;
      font-weight: 700;
      color: #fff;
      background: linear-gradient(135deg, #c0392b, #e74c3c);
      border: 2px solid rgba(255, 255, 255, 0.2);
      border-radius: 8px;
      cursor: pointer;
      font-family: 'Inter', sans-serif;
      transition: transform 0.2s, box-shadow 0.2s;
      display: none;
      margin: 16px auto 0;
    }
    .btn-reset:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 18px rgba(192, 57, 43, 0.4);
    }
  </style>
</head>
<body>

  <div class="rating-container">
    <div class="rating-title">Турнирная таблица</div>

    <div class="rating-table-wrapper">
      <table class="rating-table">
        <thead>
          <tr>
            <th class="pos-cell">#</th>
            <th>Игрок</th>
            <th class="champ-cell">Чемпион</th>
            <th class="finalist-cell">Финалист</th>
            <th class="points-cell">Чак-чак</th>
          </tr>
        </thead>
        <tbody id="ratingBody">
          <tr>
            <td colspan="5" class="rating-empty">Итоги появятся после финала</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="rating-note">Победитель финала +2 чак-чака &middot; Финалист +1 чак-чак</div>

    <div class="admin-section">
      <input type="password" id="adminPassInput" placeholder="Админ-пароль" onkeydown="if(event.key==='Enter') toggleAdmin()">
      <button class="btn-admin" onclick="toggleAdmin()">Войти как админ</button>
    </div>
    <button class="btn-reset" id="btnReset" onclick="resetRating()">Сбросить чак-чаки</button>
  </div>

  <!-- Firebase SDK -->
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
      var LOGO_URL = 'https://4ak4ak.moy.su/logo1.jpg';

      function escapeHtml(t) {
        if (!t) return '';
        return String(t)
          .replace(/&/g, "&amp;")
          .replace(/</g, "&lt;")
          .replace(/>/g, "&gt;")
          .replace(/"/g, "&quot;")
          .replace(/'/g, "&#039;");
      }

      function renderRating(finalResult) {
        var body = document.getElementById('ratingBody');
        if (!finalResult || (!finalResult.winners && !finalResult.runnersUp)) {
          body.innerHTML = '<tr><td colspan="5" class="rating-empty">Итоги появятся после финала</td></tr>';
          return;
        }
        var winners = finalResult.winners || [];
        var runnersUp = finalResult.runnersUp || [];

        var stats = {};
        winners.forEach(function(nick) {
          if (!nick) return;
          if (!stats[nick]) stats[nick] = { champ: 0, finalist: 0, points: 0 };
          stats[nick].champ++;
          stats[nick].points += 2;
        });
        runnersUp.forEach(function(nick) {
          if (!nick) return;
          if (!stats[nick]) stats[nick] = { champ: 0, finalist: 0, points: 0 };
          stats[nick].finalist++;
          stats[nick].points += 1;
        });

        var arr = Object.keys(stats).map(function(nick) {
          return { nick: nick, champ: stats[nick].champ, finalist: stats[nick].finalist, points: stats[nick].points };
        });

        arr.sort(function(a, b) {
          if (b.points !== a.points) return b.points - a.points;
          if (b.champ !== a.champ) return b.champ - a.champ;
          return b.finalist - a.finalist;
        });

        var html = '';
        arr.forEach(function(row, i) {
          var pos = i + 1;
          var posClass = '';
          var nameClass = '';
          var champClass = '';
          var finalistClass = '';
          if (pos === 1) { posClass = nameClass = champClass = finalistClass = ' first'; }
          else if (pos === 2) { posClass = nameClass = champClass = finalistClass = ' second'; }
          else if (pos === 3) { posClass = nameClass = champClass = finalistClass = ' third'; }

          var pointsClass = (row.points === 0) ? ' zero' : '';
          var logoHtml = (row.points > 0) ? (' <img src="' + LOGO_URL + '" class="points-logo" alt="Чак-чак">') : '';

          html += '<tr>'
            + '<td class="pos-cell' + posClass + '">' + pos + '</td>'
            + '<td class="name-cell' + nameClass + '">' + escapeHtml(row.nick) + '</td>'
            + '<td class="champ-cell' + champClass + '">' + row.champ + '</td>'
            + '<td class="finalist-cell' + finalistClass + '">' + row.finalist + '</td>'
            + '<td class="points-cell' + pointsClass + '">' + row.points + logoHtml + '</td>'
            + '</tr>';
        });
        body.innerHTML = html;
      }

      window.toggleAdmin = function() {
        var p = document.getElementById('adminPassInput').value;
        var btnReset = document.getElementById('btnReset');
        if (!isAdmin) {
          if (p === ADMIN_PASSWORD) {
            isAdmin = true;
            document.getElementById('adminPassInput').value = '';
            btnReset.style.display = 'block';
            alert('Админ-режим включён!');
          } else {
            alert('Неверный пароль!');
          }
        } else {
          isAdmin = false;
          btnReset.style.display = 'none';
          alert('Админ-режим выключен.');
        }
      };

      window.resetRating = function() {
        if (!isAdmin) return;
        if (!confirm('Сбросить чак-чаки? Результат финала будет удалён.')) return;
        db.ref('playoff/finalResult').remove().then(function() {
          renderRating(null);
          alert('Чак-чаки сброшены!');
        });
      };

      db.ref('playoff/finalResult').on('value', function(snap) {
        renderRating(snap.val());
      });
    })();
  </script>
</body>
</html>

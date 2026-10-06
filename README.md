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
      overflow-y: auto;
      scrollbar-width: none;
      -ms-overflow-style: none;
    }
    body::-webkit-scrollbar {
      display: none;
    }

    .rating-container {
      max-width: 650px;
      margin: 0 auto;
      padding: 20px;
      background: rgba(10, 42, 107, 0.55);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border: 1px solid rgba(74, 158, 255, 0.45);
      border-radius: 14px;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
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
      margin: 0 auto;
    }

    .rating-scroll {
      max-height: 400px;
      overflow-y: auto;
      scrollbar-width: thin;
      scrollbar-color: rgba(74, 158, 255, 0.5) rgba(10, 42, 107, 0.3);
      border-radius: 8px;
    }
    .rating-scroll::-webkit-scrollbar {
      width: 8px;
    }
    .rating-scroll::-webkit-scrollbar-track {
      background: rgba(10, 42, 107, 0.3);
      border-radius: 4px;
    }
    .rating-scroll::-webkit-scrollbar-thumb {
      background: rgba(74, 158, 255, 0.5);
      border-radius: 4px;
    }
    .rating-scroll::-webkit-scrollbar-thumb:hover {
      background: rgba(74, 158, 255, 0.7);
    }

    .rating-table {
      width: 100%;
      border-collapse: collapse;
      color: #fff;
      table-layout: fixed;
    }

    .rating-table th,
    .rating-table td {
      padding: 0;
      border-bottom: 1px solid rgba(255, 255, 255, 0.12);
      text-align: center;
      vertical-align: middle;
      background: rgba(10, 42, 107, 0.65);
      white-space: nowrap;
    }

    .cell-content {
      display: block;
      padding: 6px 16px;
      text-align: center;
    }

    .rating-table th {
      font-weight: 700;
      color: rgba(255, 255, 255, 0.95);
      text-transform: uppercase;
      font-size: 12px;
      letter-spacing: 0.5px;
      position: sticky;
      top: 0;
      z-index: 1;
    }

    .rating-table tbody tr:last-child td {
      border-bottom: none;
    }

    .pos-cell {
      width: 40px;
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

    .name-cell a {
      color: inherit;
      text-decoration: none;
      transition: text-decoration 0.2s;
    }
    .name-cell a:hover {
      text-decoration: underline;
    }

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
      width: 110px;
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
      color: rgba(255, 255, 255, 0.35);
      font-size: 14px;
      padding: 24px;
      font-style: italic;
    }

    .rating-note {
      text-align: center;
      color: rgba(255, 255, 255, 0.45);
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
      background: rgba(255, 255, 255, 0.08);
      color: #fff;
      font-size: 14px;
      width: 200px;
      font-family: 'Inter', sans-serif;
    }
    .admin-section input::placeholder {
      color: rgba(255, 255, 255, 0.4);
    }
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
      box-shadow: 0 8px 28px rgba(10, 42, 107, 0.7);
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
      box-shadow: 0 6px 22px rgba(192, 57, 43, 0.5);
    }
  </style>
</head>
<body>

  <div class="rating-container">
    <div class="rating-title">Турнирная таблица</div>

    <div class="rating-scroll">
      <div class="rating-table-wrapper">
        <table class="rating-table">
          <thead>
            <tr>
              <th class="pos-cell"><span class="cell-content">#</span></th>
              <th><span class="cell-content">Игрок</span></th>
              <th class="champ-cell"><span class="cell-content">Чемпион</span></th>
              <th class="finalist-cell"><span class="cell-content">Финалист</span></th>
              <th class="points-cell"><span class="cell-content">Чак-чак</span></th>
            </tr>
          </thead>
          <tbody id="ratingBody">
            <tr>
              <td colspan="5" class="rating-empty">Итоги появятся после финала</td>
            </tr>
          </tbody>
        </table>
      </div>
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

      function renderRating(allResults) {
        var body = document.getElementById('ratingBody');

        var stats = {};

        allResults.forEach(function(finalResult) {
          if (!finalResult) return;
          var winners = finalResult.winners || [];
          var runnersUp = finalResult.runnersUp || [];

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
        });

        var hasData = Object.keys(stats).length > 0;
        if (!hasData) {
          body.innerHTML = '<tr><td colspan="5" class="rating-empty">Итоги появятся после финала</td></tr>';
          return;
        }

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
            + '<td class="pos-cell"><span class="cell-content">' + pos + '</span></td>'
            + '<td><span class="cell-content"><span class="name-cell' + nameClass + '"><a href="https://4ak4ak.moy.su/index/8-0-' + encodeURIComponent(row.nick) + '" target="_top" style="color:inherit;text-decoration:none;">' + escapeHtml(row.nick) + '</a></span></span></td>'
            + '<td class="champ-cell"><span class="cell-content"><span class="champ-cell' + champClass + '">' + row.champ + '</span></span></td>'
            + '<td class="finalist-cell"><span class="cell-content"><span class="finalist-cell' + finalistClass + '">' + row.finalist + '</span></span></td>'
            + '<td class="points-cell"><span class="cell-content"><span class="points-cell' + pointsClass + '">' + row.points + logoHtml + '</span></span></td>'
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
            document.querySelector('.admin-section').style.display = 'none';
            btnReset.style.display = 'block';
          } else {
            alert('Неверный пароль!');
          }
        } else {
          isAdmin = false;
          document.querySelector('.admin-section').style.display = 'flex';
          btnReset.style.display = 'none';
        }
      };

      window.resetRating = function() {
        if (!isAdmin) return;
        if (!confirm('Сбросить чак-чаки? Результаты всех финалов будут удалены.')) return;
        db.ref('playoff/tournaments').once('value').then(function(snap) {
          var tournaments = snap.val() || {};
          var updates = {};
          Object.keys(tournaments).forEach(function(tid) {
            if (tournaments[tid] && tournaments[tid].finalResult) {
              updates['playoff/tournaments/' + tid + '/finalResult'] = null;
            }
          });
          if (Object.keys(updates).length > 0) {
            db.ref().update(updates);
          }
          renderRating([]);
          alert('Чак-чаки сброшены!');
        });
      };

      function loadAndRender() {
        db.ref('playoff/tournaments').on('value', function(snap) {
          var tournaments = snap.val() || {};
          var allResults = [];
          Object.keys(tournaments).forEach(function(tid) {
            if (tournaments[tid] && tournaments[tid].finalResult) {
              allResults.push(tournaments[tid].finalResult);
            }
          });
          renderRating(allResults);
        });
      }

      loadAndRender();
    })();
  </script>
</body>
</html>

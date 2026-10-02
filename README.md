<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Рейтинг</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

* { box-sizing: border-box; }

body {
  margin: 0;
  padding: 0;
  background: transparent;
  font-family: 'Inter', sans-serif;
  /* Никакого overflow:hidden — скроллит сама страница */
}

.rating-wrapper {
  max-width: 700px;
  margin: 20px auto;
  padding: 24px;
  background: rgba(10, 10, 30, 0.85);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 14px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}

.rating-title {
  text-align: center;
  color: #fff;
  font-size: 24px;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 20px;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.8);
}

.rating-table {
  width: 100%;
  border-collapse: collapse;
}

.rating-table th {
  padding: 12px 10px;
  text-align: left;
  font-size: 12px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.8px;
  color: rgba(255, 255, 255, 0.5);
  border-bottom: 2px solid rgba(255, 215, 0, 0.3);
  white-space: nowrap;
}

.rating-table th.center { text-align: center; }

.rating-table td {
  padding: 10px 10px;
  font-size: 14px;
  color: #fff;
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  white-space: nowrap;
}

.rating-table td.center { text-align: center; }

.rating-table tr:hover td {
  background: rgba(255, 255, 255, 0.04);
}

.rank-cell {
  font-weight: 800;
  font-size: 16px;
  color: rgba(255, 255, 255, 0.4);
}

.rank-cell.gold { color: #ffd700; text-shadow: 0 0 8px rgba(255, 215, 0, 0.5); }
.rank-cell.silver { color: #c0c0c0; }
.rank-cell.bronze { color: #cd7f32; }

.nick-cell {
  font-weight: 600;
  color: #fff;
}

.wins-cell { color: #66bb6a; font-weight: 700; }
.finals-cell { color: #6fb3ff; font-weight: 700; }
.points-cell { color: #ffd700; font-weight: 800; font-size: 15px; }

.empty-msg {
  text-align: center;
  color: rgba(255, 255, 255, 0.4);
  font-size: 15px;
  padding: 40px 0;
}

.admin-section {
  text-align: center;
  margin-top: 20px;
}

.admin-section input {
  padding: 10px 16px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  background: rgba(0, 0, 0, 0.4);
  color: #fff;
  font-size: 14px;
  width: 180px;
  font-family: 'Inter', sans-serif;
  margin-right: 8px;
}

.admin-section input::placeholder { color: rgba(255, 255, 255, 0.3); }

.btn-reset {
  display: inline-block;
  padding: 10px 24px;
  font-size: 14px;
  font-weight: 700;
  color: #fff;
  background: linear-gradient(135deg, #c0392b, #e74c3c);
  border: 2px solid rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  cursor: pointer;
  font-family: 'Inter', sans-serif;
  margin-top: 10px;
}

.btn-reset:hover { transform: translateY(-2px); box-shadow: 0 6px 18px rgba(192, 57, 43, 0.4); }
.btn-reset:disabled { opacity: 0.5; cursor: not-allowed; transform: none; box-shadow: none; }

.admin-panel {
  display: none;
  text-align: center;
  margin-top: 16px;
}

.admin-login-row {
  display: flex;
  justify-content: center;
  gap: 10px;
  flex-wrap: wrap;
}

@media (max-width: 600px) {
  .rating-wrapper { margin: 10px; padding: 16px; }
  .rating-title { font-size: 18px; }
  .rating-table th, .rating-table td { padding: 8px 6px; font-size: 12px; }
}
</style>
</head>
<body>

<div class="rating-wrapper">
  <div class="rating-title">🏆 Рейтинг игроков</div>
  <div id="ratingContent">
    <p class="empty-msg">Загрузка...</p>
  </div>
  <div class="admin-section" id="adminSection">
    <div class="admin-login-row">
      <input type="password" id="adminPassInput" placeholder="Админ-пароль" onkeydown="if(event.key==='Enter') toggleAdmin()">
      <button class="btn-reset" style="background:linear-gradient(135deg,#0a2a6b,#1a4a8b);" onclick="toggleAdmin()">Войти</button>
    </div>
  </div>
  <div class="admin-panel" id="adminPanel">
    <button class="btn-reset" id="resetBtn" onclick="resetAllResults()">Сбросить все результаты</button>
  </div>
</div>

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
  var myNick = null;

  function getUrlParam(n) { var u = new URL(window.location.href); return u.searchParams.get(n); }
  myNick = getUrlParam('user');

  function escapeHtml(t) {
    if (!t) return '';
    return String(t).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#039;");
  }

  function buildRating(allFinalResults) {
    var players = {};

    Object.keys(allFinalResults).forEach(function(tId) {
      var fr = allFinalResults[tId];
      if (!fr) return;

      if (fr.winners && Array.isArray(fr.winners)) {
        fr.winners.forEach(function(nick) {
          if (!nick) return;
          if (!players[nick]) players[nick] = { wins: 0, finals: 0, points: 0 };
          players[nick].wins++;
          players[nick].points += 3;
        });
      }

      if (fr.runnersUp && Array.isArray(fr.runnersUp)) {
        fr.runnersUp.forEach(function(nick) {
          if (!nick) return;
          if (!players[nick]) players[nick] = { wins: 0, finals: 0, points: 0 };
          players[nick].finals++;
          players[nick].points += 1;
        });
      }
    });

    var arr = Object.keys(players).map(function(nick) {
      return { nick: nick, wins: players[nick].wins, finals: players[nick].finals, points: players[nick].points };
    });

    arr.sort(function(a, b) {
      if (b.points !== a.points) return b.points - a.points;
      if (b.wins !== a.wins) return b.wins - a.wins;
      return a.nick.localeCompare(b.nick);
    });

    return arr;
  }

  function renderRating(arr) {
    var c = document.getElementById('ratingContent');
    if (arr.length === 0) {
      c.innerHTML = '<p class="empty-msg">Пока нет результатов. Сыграйте финал турнира!</p>';
      return;
    }

    var html = '<table class="rating-table"><thead><tr>';
    html += '<th>#</th>';
    html += '<th>Игрок</th>';
    html += '<th class="center">Победы</th>';
    html += '<th class="center">Финалы</th>';
    html += '<th class="center">Чак-чак</th>';
    html += '</tr></thead><tbody>';

    arr.forEach(function(p, i) {
      var rankCls = '';
      if (i === 0) rankCls = 'gold';
      else if (i === 1) rankCls = 'silver';
      else if (i === 2) rankCls = 'bronze';

      var isMe = myNick && p.nick === myNick;
      var nickStyle = isMe ? ' style="color:#4a9eff;text-shadow:0 0 8px rgba(74,158,255,0.5);"' : '';
      var meBadge = isMe ? ' <span style="background:rgba(74,158,255,0.3);color:#4a9eff;font-size:9px;font-weight:700;padding:1px 5px;border-radius:3px;">ТЫ</span>' : '';

      html += '<tr>';
      html += '<td class="rank-cell ' + rankCls + '">' + (i + 1) + '</td>';
      html += '<td class="nick-cell"' + nickStyle + '>' + escapeHtml(p.nick) + meBadge + '</td>';
      html += '<td class="center wins-cell">' + p.wins + '</td>';
      html += '<td class="center finals-cell">' + p.finals + '</td>';
      html += '<td class="center points-cell">' + p.points + '</td>';
      html += '</tr>';
    });

    html += '</tbody></table>';
    c.innerHTML = html;
  }

  function loadAndRender() {
    db.ref('playoff/tournaments').once('value').then(function(snap) {
      var all = snap.val() || {};
      var allFR = {};

      Object.keys(all).forEach(function(tId) {
        if (all[tId] && all[tId].finalResult) {
          allFR[tId] = all[tId].finalResult;
        }
      });

      var arr = buildRating(allFR);
      renderRating(arr);
    });
  }

  window.toggleAdmin = function() {
    var p = document.getElementById('adminPassInput').value;
    if (!isAdmin) {
      if (p === ADMIN_PASSWORD) {
        isAdmin = true;
        document.getElementById('adminPassInput').value = '';
        document.getElementById('adminPanel').style.display = 'block';
        document.getElementById('adminSection').style.display = 'none';
        alert('Админ-режим включён!');
      } else {
        alert('Неверный пароль!');
      }
    } else {
      isAdmin = false;
      document.getElementById('adminPanel').style.display = 'none';
      document.getElementById('adminSection').style.display = 'block';
      alert('Админ-режим выключен.');
    }
  };

  window.resetAllResults = function() {
    if (!isAdmin) return;
    if (!confirm('Удалить результаты финалов во ВСЕХ турнирах? Это необратимо!')) return;

    db.ref('playoff/tournaments').once('value').then(function(snap) {
      var all = snap.val() || {};
      var updates = {};
      Object.keys(all).forEach(function(tId) {
        if (all[tId] && all[tId].finalResult) {
          updates['playoff/tournaments/' + tId + '/finalResult'] = null;
        }
      });
      db.ref().update(updates).then(function() {
        alert('Все результаты сброшены!');
        loadAndRender();
      });
    });
  };

  // Слушаем изменения в реальном времени
  db.ref('playoff/tournaments').on('value', function(snap) {
    var all = snap.val() || {};
    var allFR = {};
    Object.keys(all).forEach(function(tId) {
      if (all[tId] && all[tId].finalResult) {
        allFR[tId] = all[tId].finalResult;
      }
    });
    var arr = buildRating(allFR);
    renderRating(arr);
  });

  loadAndRender();
})();
</script>

</body>
</html>

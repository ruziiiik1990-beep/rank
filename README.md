
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Рейтинг турнира</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
* { margin: 0; padding: 0; box-sizing: border-box; }
body { background: transparent; font-family: 'Inter', sans-serif; }

.rating-container {
  max-width: 600px; margin: 0 auto; padding: 24px;
  background: rgba(10,42,107,0.3);
  backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px);
  border: 1px solid rgba(74,158,255,0.35);
  border-radius: 14px; box-shadow: 0 4px 20px rgba(10,42,107,0.3);
}
.rating-title {
  text-align: center; color: #4a9eff;
  font-size: 22px; font-weight: 700; text-transform: uppercase;
  letter-spacing: 1px; margin-bottom: 20px;
}

.rating-table {
  width: 100%; border-collapse: collapse; color: #fff;
  background: rgba(0,0,0,0.35); border-radius: 8px; overflow: hidden;
}
.rating-table th, .rating-table td {
  padding: 12px 14px; border-bottom: 1px solid rgba(255,255,255,0.08);
  text-align: left; vertical-align: middle;
}
.rating-table th {
  font-weight: 700; color: rgba(255,255,255,0.9);
  text-transform: uppercase; font-size: 12px; letter-spacing: 0.5px;
  background: rgba(74,158,255,0.15);
}
.rating-table tr:last-child td { border-bottom: none; }
.rating-table tr:hover { background: rgba(255,255,255,0.05); }

.rank-cell { width: 40px; text-align: center; font-weight: 700; color: rgba(255,255,255,0.5); }
.rank-cell.first { color: #ffd700; font-size: 18px; }
.rank-cell.second { color: #c0c0c0; font-size: 16px; }
.rank-cell.third { color: #cd7f32; font-size: 16px; }

.name-cell { font-weight: 600; font-size: 15px; }

.points-cell { width: 80px; text-align: right; font-weight: 700; color: #ffd700; font-size: 18px; }
.points-cell.zero { color: rgba(255,255,255,0.2); font-size: 14px; }

.rating-empty { text-align: center; color: rgba(255,255,255,0.4); font-size: 14px; padding: 32px; font-style: italic; }
.rating-loading { text-align: center; color: rgba(255,255,255,0.4); font-size: 14px; padding: 32px; }
.rating-note { text-align: center; color: rgba(255,255,255,0.35); font-size: 12px; margin-top: 16px; }

.admin-section { margin-top: 24px; text-align: center; }
.admin-section input {
  padding: 10px 14px; border: 1px solid rgba(255,255,255,0.2); border-radius: 8px;
  background: rgba(0,0,0,0.4); color: #fff; font-size: 14px; width: 180px;
  font-family: 'Inter', sans-serif; margin-right: 8px;
}
.admin-section input::placeholder { color: rgba(255,255,255,0.4); }
.btn-admin {
  padding: 10px 20px; font-size: 14px; font-weight: 700;
  color: #fff; background: linear-gradient(135deg, #0a2a6b, #1a4a8b);
  border: 2px solid rgba(255,255,255,0.2); border-radius: 8px;
  cursor: pointer; font-family: 'Inter', sans-serif;
  transition: transform 0.2s, box-shadow 0.2s; margin: 4px;
}
.btn-admin:hover { transform: translateY(-2px); box-shadow: 0 4px 14px rgba(10,42,107,0.4); }
.btn-reset {
  padding: 10px 20px; font-size: 14px; font-weight: 700;
  color: #fff; background: linear-gradient(135deg, #c0392b, #e74c3c);
  border: 2px solid rgba(255,255,255,0.2); border-radius: 8px;
  cursor: pointer; font-family: 'Inter', sans-serif;
  transition: transform 0.2s, box-shadow 0.2s; display: none; margin: 4px auto;
}
.btn-reset:hover { transform: translateY(-2px); box-shadow: 0 6px 18px rgba(192,57,43,0.4); }
</style>
</head>
<body>

<div class="rating-container">
  <div class="rating-title">Рейтинг турнира</div>
  <table class="rating-table">
    <thead>
      <tr>
        <th class="rank-cell">#</th>
        <th>Игрок</th>
        <th class="points-cell">Очки</th>
      </tr>
    </thead>
    <tbody id="ratingBody">
      <tr><td colspan="3" class="rating-loading">Загрузка...</td></tr>
    </tbody>
  </table>
  <div class="rating-note">Победитель финала: +2 очка &middot; Финалист: +1 очко</div>

  <div class="admin-section">
    <input type="password" id="adminPassInput" placeholder="Админ-пароль" onkeydown="if(event.key==='Enter') toggleAdmin()">
    <button class="btn-admin" onclick="toggleAdmin()">Войти</button>
    <br>
    <button class="btn-reset" id="btnReset" onclick="resetRating()">Сбросить очки</button>
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

  function escapeHtml(t) {
    if (!t) return '';
    return String(t).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#039;");
  }

  function renderRating(finalResult) {
    var body = document.getElementById('ratingBody');
    if (!finalResult || (!finalResult.winners && !finalResult.runnersUp)) {
      body.innerHTML = '<tr><td colspan="3" class="rating-empty">Итоги появятся после финала</td></tr>';
      return;
    }
    var winners = finalResult.winners || [];
    var runnersUp = finalResult.runnersUp || [];
    var scores = {};
    winners.forEach(function(nick) { if (nick) scores[nick] = (scores[nick]||0) + 2; });
    runnersUp.forEach(function(nick) { if (nick) scores[nick] = (scores[nick]||0) + 1; });
    var arr = Object.keys(scores).map(function(nick) {
      return { nick: nick, points: scores[nick] };
    }).sort(function(a, b) { return b.points - a.points; });
    var html = '';
    arr.forEach(function(row, i) {
      var pos = i + 1; var rankClass = '';
      if (pos === 1) rankClass = ' first';
      else if (pos === 2) rankClass = ' second';
      else if (pos === 3) rankClass = ' third';
      var pointsClass = row.points > 0 ? '' : ' zero';
      html += '<tr><td class="rank-cell'+rankClass+'">'+pos+'</td><td class="name-cell">'+escapeHtml(row.nick)+'</td><td class="points-cell'+pointsClass+'">'+row.points+'</td></tr>';
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
        btnReset.style.display = 'inline-block';
        alert('Админ-режим включён!');
      } else { alert('Неверный пароль!'); }
    } else {
      isAdmin = false;
      btnReset.style.display = 'none';
      alert('Админ-режим выключен.');
    }
  };

  window.resetRating = function() {
    if (!isAdmin) return;
    if (!confirm('Сбросить очки турнира? Результат финала будет удалён.')) return;
    db.ref('playoff/finalResult').remove().then(function() {
      renderRating(null);
      alert('Очки сброшены!');
    });
  };

  db.ref('playoff/finalResult').on('value', function(snap) {
    renderRating(snap.val());
  });
})();
</script>
</body>
</html>

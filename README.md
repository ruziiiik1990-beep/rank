<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Рейтинг турнира</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
* { margin: 0; padding: 0; box-sizing: border-box; }
body { background: transparent !important; font-family: 'Inter', sans-serif; }

.rating-container {
  max-width: 600px; margin: 0 auto; padding: 24px;
  background: rgba(10,42,107,0.3);ф<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Рейтинг турнира</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
* { margin: 0; padding: 0; box-sizing: border-box; }
body { background: transparent !important; font-family: 'Inter', sans-serif; }

.rating-container {
  max-width: 600px; margin: 0 auto; padding: 24px;
  background: rgba(10,42,107,0.3);
  backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px);
  border: 1px solid rgba(74,158,255,0.35);
  border-radius: 14px; box-shadow: 0 4px 20px rgba(10,42,107,0.3);
}
.rating-title {
  text-align: center; color: #ffa726;
  font-size: 22px; font-weight: 700; text-transform: uppercase;
  letter-spacing: 1px; margin-bottom: 20px;
}

.rating-table {
  width: 100%; border-collapse: collapse;
  background: transparent !important;
  border-radius: 8px; overflow: hidden;
}
.rating-table th {
  padding: 12px 14px; border-bottom: 1px solid rgba(255,167,38,0.2);
  text-align: left; vertical-align: middle;
  font-weight: 700; color: #ffa726;
  text-transform: uppercase; font-size: 12px; letter-spacing: 0.5px;
  background: transparent !important;
}
.rating-table td {
  padding: 12px 14px; border-bottom: 1px solid rgba(255,167,38,0.1);
  text-align: left; vertical-align: middle;
  background: transparent !important;
}
.rating-table tr:last-child td { border-bottom: none; }

.rank-cell { width: 40px; text-align: center; font-weight: 700; font-size: 16px; color: #ffffff; }
.rank-cell.first { color: #FFD700; font-size: 18px; font-weight: 800; }
.rank-cell.second { color: #C0C0C0; font-size: 17px; font-weight: 800; }
.rank-cell.third { color: #CD7F32; font-size: 16px; font-weight: 800; }

.name-cell { font-weight: 600; font-size: 15px; color: #ffa726; }
.name-cell.first { color: #FFD700; font-weight: 800; }
.name-cell.second { color: #C0C0C0; font-weight: 800; }
.name-cell.third { color: #CD7F32; font-weight: 800; }

.points-cell { width: 120px; text-align: right; font-weight: 700; color: #ffb74d; font-size: 18px; }
.points-cell.zero { color: rgba(255,167,38,0.3); font-size: 14px; }

.points-logo { width: 20px; height: 20px; border-radius: 50%; vertical-align: middle; margin-left: 6px; }

.rating-empty { text-align: center; color: #ffa726; font-size: 14px; padding: 32px; font-style: italic; opacity: 0.6; }
.rating-loading { text-align: center; color: #ffa726; font-size: 14px; padding: 32px; opacity: 0.6; }
.rating-note { text-align: center; color: #ffa726; font-size: 12px; margin-top: 16px; opacity: 0.7; }

.admin-section { margin-top: 24px; text-align: center; }
.admin-section input {
  padding: 10px 14px; border: 1px solid rgba(255,167,38,0.3); border-radius: 8px;
  background: rgba(0,0,0,0.4); color: #ffa726; font-size: 14px; width: 180px;
  font-family: 'Inter', sans-serif; margin-right: 8px;
}
.admin-section input::placeholder { color: rgba(255,167,38,0.4); }
.btn-admin {
  padding: 10px 20px; font-size: 14px; font-weight: 700;
  color: #fff; background: linear-gradient(135deg, #e65100, #f57c00);
  border: 2px solid rgba(255,167,38,0.3); border-radius: 8px;
  cursor: pointer; font-family: 'Inter', sans-serif;
  transition: transform 0.2s, box-shadow 0.2s; margin: 4px;
}
.btn-admin:hover { transform: translateY(-2px); box-shadow: 0 4px 14px rgba(230,81,0,0.4); }
.btn-reset {
  padding: 10px 20px; font-size: 14px; font-weight: 700;
  color: #fff; background: linear-gradient(135deg, #c0392b, #e74c3c);
  border: 2px solid rgba(255,167,38,0.3); border-radius: 8px;
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
        <th class="points-cell">Чак-чак</th>
      </tr>
    </thead>
    <tbody id="ratingBody">
      <tr><td colspan="3" class="rating-loading">Загрузка...</td></tr>
    </tbody>
  </table>
  <div class="rating-note">Победитель финала: +2 чак-чака &middot; Финалист: +1 чак-чак</div>

  <div class="admin-section">
    <input type="password" id="adminPassInput" placeholder="Админ-пароль" onkeydown="if(event.key==='Enter') toggleAdmin()">
    <button class="btn-admin" onclick="toggleAdmin()">Войти</button>
    <br>
    <button class="btn-reset" id="btnReset" onclick="resetRating()">Сбросить чак-чаки</button>
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
  var LOGO_URL = 'https://4ak4ak.moy.su/logo1.jpg';

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
      var pos = i + 1;
      var rankClass = '';
      var nameClass = '';
      if (pos === 1) { rankClass = ' first'; nameClass = ' first'; }
      else if (pos === 2) { rankClass = ' second'; nameClass = ' second'; }
      else if (pos === 3) { rankClass = ' third'; nameClass = ' third'; }
      var pointsClass = row.points > 0 ? '' : ' zero';
      var logoHtml = row.points > 0 ? ' <img src="' + LOGO_URL + '" class="points-logo" alt="">' : '';
      html += '<tr>'
        + '<td class="rank-cell' + rankClass + '">' + pos + '</td>'
        + '<td class="name-cell' + nameClass + '">' + escapeHtml(row.nick) + '</td>'
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

  backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px);
  border: 1px solid rgba(74,158,255,0.35);
  border-radius: 14px; box-shadow: 0 4px 20px rgba(10,42,107,0.3);
}
.rating-title {
  text-align: center; color: #ffa726;
  font-size: 22px; font-weight: 700; text-transform: uppercase;
  letter-spacing: 1px; margin-bottom: 20px;
}

.rating-table {
  width: 100%; border-collapse: collapse;
  background: transparent !important;
  border-radius: 8px; overflow: hidden;
}
.rating-table th {
  padding: 12px 14px; border-bottom: 1px solid rgba(255,167,38,0.2);
  text-align: left; vertical-align: middle;
  font-weight: 700; color: #ffa726;
  text-transform: uppercase; font-size: 12px; letter-spacing: 0.5px;
  background: transparent !important;
}
.rating-table td {
  padding: 12px 14px; border-bottom: 1px solid rgba(255,167,38,0.1);
  text-align: left; vertical-align: middle;
  background: transparent !important;
}
.rating-table tr:last-child td { border-bottom: none; }

.rank-cell { width: 40px; text-align: center; font-weight: 700; font-size: 16px; color: #ffffff; }
.rank-cell.first { color: #FFD700; font-size: 18px; font-weight: 800; }
.rank-cell.second { color: #C0C0C0; font-size: 17px; font-weight: 800; }
.rank-cell.third { color: #CD7F32; font-size: 16px; font-weight: 800; }

.name-cell { font-weight: 600; font-size: 15px; color: #ffa726; }

.points-cell { width: 120px; text-align: right; font-weight: 700; color: #ffb74d; font-size: 18px; }
.points-cell.zero { color: rgba(255,167,38,0.3); font-size: 14px; }

.points-logo { width: 20px; height: 20px; border-radius: 50%; vertical-align: middle; margin-left: 6px; }

.rating-empty { text-align: center; color: #ffa726; font-size: 14px; padding: 32px; font-style: italic; opacity: 0.6; }
.rating-loading { text-align: center; color: #ffa726; font-size: 14px; padding: 32px; opacity: 0.6; }
.rating-note { text-align: center; color: #ffa726; font-size: 12px; margin-top: 16px; opacity: 0.7; }

.admin-section { margin-top: 24px; text-align: center; }
.admin-section input {
  padding: 10px 14px; border: 1px solid rgba(255,167,38,0.3); border-radius: 8px;
  background: rgba(0,0,0,0.4); color: #ffa726; font-size: 14px; width: 180px;
  font-family: 'Inter', sans-serif; margin-right: 8px;
}
.admin-section input::placeholder { color: rgba(255,167,38,0.4); }
.btn-admin {
  padding: 10px 20px; font-size: 14px; font-weight: 700;
  color: #fff; background: linear-gradient(135deg, #e65100, #f57c00);
  border: 2px solid rgba(255,167,38,0.3); border-radius: 8px;
  cursor: pointer; font-family: 'Inter', sans-serif;
  transition: transform 0.2s, box-shadow 0.2s; margin: 4px;
}
.btn-admin:hover { transform: translateY(-2px); box-shadow: 0 4px 14px rgba(230,81,0,0.4); }
.btn-reset {
  padding: 10px 20px; font-size: 14px; font-weight: 700;
  color: #fff; background: linear-gradient(135deg, #c0392b, #e74c3c);
  border: 2px solid rgba(255,167,38,0.3); border-radius: 8px;
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
        <th class="points-cell">Чак-чак</th>
      </tr>
    </thead>
    <tbody id="ratingBody">
      <tr><td colspan="3" class="rating-loading">Загрузка...</td></tr>
    </tbody>
  </table>
  <div class="rating-note">Победитель финала: +2 чак-чака &middot; Финалист: +1 чак-чак</div>

  <div class="admin-section">
    <input type="password" id="adminPassInput" placeholder="Админ-пароль" onkeydown="if(event.key==='Enter') toggleAdmin()">
    <button class="btn-admin" onclick="toggleAdmin()">Войти</button>
    <br>
    <button class="btn-reset" id="btnReset" onclick="resetRating()">Сбросить чак-чаки</button>
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
  var LOGO_URL = 'https://4ak4ak.moy.su/logo1.jpg';

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
      var logoHtml = row.points > 0 ? ' <img src="' + LOGO_URL + '" class="points-logo" alt="">' : '';
      html += '<tr><td class="rank-cell'+rankClass+'">'+pos+'</td><td class="name-cell">'+escapeHtml(row.nick)+'</td><td class="points-cell'+pointsClass+'">'+row.points+logoHtml+'</td></tr>';
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

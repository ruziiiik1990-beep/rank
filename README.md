<!DOCTYPE html>
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
  border-radius: 14px;
  box-shadow: 0 4px 20px rgba(10,42,107,0.3);
}

.rating-title {
  text-align: center; color: #4a9eff;
  font-size: 22px; font-weight: 700; text-transform: uppercase;
  letter-spacing: 1px; margin-bottom: 20px;
}

.rating-table { width: 100%; border-collapse: collapse; color: #fff; }
.rating-table th, .rating-table td {
  padding: 12px 14px; border-bottom: 1px solid rgba(255,255,255,0.1);
  text-align: left; vertical-align: middle;
}
.rating-table th {
  font-weight: 700; color: rgba(255,255,255,0.9);
  text-transform: uppercase; font-size: 12px; letter-spacing: 0.5px;
}
.rating-table tr:last-child td { border-bottom: none; }
.rating-table tr:hover { background: rgba(255,255,255,0.03); }

.rank-cell { width: 40px; text-align: center; font-weight: 700; color: rgba(255,255,255,0.5); }
.rank-cell.first { color: #ffd700; font-size: 18px; }
.rank-cell.second { color: #c0c0c0; font-size: 16px; }
.rank-cell.third { color: #cd7f32; font-size: 16px; }

.name-cell { font-weight: 600; font-size: 15px; }
.champion-badge {
  display: inline-block; background: linear-gradient(135deg, #ffd700, #ffb300);
  color: #1a1a2e; font-size: 9px; font-weight: 800;
  padding: 2px 6px; border-radius: 4px; margin-left: 6px; text-transform: uppercase;
}
.runner-up-badge {
  display: inline-block; background: rgba(192,192,192,0.2); color: #c0c0c0;
  font-size: 9px; font-weight: 700; padding: 2px 6px; border-radius: 4px; margin-left: 6px; text-transform: uppercase;
}

.points-cell { width: 80px; text-align: right; font-weight: 700; color: #ffd700; font-size: 18px; }
.points-cell.zero { color: rgba(255,255,255,0.2); font-size: 14px; }

.rating-empty { text-align: center; color: rgba(255,255,255,0.3); font-size: 14px; padding: 32px; font-style: italic; }
.rating-loading { text-align: center; color: rgba(255,255,255,0.4); font-size: 14px; padding: 32px; }
.rating-note { text-align: center; color: rgba(255,255,255,0.35); font-size: 12px; margin-top: 16px; }
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
    winners.forEach(function(nick) {
      if (nick) scores[nick] = (scores[nick] || 0) + 2;
    });
    runnersUp.forEach(function(nick) {
      if (nick) scores[nick] = (scores[nick] || 0) + 1;
    });

    var arr = Object.keys(scores).map(function(nick) {
      return { nick: nick, points: scores[nick] };
    }).sort(function(a, b) {
      return b.points - a.points;
    });

    var html = '';
    arr.forEach(function(row, i) {
      var pos = i + 1;
      var rankClass = '';
      if (pos === 1) rankClass = ' first';
      else if (pos === 2) rankClass = ' second';
      else if (pos === 3) rankClass = ' third';

      var badge = '';
      if (winners.indexOf(row.nick) !== -1) {
        badge = ' <span class="champion-badge">ЧЕМПИОН</span>';
      } else if (runnersUp.indexOf(row.nick) !== -1) {
        badge = ' <span class="runner-up-badge">ФИНАЛИСТ</span>';
      }

      var pointsClass = row.points > 0 ? '' : ' zero';

      html += '<tr>'
        + '<td class="rank-cell' + rankClass + '">' + pos + '</td>'
        + '<td class="name-cell">' + escapeHtml(row.nick) + badge + '</td>'
        + '<td class="points-cell' + pointsClass + '">' + row.points + '</td>'
        + '</tr>';
    });

    body.innerHTML = html;
  }

  db.ref('playoff/finalResult').on('value', function(snap) {
    renderRating(snap.val());
  });
})();
</script>
</body>
</html>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

body { margin: 0; padding: 0; background: transparent; font-family: 'Inter', sans-serif; }

.tournament-wrapper {
  background-image: url('https://4ak4ak.moy.su/Tchak.jpg');
  background-size: cover; background-position: center center; background-repeat: no-repeat;
  padding: 30px 0; border-radius: 12px; position: relative; overflow: hidden;
}
.tournament-wrapper::before {
  content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 100%;
  background: rgba(0,0,0,0.5); z-index: 0;
}
.tournament-wrapper > * { position: relative; z-index: 1; }

.tournament-title {
  text-align: center; color: #fff; font-size: 28px; font-weight: 800;
  text-transform: uppercase; letter-spacing: 2px; margin-bottom: 24px;
  text-shadow: 0 2px 8px rgba(0,0,0,0.8);
}

.bracket-row { display: flex; gap: 16px; justify-content: center; align-items: stretch; flex-wrap: wrap; }
.bracket-col { flex: 1; min-width: 180px; max-width: 22%; display: flex; flex-direction: column; }
.bracket-col.final-col { max-width: 260px; }
.bracket-col.semifinal-col, .bracket-col.final-col { justify-content: center; }

.conf-label { text-align: center; font-size: 16px; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 12px; padding-bottom: 8px; border-bottom: 1px solid rgba(255,255,255,0.2); }
.conf-label.west { color: #6fb3ff; }
.conf-label.east { color: #ff8a65; }

.round-label { text-align: center; color: rgba(255,255,255,0.55); font-size: 12px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.8px; margin-bottom: 8px; }

.match { display: flex; flex-direction: column; background: rgba(255,255,255,0.06); border-radius: 6px; overflow: hidden; margin: 0 auto 8px; width: 100%; border: 1px solid rgba(255,255,255,0.08); box-sizing: border-box; cursor: pointer; transition: border-color 0.2s, background 0.2s, transform 0.15s; }
.match:hover { border-color: rgba(255,215,0,0.4); background: rgba(255,255,255,0.1); transform: translateY(-2px); }
.match.is-mine { border-color: rgba(74,158,255,0.6); box-shadow: 0 0 12px rgba(74,158,255,0.4); }

.match-row { display: flex; justify-content: space-between; align-items: center; padding: 8px 12px; color: #fff; font-size: 13px; font-weight: 500; transition: background 0.2s; }
.match-row.winner { background: rgba(76,175,80,0.3); font-weight: 700; }
.match-row.winner::after { content: '\2713'; color: #66bb6a; margin-left: 6px; }
.match-row.is-mine-row { background: rgba(74,158,255,0.2); }
.match-team { display: flex; align-items: center; gap: 6px; }
.team-seed { background: rgba(255,255,255,0.12); border-radius: 3px; padding: 2px 5px; font-size: 11px; font-weight: 600; color: rgba(255,255,255,0.7); min-width: 18px; text-align: center; }
.match-score { font-weight: 700; font-size: 14px; min-width: 22px; text-align: center; }
.match-divider { height: 1px; background: rgba(255,255,255,0.08); }

.final-box { background: rgba(0,0,0,0.55); border-radius: 12px; padding: 20px; border: 2px solid rgba(255,215,0,0.4); text-align: center; width: 100%; box-sizing: border-box; }
.final-title { color: #ffd700; font-size: 18px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 14px; text-shadow: 0 2px 8px rgba(0,0,0,0.8); }
.final-match { background: rgba(255,215,0,0.08); border: 1px solid rgba(255,215,0,0.2); }
.final-match:hover { border-color: rgba(255,215,0,0.6); }

.join-section { text-align: center; margin: 24px 0 20px; }
.btn-join { display: inline-block; padding: 14px 40px; font-size: 17px; font-weight: 700; color: #fff; background: linear-gradient(135deg, #0a2a6b, #1a4a8b); border: 2px solid rgba(255,255,255,0.3); border-radius: 50px; cursor: pointer; transition: transform 0.2s, box-shadow 0.2s, background 0.3s; box-shadow: 0 4px 14px rgba(10,42,107,0.4); font-family: 'Inter', sans-serif; }
.btn-join:hover { transform: translateY(-2px); box-shadow: 0 8px 22px rgba(10,42,107,0.6); background: linear-gradient(135deg, #1a4a8b, #2a6abb); }
.btn-join:disabled { opacity: 0.5; cursor: not-allowed; transform: none; box-shadow: none; }
.btn-join:disabled:hover { transform: none; box-shadow: none; background: linear-gradient(135deg, #0a2a6b, #1a4a8b); }
.joined-msg { text-align: center; color: #4a9eff; font-weight: 700; font-size: 17px; margin-bottom: 20px; text-shadow: 0 0 10px rgba(74,158,255,0.5); }
.guest-warning { text-align: center; margin-bottom: 20px; }
.guest-warning-text { font-weight: 800; background: linear-gradient(180deg, transparent 45%, #0a2a6bcc 45%); padding: 3px 10px; border-radius: 5px; color: #fff; text-shadow: 0 0 5px #0a2a6b, 0 0 10px #0a2a6b; display: inline-block; font-size: 15px; }
.tournament-full-msg { text-align: center; color: rgba(255,215,0,0.7); font-weight: 700; font-size: 15px; margin-bottom: 20px; text-shadow: 0 0 10px rgba(255,215,0,0.3); }
.admin-login-row { text-align: center; margin: 20px 0; display: flex; justify-content: center; gap: 10px; flex-wrap: wrap; }
.admin-login-row input { padding: 12px 18px; border: 1px solid rgba(255,255,255,0.2); border-radius: 8px; background: rgba(0,0,0,0.4); color: #fff; font-size: 14px; width: 200px; font-family: 'Inter', sans-serif; }
.admin-login-row input::placeholder { color: rgba(255,255,255,0.4); }
.admin-panel { max-width: 850px; margin: 0 auto 20px; padding: 22px; background: rgba(10,42,107,0.3); backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px); border: 1px solid rgba(74,158,255,0.35); border-radius: 14px; box-shadow: 0 4px 20px rgba(10,42,107,0.3); }
.admin-panel h3 { font-size: 18px; margin-bottom: 12px; color: #4a9eff; text-shadow: 0 0 10px rgba(74,158,255,0.5); font-weight: 700; }
.admin-hint { font-size: 13px; color: rgba(255,255,255,0.5); }
.admin-active-badge { display: inline-block; background: linear-gradient(135deg, #27ae60, #2ecc71); color: #fff; font-size: 12px; padding: 4px 12px; border-radius: 20px; font-weight: 700; margin-left: 10px; box-shadow: 0 2px 8px rgba(39,174,96,0.4); }

.team-modal-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.75); z-index: 9999; justify-content: center; align-items: center; }
.team-modal-overlay.active { display: flex; }
.team-modal { background: #1a1a2e; border: 1px solid rgba(255,255,255,0.15); border-radius: 14px; padding: 28px 32px; width: 800px; max-width: 92vw; max-height: 88vh; overflow-y: auto; box-shadow: 0 12px 40px rgba(0,0,0,0.6); animation: modalIn 0.25s ease; }
@keyframes modalIn { from { transform: scale(0.92); opacity: 0; } to { transform: scale(1); opacity: 1; } }
.team-modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; padding-bottom: 14px; border-bottom: 1px solid rgba(255,255,255,0.15); }
.team-modal-matchup { font-size: 18px; font-weight: 800; color: #fff; text-transform: uppercase; letter-spacing: 1px; }
.team-modal-close { background: rgba(255,255,255,0.1); border: none; color: #fff; font-size: 22px; cursor: pointer; width: 34px; height: 34px; border-radius: 50%; display: flex; align-items: center; justify-content: center; transition: background 0.2s; line-height: 1; }
.team-modal-close:hover { background: rgba(255,80,80,0.4); }

.participants-grid { display: flex; gap: 16px; justify-content: space-between; align-items: flex-start; }
.participants-col { flex: 1; min-width: 0; display: flex; flex-direction: column; }
.participants-col.is-mine-col { border: 2px solid rgba(74,158,255,0.5); border-radius: 10px; padding: 12px; box-shadow: 0 0 14px rgba(74,158,255,0.3); animation: pulse-mine 2.5s ease-in-out infinite; }
@keyframes pulse-mine { 0%,100% { box-shadow: 0 0 10px rgba(74,158,255,0.3); } 50% { box-shadow: 0 0 22px rgba(74,158,255,0.6); } }
.participants-col-title { font-size: 16px; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; text-align: center; margin-bottom: 14px; padding-bottom: 10px; border-bottom: 1px solid rgba(255,255,255,0.15); }
.participants-col.left .participants-col-title { color: #6fb3ff; }
.participants-col.right .participants-col-title { color: #ff8a65; }
.participant-list { list-style: none; padding: 0; margin: 0 0 10px; display: flex; flex-direction: column; gap: 8px; }
.participant-item { display: flex; align-items: center; gap: 10px; background: rgba(255,255,255,0.06); border-radius: 8px; padding: 8px 12px; color: #fff; font-size: 13px; font-weight: 500; position: relative; flex-wrap: wrap; }
.participant-item.is-me { background: rgba(74,158,255,0.2); border: 1px solid rgba(74,158,255,0.5); }
.participant-item.is-me .participant-avatar { box-shadow: 0 0 8px rgba(74,158,255,0.7); }
.participant-avatar { width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 14px; font-weight: 700; color: #fff; flex-shrink: 0; }
.participants-col.left .participant-avatar { background: linear-gradient(135deg, #4a90d9, #6fb3ff); }
.participants-col.right .participant-avatar { background: linear-gradient(135deg, #e07845, #ff8a65); }
.participant-num { color: rgba(255,255,255,0.45); font-size: 11px; font-weight: 600; }
.participant-del { position: absolute; right: 6px; top: 50%; transform: translateY(-50%); background: rgba(255,80,80,0.2); border: none; color: #ff6b6b; font-size: 16px; cursor: pointer; width: 24px; height: 24px; border-radius: 50%; display: none; align-items: center; justify-content: center; line-height: 1; }
.participant-item:hover .participant-del { display: flex; }
.participant-del:hover { background: rgba(255,80,80,0.4); }

.winner-logo-section { display: flex; justify-content: center; padding: 8px 0 4px; }
.winner-logo-section img { width: 32px; height: 32px; border-radius: 50%; border: 2px solid #66bb6a; box-shadow: 0 0 12px rgba(102,187,106,0.7); animation: pulse-win 2s ease-in-out infinite; }
.winner-logo-section.admin-can-cancel img { cursor: pointer; border-color: #ff6b6b; box-shadow: 0 0 12px rgba(255,107,107,0.6); }
.winner-logo-section.admin-can-cancel img:hover { border-color: #ff3333; box-shadow: 0 0 18px rgba(255,51,51,0.9); transform: scale(1.15); }
.winner-logo-section.admin-can-cancel::after { content: '\2715'; color: #ff6b6b; font-size: 10px; font-weight: 700; margin-left: 4px; align-self: center; }
@keyframes pulse-win { 0%,100% { box-shadow: 0 0 8px rgba(102,187,106,0.5); } 50% { box-shadow: 0 0 18px rgba(102,187,106,0.9); } }

.admin-add-row { display: flex; gap: 8px; margin-top: 10px; }
.admin-add-row input { flex: 1; padding: 8px 10px; border: 1px solid rgba(255,255,255,0.15); border-radius: 6px; background: rgba(0,0,0,0.3); color: #fff; font-size: 13px; font-family: 'Inter', sans-serif; }
.admin-add-row input::placeholder { color: rgba(255,255,255,0.3); }
.admin-add-row button { padding: 8px 14px; border: none; border-radius: 6px; font-weight: 600; cursor: pointer; font-size: 12px; white-space: nowrap; font-family: 'Inter', sans-serif; }
.admin-add-row button.add-left { background: #4a90d9; color: #fff; }
.admin-add-row button.add-right { background: #e07845; color: #fff; }

.admin-winner-row { display: flex; gap: 10px; justify-content: center; margin-top: 16px; padding-top: 14px; border-top: 1px solid rgba(255,255,255,0.1); }
.admin-winner-btn { display: flex; align-items: center; gap: 6px; padding: 8px 16px; border: none; border-radius: 8px; font-weight: 700; cursor: pointer; font-size: 13px; font-family: 'Inter', sans-serif; transition: transform 0.15s, box-shadow 0.2s; }
.admin-winner-btn:hover { transform: translateY(-2px); box-shadow: 0 4px 12px rgba(0,0,0,0.3); }
.admin-winner-btn.win-left { background: linear-gradient(135deg, #4a90d9, #6fb3ff); color: #fff; }
.admin-winner-btn.win-right { background: linear-gradient(135deg, #e07845, #ff8a65); color: #fff; }

.map-center { flex: 0 0 auto; width: 140px; display: flex; flex-direction: column; align-items: center; gap: 10px; padding-top: 40px; }
.map-label { font-size: 11px; font-weight: 700; color: rgba(255,215,0,0.7); text-transform: uppercase; letter-spacing: 1px; text-align: center; }
.map-image { width: 120px; height: 120px; border-radius: 10px; object-fit: cover; border: 2px solid rgba(255,215,0,0.3); box-shadow: 0 4px 16px rgba(0,0,0,0.4); }
.map-vs { font-size: 22px; font-weight: 800; color: rgba(255,215,0,0.6); text-align: center; }
.map-name { font-size: 12px; font-weight: 600; color: rgba(255,255,255,0.8); text-align: center; text-transform: uppercase; letter-spacing: 0.5px; }
.map-placeholder { width: 120px; height: 120px; border-radius: 10px; border: 2px dashed rgba(255,255,255,0.2); display: flex; align-items: center; justify-content: center; text-align: center; font-size: 11px; color: rgba(255,255,255,0.4); line-height: 1.4; padding: 10px; }
.map-name.empty { color: rgba(255,255,255,0.3); }

.common-chat-container { width: 100%; margin-top: 20px; border-top: 1px solid rgba(255,255,255,0.1); padding-top: 16px; }
.chat-title { font-size: 14px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.8px; margin-bottom: 12px; color: #fff; text-align: center; }
.chat-messages { max-height: 200px; overflow-y: auto; display: flex; flex-direction: column; gap: 8px; margin-bottom: 16px; padding: 4px 0; }
.chat-messages::-webkit-scrollbar { width: 6px; }
.chat-messages::-webkit-scrollbar-track { background: rgba(255,255,255,0.05); }
.chat-messages::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.2); border-radius: 3px; }
.chat-msg { background: rgba(255,255,255,0.08); border-radius: 10px; padding: 10px 14px; font-size: 13px; line-height: 1.4; word-break: break-word; position: relative; max-width: 85%; align-self: flex-start; box-shadow: 0 1px 3px rgba(0,0,0,0.2); }
.chat-msg.team-west { background: rgba(74,144,217,0.15); border-left: 3px solid #6fb3ff; align-self: flex-start; }
.chat-msg.team-east { background: rgba(224,120,69,0.15); border-right: 3px solid #ff8a65; align-self: flex-end; }
.chat-msg.team-admin { background: rgba(255,215,0,0.15); border-left: 3px solid #ffd700; align-self: center; max-width: 90%; }
.chat-msg-author { font-size: 11px; font-weight: 700; margin-bottom: 4px; display: block; }
.chat-msg-author.west { color: #6fb3ff; }
.chat-msg-author.east { color: #ff8a65; }
.chat-msg-author.admin { color: #ffd700; }
.chat-msg-text { font-weight: 400; color: rgba(255,255,255,0.9); }
.chat-msg-time { font-size: 9px; color: rgba(255,255,255,0.3); margin-top: 4px; }
.chat-msg-delete { position: absolute; top: 6px; right: 6px; background: rgba(255,80,80,0.2); border: none; color: #ff6b6b; font-size: 14px; cursor: pointer; width: 24px; height: 24px; border-radius: 50%; display: none; align-items: center; justify-content: center; line-height: 1; }
.chat-msg:hover .chat-msg-delete { display: flex; }
.chat-msg-delete:hover { background: rgba(255,80,80,0.4); }
.chat-input-row { display: flex; gap: 10px; }
.chat-input { flex: 1; background: rgba(255,255,255,0.08); border: 1px solid rgba(255,255,255,0.1); border-radius: 8px; padding: 12px; color: #fff; font-size: 14px; font-family: 'Inter', sans-serif; outline: none; transition: border-color 0.2s; }
.chat-input:focus { border-color: rgba(255,215,0,0.4); }
.chat-input::placeholder { color: rgba(255,255,255,0.3); }
.chat-send { background: rgba(255,215,0,0.15); border: 1px solid rgba(255,215,0,0.3); border-radius: 8px; padding: 0 20px; color: #ffd700; font-size: 14px; font-weight: 600; cursor: pointer; transition: background 0.2s; white-space: nowrap; }
.chat-send:hover { background: rgba(255,215,0,0.25); }
.chat-guest-block { text-align: center; color: rgba(255,255,255,0.4); font-size: 13px; padding: 12px; font-style: italic; }
.admin-badge { display: inline-block; background: rgba(255,215,0,0.2); color: #ffd700; font-size: 9px; font-weight: 700; padding: 1px 5px; border-radius: 3px; margin-left: 4px; vertical-align: middle; }
.you-badge { display: inline-block; background: rgba(74,158,255,0.3); color: #4a9eff; font-size: 9px; font-weight: 700; padding: 1px 5px; border-radius: 3px; margin-left: 4px; vertical-align: middle; }

@media (max-width: 900px) {
  .bracket-row { flex-direction: column; align-items: center; }
  .bracket-col { max-width: 100%; width: 100%; }
  .tournament-title { font-size: 22px; }
  .match { max-width: 100%; }
  .participants-grid { flex-direction: column; align-items: center; gap: 20px; }
  .map-center { padding-top: 0; }
  .team-modal { width: 100%; padding: 20px; }
  .chat-msg { max-width: 95%; }
}
</style>

<div class="tournament-wrapper">
  <div class="tournament-title">Плей-офф рандом турнира</div>
  <div class="bracket-row">
    <div class="bracket-col">
      <div class="conf-label west">Запад</div>
      <div class="round-label">Четвертьфиналы</div>
      <div class="match" data-match-id="qf_w1"><div class="match-row"><div class="match-team"><span class="team-seed">1</span> Команда A</div><div class="match-score"></div></div><div class="match-divider"></div><div class="match-row"><div class="match-team"><span class="team-seed">4</span> Команда B</div><div class="match-score"></div></div></div>
      <div class="match" data-match-id="qf_w2"><div class="match-row"><div class="match-team"><span class="team-seed">2</span> Команда C</div><div class="match-score"></div></div><div class="match-divider"></div><div class="match-row"><div class="match-team"><span class="team-seed">3</span> Команда D</div><div class="match-score"></div></div></div>
    </div>
    <div class="bracket-col semifinal-col">
      <div class="round-label">Полуфинал</div>
      <div class="match" data-match-id="sf_w"><div class="match-row"><div class="match-team"><span class="team-seed">З1</span> <span class="sf-team-name">Ожидание...</span></div><div class="match-score"></div></div><div class="match-divider"></div><div class="match-row"><div class="match-team"><span class="team-seed">З2</span> <span class="sf-team-name">Ожидание...</span></div><div class="match-score"></div></div></div>
    </div>
    <div class="bracket-col final-col">
      <div class="final-box">
        <div class="final-title">Финал</div>
        <div class="match final-match" data-match-id="final"><div class="match-row"><div class="match-team"><span class="team-seed">З</span> <span class="sf-team-name">Ожидание...</span></div><div class="match-score"></div></div><div class="match-divider"></div><div class="match-row"><div class="match-team"><span class="team-seed">В</span> <span class="sf-team-name">Ожидание...</span></div><div class="match-score"></div></div></div>
      </div>
    </div>
    <div class="bracket-col semifinal-col">
      <div class="round-label">Полуфинал</div>
      <div class="match" data-match-id="sf_e"><div class="match-row"><div class="match-team"><span class="team-seed">В1</span> <span class="sf-team-name">Ожидание...</span></div><div class="match-score"></div></div><div class="match-divider"></div><div class="match-row"><div class="match-team"><span class="team-seed">В2</span> <span class="sf-team-name">Ожидание...</span></div><div class="match-score"></div></div></div>
    </div>
    <div class="bracket-col">
      <div class="conf-label east">Восток</div>
      <div class="round-label">Четвертьфиналы</div>
      <div class="match" data-match-id="qf_e1"><div class="match-row"><div class="match-team"><span class="team-seed">1</span> Команда E</div><div class="match-score"></div></div><div class="match-divider"></div><div class="match-row"><div class="match-team"><span class="team-seed">4</span> Команда F</div><div class="match-score"></div></div></div>
      <div class="match" data-match-id="qf_e2"><div class="match-row"><div class="match-team"><span class="team-seed">2</span> Команда G</div><div class="match-score"></div></div><div class="match-divider"></div><div class="match-row"><div class="match-team"><span class="team-seed">3</span> Команда H</div><div class="match-score"></div></div></div>
    </div>
  </div>
</div>

<div class="join-section" id="joinSection"></div>

<div class="admin-login-row">
  <input type="password" id="adminPassInput" placeholder="Админ-пароль" onkeydown="if(event.key==='Enter') toggleAdmin()">
  <button class="btn-join" style="padding:12px 26px; font-size:14px;" onclick="toggleAdmin()">Войти как админ</button>
</div>

<div class="admin-panel" id="adminPanel" style="display:none;">
  <h3>Админ-панель <span class="admin-active-badge">АКТИВЕН</span></h3>
  <div class="admin-hint">Открой любой матч — появились поля добавления игроков и кнопки подтверждения победы. Чтобы отменить победителя — нажми на картинку под победившей командой.</div>
</div>

<div class="team-modal-overlay" id="teamModalOverlay">
  <div class="team-modal">
    <div class="team-modal-header">
      <span class="team-modal-matchup" id="teamModalMatchup">Матч</span>
      <button class="team-modal-close" id="teamModalClose">&times;</button>
    </div>
    <div class="participants-grid" id="participantsGrid">
      <div class="participants-col left" id="leftCol">
        <div class="participants-col-title" id="leftTeamName">Команда 1</div>
        <ul class="participant-list" id="leftParticipantList"></ul>
      </div>
      <div class="map-center">
        <div class="map-label">Карта</div>
        <div class="map-vs">VS</div>
        <div id="mapContainer">
          <img class="map-image" id="mapImage" src="" alt="Карта" style="display:none;">
          <div class="map-placeholder" id="mapPlaceholder">Карта будет выбрана, когда обе команды укомплектованы</div>
        </div>
        <div class="map-name" id="mapName"></div>
      </div>
      <div class="participants-col right" id="rightCol">
        <div class="participants-col-title" id="rightTeamName">Команда 2</div>
        <ul class="participant-list" id="rightParticipantList"></ul>
      </div>
    </div>
    <div class="common-chat-container">
      <div class="chat-title">Общий чат матча</div>
      <div class="chat-messages" id="commonChatMessages"></div>
      <div id="chatInputArea">
        <div class="chat-input-row">
          <input type="text" class="chat-input" id="commonChatInput" placeholder="Напишите сообщение..." maxlength="200">
          <button class="chat-send" id="commonChatSend">Отправить</button>
        </div>
      </div>
      <div id="chatGuestBlock" class="chat-guest-block" style="display:none;">Писать в чате могут только участники этого матча</div>
    </div>
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
  var MAX_PLAYERS = 5;
  var WIN_LOGO = 'https://4ak4ak.moy.su/logo1.jpg';
  var myNick = null;
  var isAdmin = false;
  var currentMatchId = null;
  var chatRef = null;
  var allMatches = {};
  var qfMatchIds = ['qf_w1','qf_w2','qf_e1','qf_e2'];

  var maps = [
    { url: 'https://4ak4ak.moy.su/dust2.png', name: 'Dust 2' },
    { url: 'https://4ak4ak.moy.su/360fx360f.png', name: 'Nuke' },
    { url: 'https://4ak4ak.moy.su/ancient.jpg', name: 'Ancient' },
    { url: 'https://4ak4ak.moy.su/anubis.png', name: 'Anubis' },
    { url: 'https://4ak4ak.moy.su/cache.png', name: 'Cache' },
    { url: 'https://4ak4ak.moy.su/inferno.png', name: 'Inferno' },
    { url: 'https://4ak4ak.moy.su/mirage.png', name: 'Mirage' },
    { url: 'https://4ak4ak.moy.su/vertigo.png', name: 'Vertigo' }
  ];

  var matchOrder = ['qf_w1','qf_w2','sf_w','final','sf_e','qf_e1','qf_e2'];

  var qfTeams = {
    'qf_w1': { left: 'Команда A', right: 'Команда B' },
    'qf_w2': { left: 'Команда C', right: 'Команда D' },
    'qf_e1': { left: 'Команда E', right: 'Команда F' },
    'qf_e2': { left: 'Команда G', right: 'Команда H' }
  };

  var sfTeamNames = {
    'sf_w': { left: 'Команда I', right: 'Команда J' },
    'sf_e': { left: 'Команда K', right: 'Команда L' }
  };
  var finalTeamNames = { left: 'Команда M', right: 'Команда N' };

  var sfSlots = [
    { sfId: 'sf_w', sfSide: 'left' },
    { sfId: 'sf_w', sfSide: 'right' },
    { sfId: 'sf_e', sfSide: 'left' },
    { sfId: 'sf_e', sfSide: 'right' }
  ];
  var finalSlots = [
    { finalSide: 'left' },
    { finalSide: 'right' }
  ];

  function getUrlParam(n) { var u = new URL(window.location.href); return u.searchParams.get(n); }
  myNick = getUrlParam('user');

  function escapeHtml(t) {
    if (!t) return '';
    return String(t).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#039;");
  }

  function formatTime(ts) {
    var d = new Date(ts); var h = String(d.getHours()).padStart(2,'0'); var m = String(d.getMinutes()).padStart(2,'0');
    return h + ':' + m;
  }

  function isLoggedIn() {
    return myNick && myNick !== 'null' && myNick !== '' && myNick !== 'guest' && myNick !== 'Гость';
  }

  function isUserInAnyMatch(nick) {
    if (!nick) return false;
    for (var mid in allMatches) {
      var m = allMatches[mid];
      if (m && m.left && m.left.indexOf(nick) !== -1) return true;
      if (m && m.right && m.right.indexOf(nick) !== -1) return true;
    }
    return false;
  }

  function isUserInMatch(nick, mid) {
    if (!nick) return false;
    var m = allMatches[mid] || {};
    if (m.left && m.left.indexOf(nick) !== -1) return true;
    if (m.right && m.right.indexOf(nick) !== -1) return true;
    return false;
  }

  function canChat() {
    if (isAdmin) return true;
    if (!isLoggedIn()) return false;
    if (!currentMatchId) return false;
    return isUserInMatch(myNick, currentMatchId);
  }

  function updateChatInputVisibility() {
    var inputArea = document.getElementById('chatInputArea');
    var guestBlock = document.getElementById('chatGuestBlock');
    if (canChat()) {
      inputArea.style.display = '';
      guestBlock.style.display = 'none';
    } else {
      inputArea.style.display = 'none';
      guestBlock.style.display = '';
    }
  }

  function hasQfSpace() {
    for (var i = 0; i < qfMatchIds.length; i++) {
      var mid = qfMatchIds[i];
      var m = allMatches[mid] || {};
      var l = m.left || [], r = m.right || [];
      if (l.length < MAX_PLAYERS || r.length < MAX_PLAYERS) return true;
    }
    return false;
  }

  function updateJoinSection() {
    var s = document.getElementById('joinSection');
    if (!isLoggedIn()) {
      s.innerHTML = '<p class="guest-warning"><span class="guest-warning-text">Войдите на сайт, чтобы участвовать в турнире</span></p>';
      return;
    }
    if (isUserInAnyMatch(myNick)) {
      s.innerHTML = '<p class="joined-msg">Ты уже в турнире! Найди свою команду в сетке.</p>';
      return;
    }
    if (!hasQfSpace()) {
      s.innerHTML = '<p class="tournament-full-msg">Турнирная таблица полностью заполнена!</p>';
      return;
    }
    s.innerHTML = '<button class="btn-join" onclick="joinTournament()">Участвовать</button>';
  }

  window.joinTournament = function() {
    if (!isLoggedIn()) { alert('Войдите на сайт, чтобы участвовать в турнире!'); return; }
    var candidates = [];
    var sides = ['left','right'];
    qfMatchIds.forEach(function(mid) {
      sides.forEach(function(side) {
        var m = allMatches[mid] || {};
        var arr = m[side] || [];
        if (arr.length < MAX_PLAYERS) candidates.push({ matchId: mid, side: side });
      });
    });
    if (candidates.length === 0) { alert('Все команды четвертьфинала заполнены!'); return; }
    var pick = candidates[Math.floor(Math.random() * candidates.length)];
    var arr = (allMatches[pick.matchId] || {})[pick.side] || [];
    arr.push(myNick);
    db.ref('playoff/matches/' + pick.matchId + '/' + pick.side).set(arr).then(function() {
      db.ref('playoff/allParticipants/' + myNick.replace(/[^a-zA-Z0-9]/g,'_')).set(myNick);
      allMatches[pick.matchId] = allMatches[pick.matchId] || {};
      allMatches[pick.matchId][pick.side] = arr;
      updateJoinSection();
      renderBracket();
    });
  };

  window.toggleAdmin = function() {
    var p = document.getElementById('adminPassInput').value;
    if (!isAdmin) {
      if (p === ADMIN_PASSWORD) {
        isAdmin = true;
        document.getElementById('adminPassInput').value = '';
        document.getElementById('adminPanel').style.display = 'block';
        alert('Админ-режим включён!');
        renderBracket();
      } else { alert('Неверный пароль!'); }
    } else {
      isAdmin = false;
      document.getElementById('adminPanel').style.display = 'none';
      alert('Админ-режим выключен.');
      renderBracket();
    }
  };

  function loadAllMatches(cb) {
    db.ref('playoff/matches').once('value').then(function(snap) {
      allMatches = snap.val() || {};
      if (cb) cb();
    });
  }

  function isTeamFull(arr) { return arr && arr.length >= MAX_PLAYERS; }

  function renderBracket() {
    loadAllMatches(function() {
      matchOrder.forEach(function(mid) {
        var el = document.querySelector('[data-match-id="' + mid + '"]');
        if (!el) return;
        var m = allMatches[mid] || {};
        var left = m.left || [], right = m.right || [];
        var winner = m.winner || null;
        var rows = el.querySelectorAll('.match-row');
        var leftNameEl = rows[0].querySelector('.match-team');
        var rightNameEl = rows[1].querySelector('.match-team');
        var leftScoreEl = rows[0].querySelector('.match-score');
        var rightScoreEl = rows[1].querySelector('.match-score');
        if (mid.startsWith('qf_')) {
          var teams = qfTeams[mid];
          leftNameEl.innerHTML = '<span class="team-seed">' + (rows[0].querySelector('.team-seed') ? rows[0].querySelector('.team-seed').textContent : '') + '</span> ' + teams.left;
          rightNameEl.innerHTML = '<span class="team-seed">' + (rows[1].querySelector('.team-seed') ? rows[1].querySelector('.team-seed').textContent : '') + '</span> ' + teams.right;
        } else {
          var sfNameL = leftNameEl.querySelector('.sf-team-name');
          var sfNameR = rightNameEl.querySelector('.sf-team-name');
          if (sfNameL && sfNameR) {
            if (mid === 'sf_w' || mid === 'sf_e') {
              var names = sfTeamNames[mid] || { left: '?', right: '?' };
              sfNameL.textContent = (left.length > 0) ? names.left : 'Ожидание...';
              sfNameR.textContent = (right.length > 0) ? names.right : 'Ожидание...';
            } else if (mid === 'final') {
              sfNameL.textContent = (left.length > 0) ? finalTeamNames.left : 'Ожидание...';
              sfNameR.textContent = (right.length > 0) ? finalTeamNames.right : 'Ожидание...';
            }
          }
        }
        leftScoreEl.textContent = ''; rightScoreEl.textContent = '';
        rows[0].classList.remove('winner'); rows[1].classList.remove('winner');
        rows[0].classList.remove('is-mine-row'); rows[1].classList.remove('is-mine-row');
        if (myNick) { if (left.indexOf(myNick) !== -1) rows[0].classList.add('is-mine-row'); if (right.indexOf(myNick) !== -1) rows[1].classList.add('is-mine-row'); }
        if (winner === 'left') rows[0].classList.add('winner');
        if (winner === 'right') rows[1].classList.add('winner');
        el.classList.remove('is-mine');
        if (myNick && (left.indexOf(myNick) !== -1 || right.indexOf(myNick) !== -1)) el.classList.add('is-mine');
      });
    });
  }

  function syncMap(mid, m) {
    var bothFull = isTeamFull(m.left) && isTeamFull(m.right);
    if (bothFull && !m.map) {
      var idx = Math.floor(Math.random() * maps.length);
      db.ref('playoff/matches/' + mid + '/map').set(maps[idx]);
    }
    if (!bothFull && m.map) { db.ref('playoff/matches/' + mid + '/map').remove(); }
  }

  function openModal(matchEl) {
    var mid = matchEl.getAttribute('data-match-id');
    currentMatchId = mid;
    loadAllMatches(function() {
      var m = allMatches[mid] || {};
      var left = m.left || [], right = m.right || [];
      var teams;
      if (mid.startsWith('qf_')) teams = qfTeams[mid];
      else if (mid === 'sf_w' || mid === 'sf_e') teams = sfTeamNames[mid] || { left: '?', right: '?' };
      else if (mid === 'final') teams = finalTeamNames;
      else teams = { left: 'Команда 1', right: 'Команда 2' };
      document.getElementById('teamModalMatchup').textContent = teams.left + ' vs ' + teams.right;
      document.getElementById('leftTeamName').textContent = teams.left;
      document.getElementById('rightTeamName').textContent = teams.right;
      var leftCol = document.getElementById('leftCol'), rightCol = document.getElementById('rightCol');
      leftCol.classList.remove('is-mine-col'); rightCol.classList.remove('is-mine-col');
      if (myNick && left.indexOf(myNick) !== -1) leftCol.classList.add('is-mine-col');
      if (myNick && right.indexOf(myNick) !== -1) rightCol.classList.add('is-mine-col');
      document.getElementById('leftParticipantList').innerHTML = buildParticipantList(mid, 'left', left);
      document.getElementById('rightParticipantList').innerHTML = buildParticipantList(mid, 'right', right);
      var oldW = document.querySelector('.winner-logo-section'); if (oldW) oldW.remove();
      if (m.winner) {
        var winCol = m.winner === 'left' ? leftCol : rightCol;
        var winSec = document.createElement('div'); winSec.className = 'winner-logo-section';
        if (isAdmin) winSec.classList.add('admin-can-cancel');
        winSec.innerHTML = '<img src="' + WIN_LOGO + '" alt="Победитель"' + (isAdmin ? ' onclick="cancelWinner(\'' + mid + '\')"' : '') + '>';
        winCol.appendChild(winSec);
      }
      if (isAdmin) addAdminControls(mid, teams);
      var bothFull = isTeamFull(left) && isTeamFull(right);
      var mapUrl = (bothFull && m.map) ? m.map.url : null;
      var mapName = (bothFull && m.map) ? m.map.name : null;
      var mapImg = document.getElementById('mapImage'), mapPh = document.getElementById('mapPlaceholder'), mapNameEl = document.getElementById('mapName');
      if (mapUrl) { mapImg.src = mapUrl; mapImg.alt = mapName; mapImg.style.display = 'block'; mapPh.style.display = 'none'; mapNameEl.textContent = mapName; mapNameEl.classList.remove('empty'); }
      else { mapImg.style.display = 'none'; mapPh.style.display = 'flex'; mapNameEl.textContent = bothFull ? 'Выбирается...' : 'Не выбрана'; mapNameEl.classList.add('empty'); }
      updateChatInputVisibility();
      if (chatRef) chatRef.off();
      chatRef = db.ref('playoff/chats/' + mid);
      chatRef.on('value', renderChat);
      document.getElementById('teamModalOverlay').classList.add('active');
    });
  }

  function buildParticipantList(mid, side, arr) {
    var html = '';
    for (var i = 0; i < MAX_PLAYERS; i++) {
      var nick = arr[i] || null; var num = i + 1;
      var isMe = myNick && nick && nick === myNick;
      var delBtn = isAdmin && nick ? '<button class="participant-del" onclick="removeParticipant(\'' + mid + '\',\'' + side + '\',' + i + ')">&times;</button>' : '';
      var avatarBg = side === 'left' ? 'linear-gradient(135deg, #4a90d9, #6fb3ff)' : 'linear-gradient(135deg, #e07845, #ff8a65)';
      var avatarTxt = nick ? escapeHtml(nick.charAt(0).toUpperCase()) : num;
      var meBadge = isMe ? '<span class="you-badge">ТЫ</span>' : '';
      html += '<li class="participant-item' + (isMe ? ' is-me' : '') + '"><div class="participant-avatar" style="' + (nick ? '' : 'opacity:0.3;') + 'background:' + avatarBg + '">' + avatarTxt + '</div><span class="participant-num">#' + num + '</span> ' + (nick ? escapeHtml(nick) + meBadge : '<span style="color:rgba(255,255,255,0.25)">Свободно</span>') + delBtn + '</li>';
    }
    return html;
  }

  function addAdminControls(mid, teams) {
    var leftCol = document.getElementById('leftCol'), rightCol = document.getElementById('rightCol');
    var oldL = leftCol.querySelector('.admin-add-row'); if (oldL) oldL.remove();
    var oldR = rightCol.querySelector('.admin-add-row'); if (oldR) oldR.remove();
    var leftRow = document.createElement('div'); leftRow.className = 'admin-add-row';
    leftRow.innerHTML = '<input type="text" placeholder="Добавить игрока" id="addInput_left_' + mid + '" maxlength="20"><button class="add-left" onclick="addPlayer(\'' + mid + '\',\'left\')">+</button>';
    var rightRow = document.createElement('div'); rightRow.className = 'admin-add-row';
    rightRow.innerHTML = '<input type="text" placeholder="Добавить игрока" id="addInput_right_' + mid + '" maxlength="20"><button class="add-right" onclick="addPlayer(\'' + mid + '\',\'right\')">+</button>';
    var lwl = leftCol.querySelector('.winner-logo-section'); if (lwl) leftCol.insertBefore(leftRow, lwl); else leftCol.appendChild(leftRow);
    var rwl = rightCol.querySelector('.winner-logo-section'); if (rwl) rightCol.insertBefore(rightRow, rwl); else rightCol.appendChild(rightRow);
    var oldW2 = document.querySelector('.admin-winner-row'); if (oldW2) oldW2.remove();
    var winRow = document.createElement('div'); winRow.className = 'admin-winner-row';
    var m = allMatches[mid] || {}; var ld = m.winner ? 'disabled' : '', rd = m.winner ? 'disabled' : '';
    winRow.innerHTML = '<button class="admin-winner-btn win-left" ' + ld + ' onclick="confirmWinner(\'' + mid + '\',\'left\')">Победа: ' + escapeHtml(teams.left) + '</button><button class="admin-winner-btn win-right" ' + rd + ' onclick="confirmWinner(\'' + mid + '\',\'right\')">Победа: ' + escapeHtml(teams.right) + '</button>';
    document.querySelector('.participants-grid').after(winRow);
  }

  window.addPlayer = function(mid, side) {
    var input = document.getElementById('addInput_' + side + '_' + mid);
    var nick = input.value.trim(); if (!nick) return;
    var arr = (allMatches[mid] || {})[side] || [];
    if (arr.length >= MAX_PLAYERS) { alert('Команда заполнена!'); return; }
    arr.push(nick);
    db.ref('playoff/matches/' + mid + '/' + side).set(arr).then(function() {
      allMatches[mid] = allMatches[mid] || {}; allMatches[mid][side] = arr;
      input.value = ''; syncMap(mid, allMatches[mid]);
      openModal(document.querySelector('[data-match-id="' + mid + '"]')); renderBracket(); updateJoinSection();
    });
  };

  window.removeParticipant = function(mid, side, idx) {
    var arr = (allMatches[mid] || {})[side] || []; arr.splice(idx, 1);
    db.ref('playoff/matches/' + mid + '/' + side).set(arr).then(function() {
      allMatches[mid] = allMatches[mid] || {}; allMatches[mid][side] = arr;
      syncMap(mid, allMatches[mid]);
      openModal(document.querySelector('[data-match-id="' + mid + '"]')); renderBracket(); updateJoinSection();
    });
  };

  window.confirmWinner = function(mid, side) {
    var m = allMatches[mid] || {};
    if (m.winner) { alert('Победитель уже выбран!'); return; }
    var winArr = m[side] || [];
    var updates = {};
    updates['playoff/matches/' + mid + '/winner'] = side;

    if (mid.startsWith('qf_')) {
      var distribution = {};
      winArr.forEach(function(p) {
        var available = sfSlots.filter(function(s) { var a = (allMatches[s.sfId] || {})[s.sfSide] || []; return a.length < MAX_PLAYERS; });
        if (available.length === 0) return;
        var slot = available[Math.floor(Math.random() * available.length)];
        var sfArr = (allMatches[slot.sfId] || {})[slot.sfSide] || []; sfArr.push(p);
        updates['playoff/matches/' + slot.sfId + '/' + slot.sfSide] = sfArr;
        allMatches[slot.sfId] = allMatches[slot.sfId] || {}; allMatches[slot.sfId][slot.sfSide] = sfArr;
        distribution[p] = { sfId: slot.sfId, sfSide: slot.sfSide };
      });
      updates['playoff/distribution/' + mid] = distribution;
    }

    if (mid === 'sf_w' || mid === 'sf_e') {
      var finDist = {};
      winArr.forEach(function(p) {
        var available = finalSlots.filter(function(s) { var a = (allMatches['final'] || {})[s.finalSide] || []; return a.length < MAX_PLAYERS; });
        if (available.length === 0) return;
        var slot = available[Math.floor(Math.random() * available.length)];
        var finArr = (allMatches['final'] || {})[slot.finalSide] || []; finArr.push(p);
        updates['playoff/matches/final/' + slot.finalSide] = finArr;
        allMatches['final'] = allMatches['final'] || {}; allMatches['final'][slot.finalSide] = finArr;
        finDist[p] = { finalSide: slot.finalSide };
      });
      updates['playoff/distribution/' + mid] = finDist;
    }

    db.ref().update(updates).then(function() {
      if (mid === 'final') {
        var loseSide = side === 'left' ? 'right' : 'left';
        var winners = (allMatches['final'] || {})[side] || [];
        var runnersUp = (allMatches['final'] || {})[loseSide] || [];
        db.ref('playoff/finalResult').set({ winners: winners, runnersUp: runnersUp, time: Date.now() });
      }
      loadAllMatches(function() {
        openModal(document.querySelector('[data-match-id="' + mid + '"]')); renderBracket(); updateJoinSection();
      });
    });
  };

  window.cancelWinner = function(mid) {
    if (!isAdmin) return;
    var m = allMatches[mid] || {}; if (!m.winner) return;
    if (!confirm('Отменить победителя этого матча? Игроки будут убраны из следующего раунда.')) return;
    var updates = {};
    updates['playoff/matches/' + mid + '/winner'] = null;

    if (mid === 'final') { db.ref('playoff/finalResult').remove(); }

    if (mid.startsWith('qf_')) {
      db.ref('playoff/distribution/' + mid).once('value').then(function(snap) {
        var dist = snap.val() || {};
        var sfToRemove = {};
        Object.keys(dist).forEach(function(player) { var d = dist[player]; var key = d.sfId + '/' + d.sfSide; if (!sfToRemove[key]) sfToRemove[key] = []; sfToRemove[key].push(player); });
        Object.keys(sfToRemove).forEach(function(key) {
          var parts = key.split('/'); var sfId = parts[0], sfSide = parts[1];
          var arr = (allMatches[sfId] || {})[sfSide] || [];
          sfToRemove[key].forEach(function(p) { var idx = arr.indexOf(p); if (idx !== -1) arr.splice(idx, 1); });
          updates['playoff/matches/' + key] = arr;
          allMatches[sfId] = allMatches[sfId] || {}; allMatches[sfId][sfSide] = arr;
        });
        updates['playoff/distribution/' + mid] = null;
        db.ref().update(updates).then(function() {
          db.ref('playoff/scores/' + mid).remove();
          loadAllMatches(function() { openModal(document.querySelector('[data-match-id="' + mid + '"]')); renderBracket(); updateJoinSection(); });
        });
      });
      return;
    }

    if (mid === 'sf_w' || mid === 'sf_e') {
      db.ref('playoff/distribution/' + mid).once('value').then(function(snap) {
        var dist = snap.val() || {};
        var finToRemove = {};
        Object.keys(dist).forEach(function(player) { var d = dist[player]; var key = d.finalSide; if (!finToRemove[key]) finToRemove[key] = []; finToRemove[key].push(player); });
        Object.keys(finToRemove).forEach(function(finSide) {
          var arr = (allMatches['final'] || {})[finSide] || [];
          finToRemove[finSide].forEach(function(p) { var idx = arr.indexOf(p); if (idx !== -1) arr.splice(idx, 1); });
          updates['playoff/matches/final/' + finSide] = arr;
          allMatches['final'] = allMatches['final'] || {}; allMatches['final'][finSide] = arr;
        });
        updates['playoff/distribution/' + mid] = null;
        db.ref().update(updates).then(function() {
          db.ref('playoff/scores/' + mid).remove();
          loadAllMatches(function() { openModal(document.querySelector('[data-match-id="' + mid + '"]')); renderBracket(); updateJoinSection(); });
        });
      });
      return;
    }

    db.ref().update(updates).then(function() {
      db.ref('playoff/scores/' + mid).remove();
      loadAllMatches(function() { openModal(document.querySelector('[data-match-id="' + mid + '"]')); renderBracket(); updateJoinSection(); });
    });
  };

  function renderChat(snap) {
    var c = document.getElementById('commonChatMessages');
    if (!snap || !snap.exists()) {
      c.innerHTML = '<div style="font-size:12px;color:rgba(255,255,255,0.3);text-align:center;padding:16px;">Здесь пока тихо. Напишите что-нибудь!</div>';
      return;
    }
    var data = snap.val();
    var keys = Object.keys(data).sort(function(a,b) { return (data[a].time||0) - (data[b].time||0); });
    var html = '';
    keys.forEach(function(k) {
      var msg = data[k]; var cls = '', colCls = '', badge = '';
      if (msg.isAdmin) { cls = 'team-admin'; colCls = 'admin'; badge = '<span class="admin-badge">ADMIN</span>'; }
      else if (msg.side === 'left') { cls = 'team-west'; colCls = 'west'; }
      else { cls = 'team-east'; colCls = 'east'; }
      var delBtn = isAdmin ? '<button class="chat-msg-delete" data-k="' + escapeHtml(k) + '">&times;</button>' : '';
      html += '<div class="chat-msg ' + cls + '">' + delBtn + '<div class="chat-msg-author ' + colCls + '">' + escapeHtml(msg.author) + badge + '</div><div class="chat-msg-text">' + escapeHtml(msg.text) + '</div><div class="chat-msg-time">' + formatTime(msg.time) + '</div></div>';
    });
    c.innerHTML = html; c.scrollTop = c.scrollHeight;
    if (isAdmin) {
      c.querySelectorAll('.chat-msg-delete').forEach(function(b) {
        b.addEventListener('click', function(e) { e.stopPropagation(); db.ref('playoff/chats/' + currentMatchId + '/' + this.getAttribute('data-k')).remove(); });
      });
    }
  }

  function sendMsg() {
    if (!canChat()) { alert('Писать в чате могут только участники этого матча!'); return; }
    var input = document.getElementById('commonChatInput'); var text = input.value.trim(); if (!text) return;
    var side = 'left'; var m = allMatches[currentMatchId] || {};
    if (myNick && m.right && m.right.indexOf(myNick) !== -1) side = 'right';
    db.ref('playoff/chats/' + currentMatchId).push({ author: myNick || 'Гость', text: text, time: Date.now(), isAdmin: isAdmin, side: side });
    input.value = '';
  }

  function closeModal() {
    document.getElementById('teamModalOverlay').classList.remove('active'); currentMatchId = null;
    if (chatRef) { chatRef.off(); chatRef = null; }
    var oldW = document.querySelector('.admin-winner-row'); if (oldW) oldW.remove();
  }

  document.getElementById('teamModalClose').addEventListener('click', closeModal);
  document.getElementById('teamModalOverlay').addEventListener('click', function(e) { if (e.target === this) closeModal(); });
  document.addEventListener('keydown', function(e) { if (e.key === 'Escape') closeModal(); });
  document.getElementById('commonChatSend').addEventListener('click', function(e) { e.stopPropagation(); sendMsg(); });
  document.getElementById('commonChatInput').addEventListener('keydown', function(e) { if (e.key === 'Enter') { e.stopPropagation(); sendMsg(); } });

  document.querySelectorAll('.match').forEach(function(m) { m.addEventListener('click', function(e) { e.preventDefault(); openModal(this); }); });

  db.ref('playoff/matches').on('value', function(snap) {
    allMatches = snap.val() || {};
    matchOrder.forEach(function(mid) { var m = allMatches[mid] || {}; syncMap(mid, m); });
    renderBracket(); updateJoinSection();
  });

  updateJoinSection();
})();
</script>

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

.standings-wrapper { max-width: 600px; margin: 32px auto; padding: 20px; background: rgba(10,42,107,0.3); backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px); border: 1px solid rgba(74,158,255,0.35); border-radius: 14px; box-shadow: 0 4px 20px rgba(10,42,107,0.3); }
.standings-title { color: #4a9eff; font-size: 20px; font-weight: 700; margin-bottom: 16px; text-transform: uppercase; letter-spacing: 1px; text-align: center; }
.standings-table { width: 100%; border-collapse: collapse; color: #fff; }
.standings-table th, .standings-table td { padding: 10px 14px; border-bottom: 1px solid rgba(255,255,255,0.1); text-align: left; vertical-align: middle; }
.standings-table th { font-weight: 700; color: rgba(255,255,255,0.9); text-transform: uppercase; font-size: 12px; letter-spacing: 0.5px; }
.standings-table tr:last-child td { border-bottom: none; }
.standings-table .pos-cell { width: 40px; text-align: center; font-weight: 700; color: rgba(255,255,255,0.5); }
.standings-table .pos-cell.first { color: #ffd700; font-size: 16px; }
.standings-table .name-cell { font-weight: 600; }
.standings-table .points-cell { width: 70px; text-align: right; font-weight: 700; color: #ffd700; font-size: 16px; }
.standings-table .champion-badge { display: inline-block; background: linear-gradient(135deg, #ffd700, #ffb300); color: #1a1a2e; font-size: 9px; font-weight: 800; padding: 2px 6px; border-radius: 4px; margin-left: 6px; text-transform: uppercase; }
.standings-empty { text-align: center; color: rgba(255,255,255,0.3); font-size: 14px; padding: 24px; font-style: italic; }

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
.btn-reset { margin-top: 14px; padding: 10px 24px; font-size: 14px; font-weight: 700; color: #fff; background: linear-gradient(135deg, #c0392b, #e74c3c); border: 2px solid rgba(255,255,255,0.2); border-radius: 8px; cursor: pointer; font-family: 'Inter', sans-serif; transition: transform 0.2s, box-shadow 0.2s; }
.btn-reset:hover { transform: translateY(-2px); box-shadow: 0 6px 18px rgba(192,57,43,0.4); }

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

<div class="standings-wrapper">
  <div class="standings-title">Турнирная таблица</div>
  <table class="standings-table">
    <thead>
      <tr><th class="pos-cell">#</th><th>Игрок</th><th class="points-cell">Очки</th></tr>
    </thead>
    <tbody id="standingsBody">
      <tr><td colspan="3" class="standings-empty">Итоги появятся после финала</td></tr>
    </tbody>
  </table>
</div>

<div class="join-section" id="joinSection"></div>

<div class="admin-login-row">
  <input type="password" id="adminPassInput" placeholder="Админ-пароль" onkeydown="if(event.key==='Enter') toggleAdmin()">
  <button class="btn-join" style="padding:12px 26px; font-size:14px;" onclick="toggleAdmin()">Войти как админ</button>
</div>

<div class="admin-panel" id="adminPanel" style="display:none;">
  <h3>Админ-панель <span class="admin-active-badge">АКТИВЕН</span></h3>
  <div class="admin-hint">Открой любой матч — появились поля добавления игроков и кнопки подтверждения победы. Чтобы отменить победителя — нажми на картинку под победившей командой.</div>
  <button class="btn-reset" onclick="resetTournament()">Сбросить весь турнир</button>
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

<script>
(function() {
  var ADMIN_PASSWORD = '12$sacreD';
  var MAX_PLAYERS = 5;
  var WIN_LOGO = 'https://4ak4ak.moy.su/logo1.jpg';
  var STORAGE_KEY = 'playoff_data_v1';
  var myNick = null;
  var isAdmin = false;
  var currentMatchId = null;
  var allMatches = {};
  var finalResult = null;
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
  var sfTeamNames = { 'sf_w': { left: 'Команда I', right: 'Команда J' }, 'sf_e': { left: 'Команда K', right: 'Команда L' } };
  var finalTeamNames = { left: 'Команда M', right: 'Команда N' };

  var sfSlots = [{ sfId:'sf_w', sfSide:'left' },{ sfId:'sf_w', sfSide:'right' },{ sfId:'sf_e', sfSide:'left' },{ sfId:'sf_e', sfSide:'right' }];
  var finalSlots = [{ finalSide:'left' },{ finalSide:'right' }];

  function getUrlParam(n) { try { var u = new URL(window.location.href); return u.searchParams.get(n); } catch(e) { return null; } }
  myNick = getUrlParam('user');

  function escapeHtml(t) { if (!t) return ''; return String(t).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#039;"); }
  function formatTime(ts) { var d = new Date(ts); var h = String(d.getHours()).padStart(2,'0'); var m = String(d.getMinutes()).padStart(2,'0'); return h+':'+m; }

  function isLoggedIn() { return myNick && myNick !== 'null' && myNick !== '' && myNick !== 'guest' && myNick !== 'Гость'; }

  function saveData() {
    var data = { matches: allMatches, finalResult: finalResult };
    try { localStorage.setItem(STORAGE_KEY, JSON.stringify(data)); } catch(e) {}
  }
  function loadData() {
    try {
      var raw = localStorage.getItem(STORAGE_KEY);
      if (raw) { var d = JSON.parse(raw); allMatches = d.matches || {}; finalResult = d.finalResult || null; }
    } catch(e) { allMatches = {}; finalResult = null; }
  }

  function isUserInAnyMatch(nick) {
    if (!nick) return false;
    for (var mid in allMatches) { var m = allMatches[mid]; if (m && m.left && m.left.indexOf(nick) !== -1) return true; if (m && m.right && m.right.indexOf(nick) !== -1) return true; }
    return false;
  }
  function isUserInMatch(nick, mid) {
    if (!nick) return false;
    var m = allMatches[mid] || {};
    if (m.left && m.left.indexOf(nick) !== -1) return true;
    if (m.right && m.right.indexOf(nick) !== -1) return true;
    return false;
  }
  function canChat() { if (isAdmin) return true; if (!isLoggedIn()) return false; if (!currentMatchId) return false; return isUserInMatch(myNick, currentMatchId); }
  function updateChatInputVisibility() {
    var ia = document.getElementById('chatInputArea'); var gb = document.getElementById('chatGuestBlock');
    if (canChat()) { ia.style.display = ''; gb.style.display = 'none'; } else { ia.style.display = 'none'; gb.style.display = ''; }
  }

  function hasQfSpace() {
    for (var i = 0; i < qfMatchIds.length; i++) { var mid = qfMatchIds[i]; var m = allMatches[mid] || {}; var l = m.left||[], r = m.right||[]; if (l.length < MAX_PLAYERS || r.length < MAX_PLAYERS) return true; }
    return false;
  }
  function updateJoinSection() {
    var s = document.getElementById('joinSection');
    if (!isLoggedIn()) { s.innerHTML = '<p class="guest-warning"><span class="guest-warning-text">Войдите на сайт, чтобы участвовать в турнире</span></p>'; return; }
    if (isUserInAnyMatch(myNick)) { s.innerHTML = '<p class="joined-msg">Ты уже в турнире! Найди свою команду в сетке.</p>'; return; }
    if (!hasQfSpace()) { s.innerHTML = '<p class="tournament-full-msg">Турнирная таблица полностью заполнена!</p>'; return; }
    s.innerHTML = '<button class="btn-join" onclick="joinTournament()">Участвовать</button>';
  }

  window.joinTournament = function() {
    if (!isLoggedIn()) { alert('Войдите на сайт!'); return; }
    var c = []; var sides = ['left','right'];
    qfMatchIds.forEach(function(mid) { sides.forEach(function(side) { var m = allMatches[mid]||{}; var arr = m[side]||[]; if (arr.length < MAX_PLAYERS) c.push({matchId:mid,side:side}); }); });
    if (c.length === 0) { alert('Все команды заполнены!'); return; }
    var pick = c[Math.floor(Math.random()*c.length)];
    var arr = (allMatches[pick.matchId]||{})[pick.side] || [];
    arr.push(myNick);
    allMatches[pick.matchId] = allMatches[pick.matchId] || {};
    allMatches[pick.matchId][pick.side] = arr;
    syncMap(pick.matchId, allMatches[pick.matchId]);
    saveData(); updateJoinSection(); renderBracket();
  };

  window.toggleAdmin = function() {
    var p = document.getElementById('adminPassInput').value;
    if (!isAdmin) {
      if (p === ADMIN_PASSWORD) { isAdmin = true; document.getElementById('adminPassInput').value=''; document.getElementById('adminPanel').style.display='block'; alert('Админ-режим включён!'); renderBracket(); }
      else { alert('Неверный пароль!'); }
    } else { isAdmin = false; document.getElementById('adminPanel').style.display='none'; alert('Админ-режим выключен.'); renderBracket(); }
  };

  window.resetTournament = function() {
    if (!confirm('Сбросить весь турнир? Все данные будут удалены!')) return;
    allMatches = {}; finalResult = null;
    try { localStorage.removeItem(STORAGE_KEY); } catch(e) {}
    updateStandings(); updateJoinSection(); renderBracket();
    alert('Турнир сброшен!');
  };

  function isTeamFull(arr) { return arr && arr.length >= MAX_PLAYERS; }

  function updateStandings() {
    var body = document.getElementById('standingsBody');
    if (!finalResult) { body.innerHTML = '<tr><td colspan="3" class="standings-empty">Итоги появятся после финала</td></tr>'; return; }
    var scores = {};
    finalResult.winners.forEach(function(n) { scores[n] = (scores[n]||0) + 2; });
    finalResult.runnersUp.forEach(function(n) { scores[n] = (scores[n]||0) + 1; });
    var arr = Object.keys(scores).map(function(n) { return { nick:n, points:scores[n] }; }).sort(function(a,b) { return b.points - a.points; });
    var html = '';
    arr.forEach(function(row, i) {
      var pc = i===0 ? ' pos-cell first' : '';
      var cb = i===0 ? ' <span class="champion-badge">ЧЕМПИОН</span>' : '';
      html += '<tr><td class="pos-cell'+pc+'">'+(i+1)+'</td><td class="name-cell">'+escapeHtml(row.nick)+cb+'</td><td class="points-cell">'+row.points+'</td></tr>';
    });
    body.innerHTML = html;
  }

  function renderBracket() {
    matchOrder.forEach(function(mid) {
      var el = document.querySelector('[data-match-id="'+mid+'"]'); if (!el) return;
      var m = allMatches[mid] || {};
      var left = m.left||[], right = m.right||[], winner = m.winner||null;
      var rows = el.querySelectorAll('.match-row');
      var lne = rows[0].querySelector('.match-team'), rne = rows[1].querySelector('.match-team');
      var lse = rows[0].querySelector('.match-score'), rse = rows[1].querySelector('.match-score');
      if (mid.startsWith('qf_')) {
        var t = qfTeams[mid];
        lne.innerHTML = '<span class="team-seed">'+(rows[0].querySelector('.team-seed')?rows[0].querySelector('.team-seed').textContent:'')+'</span> '+t.left;
        rne.innerHTML = '<span class="team-seed">'+(rows[1].querySelector('.team-seed')?rows[1].querySelector('.team-seed').textContent:'')+'</span> '+t.right;
      } else {
        var sl = lne.querySelector('.sf-team-name'), sr = rne.querySelector('.sf-team-name');
        if (sl && sr) {
          if (mid==='sf_w'||mid==='sf_e') { var n = sfTeamNames[mid]||{left:'?',right:'?'}; sl.textContent = left.length>0?n.left:'Ожидание...'; sr.textContent = right.length>0?n.right:'Ожидание...'; }
          else if (mid==='final') { sl.textContent = left.length>0?finalTeamNames.left:'Ожидание...'; sr.textContent = right.length>0?finalTeamNames.right:'Ожидание...'; }
        }
      }
      lse.textContent=''; rse.textContent='';
      rows[0].classList.remove('winner'); rows[1].classList.remove('winner');
      rows[0].classList.remove('is-mine-row'); rows[1].classList.remove('is-mine-row');
      if (myNick) { if (left.indexOf(myNick)!==-1) rows[0].classList.add('is-mine-row'); if (right.indexOf(myNick)!==-1) rows[1].classList.add('is-mine-row'); }
      if (winner==='left') rows[0].classList.add('winner');
      if (winner==='right') rows[1].classList.add('winner');
      el.classList.remove('is-mine');
      if (myNick && (left.indexOf(myNick)!==-1 || right.indexOf(myNick)!==-1)) el.classList.add('is-mine');
    });
  }

  function syncMap(mid, m) {
    var bothFull = isTeamFull(m.left) && isTeamFull(m.right);
    if (bothFull && !m.map) { m.map = maps[Math.floor(Math.random()*maps.length)]; }
    if (!bothFull && m.map) { delete m.map; }
  }

  function openModal(matchEl) {
    var mid = matchEl.getAttribute('data-match-id'); currentMatchId = mid;
    var m = allMatches[mid] || {};
    var left = m.left||[], right = m.right||[];
    var teams;
    if (mid.startsWith('qf_')) teams = qfTeams[mid];
    else if (mid==='sf_w'||mid==='sf_e') teams = sfTeamNames[mid]||{left:'?',right:'?'};
    else if (mid==='final') teams = finalTeamNames;
    else teams = {left:'Команда 1',right:'Команда 2'};
    document.getElementById('teamModalMatchup').textContent = teams.left+' vs '+teams.right;
    document.getElementById('leftTeamName').textContent = teams.left;
    document.getElementById('rightTeamName').textContent = teams.right;
    var lc = document.getElementById('leftCol'), rc = document.getElementById('rightCol');
    lc.classList.remove('is-mine-col'); rc.classList.remove('is-mine-col');
    if (myNick && left.indexOf(myNick)!==-1) lc.classList.add('is-mine-col');
    if (myNick && right.indexOf(myNick)!==-1) rc.classList.add('is-mine-col');
    document.getElementById('leftParticipantList').innerHTML = buildParticipantList(mid,'left',left);
    document.getElementById('rightParticipantList').innerHTML = buildParticipantList(mid,'right',right);
    var ow = document.querySelector('.winner-logo-section'); if (ow) ow.remove();
    if (m.winner) {
      var wc = m.winner==='left'?lc:rc;
      var ws = document.createElement('div'); ws.className='winner-logo-section';
      if (isAdmin) ws.classList.add('admin-can-cancel');
      ws.innerHTML = '<img src="'+WIN_LOGO+'" alt="Победитель"'+(isAdmin?' onclick="cancelWinner(\''+mid+'\')"':'')+'>';
      wc.appendChild(ws);
    }
    if (isAdmin) addAdminControls(mid, teams);
    var bothFull = isTeamFull(left) && isTeamFull(right);
    var mapUrl = (bothFull && m.map) ? m.map.url : null;
    var mapName = (bothFull && m.map) ? m.map.name : null;
    var mi = document.getElementById('mapImage'), mp = document.getElementById('mapPlaceholder'), mn = document.getElementById('mapName');
    if (mapUrl) { mi.src=mapUrl; mi.alt=mapName; mi.style.display='block'; mp.style.display='none'; mn.textContent=mapName; mn.classList.remove('empty'); }
    else { mi.style.display='none'; mp.style.display='flex'; mn.textContent = bothFull?'Выбирается...':'Не выбрана'; mn.classList.add('empty'); }
    renderChatLocal(mid);
    updateChatInputVisibility();
    document.getElementById('teamModalOverlay').classList.add('active');
  }

  function buildParticipantList(mid, side, arr) {
    var html = '';
    for (var i = 0; i < MAX_PLAYERS; i++) {
      var nick = arr[i]||null; var num = i+1;
      var isMe = myNick && nick && nick===myNick;
      var del = isAdmin && nick ? '<button class="participant-del" onclick="removeParticipant(\''+mid+'\',\''+side+'\','+i+')">&times;</button>' : '';
      var bg = side==='left'?'linear-gradient(135deg,#4a90d9,#6fb3ff)':'linear-gradient(135deg,#e07845,#ff8a65)';
      var av = nick ? escapeHtml(nick.charAt(0).toUpperCase()) : num;
      var mb = isMe ? '<span class="you-badge">ТЫ</span>' : '';
      html += '<li class="participant-item'+(isMe?' is-me':'')+'"><div class="participant-avatar" style="'+(nick?'':'opacity:0.3;')+'background:'+bg+'">'+av+'</div><span class="participant-num">#'+num+'</span> '+(nick?escapeHtml(nick)+mb:'<span style="color:rgba(255,255,255,0.25)">Свободно</span>')+del+'</li>';
    }
    return html;
  }

  function addAdminControls(mid, teams) {
    var lc = document.getElementById('leftCol'), rc = document.getElementById('rightCol');
    var ol = lc.querySelector('.admin-add-row'); if (ol) ol.remove();
    var or = rc.querySelector('.admin-add-row'); if (or) or.remove();
    var lr = document.createElement('div'); lr.className='admin-add-row';
    lr.innerHTML = '<input type="text" placeholder="Добавить игрока" id="addInput_left_'+mid+'" maxlength="20"><button class="add-left" onclick="addPlayer(\''+mid+'\',\'left\')">+</button>';
    var rr = document.createElement('div'); rr.className='admin-add-row';
    rr.innerHTML = '<input type="text" placeholder="Добавить игрока" id="addInput_right_'+mid+'" maxlength="20"><button class="add-right" onclick="addPlayer(\''+mid+'\',\'right\')">+</button>';
    var lw = lc.querySelector('.winner-logo-section'); if (lw) lc.insertBefore(lr,lw); else lc.appendChild(lr);
    var rw = rc.querySelector('.winner-logo-section'); if (rw) rc.insertBefore(rr,rw); else rc.appendChild(rr);
    var ow = document.querySelector('.admin-winner-row'); if (ow) ow.remove();
    var wr = document.createElement('div'); wr.className='admin-winner-row';
    var m = allMatches[mid]||{};
    var ld = m.winner?'disabled':'', rd = m.winner?'disabled':'';
    wr.innerHTML = '<button class="admin-winner-btn win-left" '+ld+' onclick="confirmWinner(\''+mid+'\',\'left\')">Победа: '+escapeHtml(teams.left)+'</button><button class="admin-winner-btn win-right" '+rd+' onclick="confirmWinner(\''+mid+'\',\'right\')">Победа: '+escapeHtml(teams.right)+'</button>';
    document.querySelector('.participants-grid').after(wr);
  }

  window.addPlayer = function(mid, side) {
    var inp = document.getElementById('addInput_'+side+'_'+mid); var nick = inp.value.trim(); if (!nick) return;
    var arr = (allMatches[mid]||{})[side]||[]; if (arr.length >= MAX_PLAYERS) { alert('Команда заполнена!'); return; }
    arr.push(nick); allMatches[mid] = allMatches[mid]||{}; allMatches[mid][side] = arr;
    syncMap(mid, allMatches[mid]); saveData();
    inp.value=''; openModal(document.querySelector('[data-match-id="'+mid+'"]')); renderBracket(); updateJoinSection();
  };

  window.removeParticipant = function(mid, side, idx) {
    var arr = (allMatches[mid]||{})[side]||[]; arr.splice(idx,1);
    allMatches[mid] = allMatches[mid]||{}; allMatches[mid][side] = arr;
    syncMap(mid, allMatches[mid]); saveData();
    openModal(document.querySelector('[data-match-id="'+mid+'"]')); renderBracket(); updateJoinSection();
  };

  window.confirmWinner = function(mid, side) {
    var m = allMatches[mid]||{}; if (m.winner) { alert('Победитель уже выбран!'); return; }
    var winArr = m[side]||[];
    allMatches[mid].winner = side;
    if (mid.startsWith('qf_')) {
      winArr.forEach(function(p) {
        var avail = sfSlots.filter(function(s) { var a = (allMatches[s.sfId]||{})[s.sfSide]||[]; return a.length < MAX_PLAYERS; });
        if (avail.length===0) return;
        var slot = avail[Math.floor(Math.random()*avail.length)];
        var sfArr = (allMatches[slot.sfId]||{})[slot.sfSide]||[];
        sfArr.push(p); allMatches[slot.sfId] = allMatches[slot.sfId]||{}; allMatches[slot.sfId][slot.sfSide] = sfArr;
      });
    }
    if (mid==='sf_w'||mid==='sf_e') {
      winArr.forEach(function(p) {
        var avail = finalSlots.filter(function(s) { var a = (allMatches['final']||{})[s.finalSide]||[]; return a.length < MAX_PLAYERS; });
        if (avail.length===0) return;
        var slot = avail[Math.floor(Math.random()*avail.length)];
        var finArr = (allMatches['final']||{})[slot.finalSide]||[];
        finArr.push(p); allMatches['final'] = allMatches['final']||{}; allMatches['final'][slot.finalSide] = finArr;
      });
    }
    if (mid==='final') {
      var loseSide = side==='left'?'right':'left';
      finalResult = { winners: allMatches['final'][side]||[], runnersUp: allMatches['final'][loseSide]||[], time: Date.now() };
      updateStandings();
    }
    saveData();
    openModal(document.querySelector('[data-match-id="'+mid+'"]')); renderBracket(); updateJoinSection();
  };

  window.cancelWinner = function(mid) {
    if (!isAdmin) return;
    var m = allMatches[mid]||{}; if (!m.winner) return;
    if (!confirm('Отменить победителя? Игроки будут убраны из следующего раунда.')) return;
    allMatches[mid].winner = null;
    if (mid.startsWith('qf_')) {
      var sfKeys = ['sf_w/left','sf_w/right','sf_e/left','sf_e/right'];
      sfKeys.forEach(function(k) { var parts = k.split('/'); var sfId=parts[0], sfSide=parts[1]; if (allMatches[sfId] && allMatches[sfId][sfSide]) { allMatches[sfId][sfSide] = []; syncMap(sfId, allMatches[sfId]); } });
    }
    if (mid==='sf_w'||mid==='sf_e') {
      if (allMatches['final']) { allMatches['final'].left = []; allMatches['final'].right = []; syncMap('final', allMatches['final']); }
    }
    if (mid==='final') { finalResult = null; updateStandings(); }
    saveData();
    openModal(document.querySelector('[data-match-id="'+mid+'"]')); renderBracket(); updateJoinSection();
  };

  function renderChatLocal(mid) {
    var c = document.getElementById('commonChatMessages');
    var m = allMatches[mid] || {};
    var msgs = m.chat || [];
    if (msgs.length === 0) { c.innerHTML = '<div style="font-size:12px;color:rgba(255,255,255,0.3);text-align:center;padding:16px;">Здесь пока тихо. Напишите что-нибудь!</div>'; return; }
    var html = '';
    msgs.forEach(function(msg, i) {
      var cls='', colCls='', badge='';
      if (msg.isAdmin) { cls='team-admin'; colCls='admin'; badge='<span class="admin-badge">ADMIN</span>'; }
      else if (msg.side==='left') { cls='team-west'; colCls='west'; }
      else { cls='team-east'; colCls='east'; }
      var del = isAdmin ? '<button class="chat-msg-delete" data-i="'+i+'">&times;</button>' : '';
      html += '<div class="chat-msg '+cls+'">'+del+'<div class="chat-msg-author '+colCls+'">'+escapeHtml(msg.author)+badge+'</div><div class="chat-msg-text">'+escapeHtml(msg.text)+'</div><div class="chat-msg-time">'+formatTime(msg.time)+'</div></div>';
    });
    c.innerHTML = html; c.scrollTop = c.scrollHeight;
    if (isAdmin) {
      c.querySelectorAll('.chat-msg-delete').forEach(function(b) {
        b.addEventListener('click', function(e) {
          e.stopPropagation();
          var idx = parseInt(this.getAttribute('data-i'));
          var mm = allMatches[currentMatchId] || {}; if (!mm.chat) return;
          mm.chat.splice(idx, 1); saveData(); renderChatLocal(currentMatchId);
        });
      });
    }
  }

  function sendMsg() {
    if (!canChat()) { alert('Писать в чате могут только участники этого матча!'); return; }
    var inp = document.getElementById('commonChatInput'); var text = inp.value.trim(); if (!text) return;
    var side = 'left';
    var m = allMatches[currentMatchId] || {};
    if (myNick && m.right && m.right.indexOf(myNick) !== -1) side = 'right';
    if (!allMatches[currentMatchId]) allMatches[currentMatchId] = {};
    if (!allMatches[currentMatchId].chat) allMatches[currentMatchId].chat = [];
    allMatches[currentMatchId].chat.push({ author: myNick||'Гость', text: text, time: Date.now(), isAdmin: isAdmin, side: side });
    saveData(); inp.value = ''; renderChatLocal(currentMatchId);
  }

  function closeModal() {
    document.getElementById('teamModalOverlay').classList.remove('active'); currentMatchId = null;
    var ow = document.querySelector('.admin-winner-row'); if (ow) ow.remove();
  }

  document.getElementById('teamModalClose').addEventListener('click', closeModal);
  document.getElementById('teamModalOverlay').addEventListener('click', function(e) { if (e.target === this) closeModal(); });
  document.addEventListener('keydown', function(e) { if (e.key === 'Escape') closeModal(); });
  document.getElementById('commonChatSend').addEventListener('click', function(e) { e.stopPropagation(); sendMsg(); });
  document.getElementById('commonChatInput').addEventListener('keydown', function(e) { if (e.key === 'Enter') { e.stopPropagation(); sendMsg(); } });

  document.querySelectorAll('.match').forEach(function(m) { m.addEventListener('click', function(e) { e.preventDefault(); openModal(this); }); });

  loadData();
  updateStandings();
  renderBracket();
  updateJoinSection();
})();
</script>

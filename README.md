<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GLOBALTACOS - リアルタイム為替＆50カ国版</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    html, body { width: 100%; height: 100%; margin: 0; padding: 0; background-color: #0f172a; color: #f8fafc; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
    body { display: flex; flex-direction: column; overflow: hidden; }
    header { background: #1e293b; border-bottom: 1px solid #334155; padding: 10px 16px; display: flex; justify-content: space-between; align-items: center; height: 50px; flex-shrink: 0; }
    .logo { font-size: 1.2rem; font-weight: bold; color: #f59e0b; }
    .controls { display: flex; gap: 8px; align-items: center; }
    select, button { background: #0f172a; color: #fff; border: 1px solid #475569; padding: 4px 8px; border-radius: 4px; font-size: 0.85rem; cursor: pointer; }
    select:hover, button:hover { border-color: #f59e0b; }
    .main-container { display: flex; flex: 1; height: calc(100vh - 50px); width: 100vw; position: relative; }
    #map { flex: 1; height: 100% !important; width: 100% !important; background: #0f172a; }
    .sidebar { width: 350px; background: #1e293b; border-left: 1px solid #334155; padding: 16px; display: flex; flex-direction: column; gap: 12px; overflow-y: auto; flex-shrink: 0; }
    .card { background: #0f172a; border: 1px solid #334155; border-radius: 8px; padding: 12px; }
    .card-title { font-size: 1.1rem; font-weight: bold; margin-bottom: 8px; display: flex; justify-content: space-between; color: #f59e0b; }
    .fx-panel { background: rgba(245, 158, 11, 0.1); border: 1px solid #f59e0b; padding: 10px; border-radius: 8px; }
    .fx-info { font-size: 0.85rem; font-weight: bold; display: flex; justify-content: space-between; align-items: center; }
    .status-badge { font-size: 0.7rem; background: #10b981; color: #fff; padding: 2px 6px; border-radius: 4px; font-weight: normal; }
    .data-row { display: flex; justify-content: space-between; font-size: 0.85rem; color: #cbd5e1; margin: 4px 0; }
    .highlight-val { color: #38bdf8; font-weight: bold; }
    .game-box { background: #1e293b; border: 1px solid #475569; border-radius: 6px; padding: 8px; margin-top: 8px; text-align: center; }
    .taco-count { font-size: 1.2rem; font-weight: bold; color: #10b981; margin: 4px 0; }
    .ranking-list { list-style: none; padding: 0; margin: 0; }
    .ranking-item { display: flex; justify-content: space-between; padding: 6px 4px; font-size: 0.85rem; border-bottom: 1px solid #334155; cursor: pointer; transition: background 0.2s; }


<!--
**GLOBALTACOS/GLOBALTACOS** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->

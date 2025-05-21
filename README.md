# desamio-familia-S1LV4
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Missão da Semana - Game Familiar</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    h1 { text-align: center; }
    table { width: 100%; border-collapse: collapse; margin-bottom: 20px; }
    th, td { border: 1px solid #ccc; padding: 8px; text-align: center; }
    th { background-color: #f4f4f4; }
    input, select { padding: 5px; }
    .controls { margin-bottom: 20px; }
    button { padding: 8px 12px; margin-left: 5px; }
  </style>
</head>
<body>
  <h1>Missão da Semana - Game Familiar</h1>

  <div class="controls">
    <label>Jogador:
      <select id="playerSelect">
        <option value="adolescente">Filho Adolescente</option>
        <option value="menor">Filha Mais Nova</option>
      </select>
    </label>
    <label>Tarefa:
      <select id="taskSelect">
        <option value="Arrumar a cama">Arrumar a cama (10)</option>
        <option value="Lavar a louça">Lavar a louça (15)</option>
        <option value="Organizar material">Organizar material escolar (10)</option>
        <option value="Estudar 1h">Estudar 1 hora (20)</option>
        <option value="Dever de casa">Dever de casa (15)</option>
        <option value="Ajudar familia">Ajudar família (15)</option>
        <option value="Ler 30min">Ler 30 minutos (20)</option>
        <option value="Atividade fisica">Atividade física 30min (20)</option>
      </select>
    </label>
    <button onclick="addEntry()">Adicionar Pontos</button>
  </div>

  <table>
    <thead>
      <tr>
        <th>#</th>
        <th>Jogador</th>
        <th>Tarefa</th>
        <th>Pontos</th>
        <th>Data/Hora</th>
      </tr>
    </thead>
    <tbody id="entries">
      <!-- Linhas serão inseridas dinamicamente -->
    </tbody>
  </table>

  <div>
    <button onclick="showSummary()">Resumo Semanal</button>
    <div id="summary"></div>
  </div>

  <script>
    let entries = [];
    let idCounter = 1;
    const taskPoints = {
      'Arrumar a cama': 10,
      'Lavar a louça': 15,
      'Organizar material': 10,
      'Estudar 1h': 20,
      'Dever de casa': 15,
      'Ajudar familia': 15,
      'Ler 30min': 20,
      'Atividade fisica': 20
    };

    function addEntry() {
      const player = document.getElementById('playerSelect').value;
      const task = document.getElementById('taskSelect').value;
      const points = taskPoints[task];
      const timestamp = new Date().toLocaleString();

      const entry = { id: idCounter++, player, task, points, timestamp };
      entries.push(entry);
      renderEntries();
    }

    function renderEntries() {
      const tbody = document.getElementById('entries');
      tbody.innerHTML = '';
      entries.forEach(e => {
        const row = document.createElement('tr');
        row.innerHTML = `
          <td>${e.id}</td>
          <td>${e.player === 'adolescente' ? 'Filho Adolescente' : 'Filha Mais Nova'}</td>
          <td>${e.task}</td>
          <td>${e.points}</td>
          <td>${e.timestamp}</td>
        `;
        tbody.appendChild(row);
      });
    }

    function showSummary() {
      const summaryDiv = document.getElementById('summary');
      const totals = entries.reduce((acc, e) => {
        acc[e.player] = (acc[e.player] || 0) + e.points;
        return acc;
      }, {});

      const minAdol = 150;
      const minMenor = 100;
      summaryDiv.innerHTML = `
        <p>Pontuação Filho Adolescente: ${totals['adolescente'] || 0} / ${minAdol}</p>
        <p>Pontuação Filha Mais Nova: ${totals['menor'] || 0} / ${minMenor}</p>
      `;
    }
  </script>
</body>
</html>

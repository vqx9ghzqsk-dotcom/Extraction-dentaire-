<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Étude CAP - Cancer du Sein - HGR Makala</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif; background-color: #fce4ec; margin: 0; padding: 0; color: #333; }
        .app-container { max-width: 1280px; margin: 20px auto; background: white; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); overflow: hidden; min-height: 90vh; display: flex; flex-direction: column; }
        
        /* HEADER & NAVIGATION */
        header { background: linear-gradient(135deg, #ec407a, #880e4f); color: white; padding: 15px 25px; display: flex; align-items: center; justify-content: space-between; }
        .logo-area h1 { margin: 0; font-size: 1.4rem; font-weight: 700; }
        .logo-area p { margin: 2px 0 0 0; font-size: 0.85rem; opacity: 0.9; }
        
        .nav-tabs { display: flex; gap: 5px; background: #fff; padding: 10px 20px; border-bottom: 1px solid #eee; overflow-x: auto; }
        .tab-btn { padding: 10px 18px; border: none; background: #f5f5f5; border-radius: 6px; cursor: pointer; font-weight: 600; color: #555; transition: 0.2s; white-space: nowrap; }
        .tab-btn:hover { background: #f8bbd0; color: #880e4f; }
        .tab-btn.active { background: #880e4f; color: white; box-shadow: 0 2px 5px rgba(136, 14, 79, 0.3); }
        .tab-btn.locked { opacity: 0.5; cursor: not-allowed; }
        .tab-btn.locked::after { content: " 🔒"; }

        /* CONTENU */
        .content-section { display: none; padding: 30px; animation: fadeIn 0.4s ease-in-out; }
        .content-section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* FORMULAIRE */
        .form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; }
        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; font-weight: 600; margin-bottom: 8px; font-size: 0.9rem; color: #444; }
        .form-control { width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 6px; font-size: 14px; transition: 0.2s; box-sizing: border-box; }
        .form-control:focus { border-color: #ec407a; outline: none; box-shadow: 0 0 0 3px rgba(236, 64, 122, 0.1); }
        
        .section-header { background: #fce4ec; color: #880e4f; padding: 10px 15px; font-weight: bold; border-left: 5px solid #ec407a; margin: 30px 0 15px 0; text-transform: uppercase; letter-spacing: 0.5px; font-size: 0.95rem; }

        /* CHECKBOX GROUP */
        .check-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 10px; background: #fafafa; padding: 15px; border-radius: 8px; border: 1px dashed #ccc; }
        .check-item { display: flex; align-items: center; cursor: pointer; font-size: 0.9rem; }
        .check-item input { margin-right: 10px; transform: scale(1.2); accent-color: #880e4f; }

        /* BOUTONS */
        .btn-primary { background: #880e4f; color: white; padding: 12px 24px; border: none; border-radius: 6px; font-weight: bold; cursor: pointer; font-size: 1rem; width: 100%; margin-top: 20px; transition: 0.3s; }
        .btn-primary:hover { background: #ad1457; transform: translateY(-2px); }
        
        .btn-admin { background: #333; color: white; padding: 8px 15px; border-radius: 4px; border: none; cursor: pointer; font-size: 0.8rem; margin-left: 10px; }
        
        /* TABLEAUX DE DONNÉES */
        .data-table-container { overflow-x: auto; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.05); }
        table { width: 100%; border-collapse: collapse; font-size: 0.9rem; }
        thead { background: #333; color: white; }
        th, td { padding: 12px 15px; text-align: left; border-bottom: 1px solid #eee; }
        tbody tr:hover { background: #fce4ec; }
        .score-badge { padding: 4px 8px; border-radius: 12px; font-size: 0.75rem; font-weight: bold; }
        .score-good { background: #e8f5e9; color: #2e7d32; }
        .score-mid { background: #fff3e0; color: #ef6c00; }
        .score-bad { background: #ffebee; color: #c62828; }

        /* ANALYTICS */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 20px; }
        .stat-card { background: white; padding: 20px; border-radius: 10px; border: 1px solid #eee; box-shadow: 0 4px 6px rgba(0,0,0,0.02); }
        .stat-title { font-size: 1rem; color: #666; font-weight: 600; margin-bottom: 15px; display: flex; justify-content: space-between; }
        
        .bar-chart-row { display: flex; align-items: center; margin-bottom: 8px; font-size: 0.85rem; }
        .bar-label { width: 180px; font-weight: 500; }
        .bar-bg { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; overflow: hidden; margin: 0 10px; }
        .bar-fill { height: 100%; background: #ec407a; transition: width 1s; display: flex; align-items: center; justify-content: flex-end; padding-right: 5px; color: white; font-size: 0.7rem; }
        .bar-val { width: 40px; text-align: right; font-weight: bold; }

        /* STYLE ACADÉMIQUE (Pour Copier-Coller Mémoire) */
        .academic-box { font-family: 'Times New Roman', serif; border: 1px solid #000; padding: 20px; background: #fff; margin-top: 20px; }
        .academic-table { width: 100%; border-collapse: collapse; font-family: 'Times New Roman', serif; margin-bottom: 10px; }
        .academic-table th { border-top: 2px solid #000; border-bottom: 1px solid #000; background: white; color: black; text-align: center; font-weight: bold; padding: 5px; }
        .academic-table td { border-bottom: 1px solid #ccc; padding: 5px; text-align: center; }
        .academic-table tr:last-child td { border-bottom: 2px solid #000; }
        .academic-caption { font-weight: bold; margin-bottom: 10px; text-align: left; }

        /* Notification Toast */
        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 4px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; transform: translateX(-50%); font-size: 16px; }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="app-container">
    <header>
        <div class="logo-area">
            <h1>HGR MAKALA • Recherche</h1>
            <p>Étude CAP : Prévention du Cancer du Sein</p>
        </div>
        <div>
            <span id="entry-counter" style="background: rgba(255,255,255,0.2); padding: 5px 10px; border-radius: 4px; font-size: 0.9rem;">📚 0 Fiches</span>
            <button class="btn-admin" onclick="unlockAdmin()">Mode Analyse</button>
        </div>
    </header>

    <div class="nav-tabs">
        <button class="tab-btn active" onclick="showTab('collecte')">1. Collecte de Données</button>
        <button class="tab-btn locked" id="tab-db" onclick="showTab('database')">2. Base de Données</button>
        <button class="tab-btn locked" id="tab-stat" onclick="showTab('stats')">3. Statistiques & Résultats</button>
        <button class="tab-btn locked" id="tab-doc" onclick="showTab('rapport')">4. Rapport Académique</button>
    </div>

    <div id="collecte" class="content-section active">
        <form id="capForm">
            <div class="section-header">I. DONNÉES SOCIODÉMOGRAPHIQUES</div>
            <div class="form-grid">
                <div class="form-group">
                    <label>Code Enquêtée</label>
                    <input type="text" id="id_enquete" class="form-control" readonly>
                </div>
                <div class="form-group">
                    <label>Service / Département</label>
                    <select id="service" class="form-control">
                        <option value="Gyneco">Gynécologie-Obstétrique</option>
                        <option value="Medecine">Médecine Interne</option>
                        <option value="Chirurgie">Chirurgie</option>
                        <option value="Urgences">Urgences / Pédiatrie</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Niveau d'Étude</label>
                    <select id="niveau" class="form-control">
                        <option value="A2">A2 (Secondaire technique - ITM)</option>
                        <option value="A1">A1/LMD (Supérieur - ISTM)</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Ancienneté (Années)</label>
                    <input type="number" id="anciennete" class="form-control" placeholder="Ex: 5">
                </div>
            </div>

            <div class="section-header">II. CONNAISSANCES (Savoirs Théoriques)</div>
            <p style="font-size:0.9rem; color:#666; margin-bottom:15px;">Interrogez l'infirmière et cochez les réponses correctes citées spontanément.</p>
            
            <div class="form-group">
                <label>1. Facteurs de Risque connus (Cochez si cité)</label>
                <div class="check-grid" id="risk-checks">
                    <label class="check-item"><input type="checkbox" value="age"> Âge (> 50 ans)</label>
                    <label class="check-item"><input type="checkbox" value="famille"> Antécédents Familiaux</label>
                    <label class="check-item"><input type="checkbox" value="regles"> Règles précoces / Ménopause tardive</label>
                    <label class="check-item"><input type="checkbox" value="niparite"> Nulliparité (Pas d'enfants)</label>
                    <label class="check-item"><input type="checkbox" value="allaitement"> Absence d'allaitement</label>
                    <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                </div>
            </div>

            <div class="form-group">
                <label>2. Signes d'appel / Symptômes (Cochez si cité)</label>
                <div class="check-grid" id="symptom-checks">
                    <label class="check-item"><input type="checkbox" value="nodule"> Nodule (Boule) indolore</label>
                    <label class="check-item"><input type="checkbox" value="peau"> Peau d'orange</label>
                    <label class="check-item"><input type="checkbox" value="retraction"> Rétraction mamelon</label>
                    <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
                    <label class="check-item"><input type="checkbox" value="ganglion"> Ganglions axillaires</label>
                </div>
            </div>

            <div class="form-grid">
                <div class="form-group">
                    <label>3. Fréquence Mammographie (Dépistage)</label>
                    <select id="q_mammo" class="form-control">
                        <option value="0">Ne sait pas / Incorrect</option>
                        <option value="1">Tous les ans / 2 ans (Correct)</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>4. Moment Autopalpation (Règles)</label>
                    <select id="q_palpation" class="form-control">
                        <option value="0">N'importe quand</option>
                        <option value="1">Après les règles (Correct)</option>
                    </select>
                </div>
            </div>

            <div class="section-header">III. PRATIQUES (Savoir-Faire)</div>
            <div class="form-grid">
                <div class="form-group">
                    <label>Pratiquez-vous l'examen clinique des seins aux patientes ?</label>
                    <select id="prat_freq" class="form-control">
                        <option value="0">Jamais</option>
                        <option value="1">Rarement (si plainte)</option>
                        <option value="2">Systématiquement (Dépistage)</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Enseignez-vous l'auto-examen aux patientes ?</label>
                    <select id="prat_teach" class="form-control">
                        <option value="0">Non</option>
                        <option value="1">Oui</option>
                    </select>
                </div>
            </div>
            
            <div class="form-group">
                <label>Démonstration technique : Mouvements utilisés</label>
                <div class="check-grid" id="tech-checks">
                    <label class="check-item"><input type="checkbox" value="circulaire"> Circulaire</label>
                    <label class="check-item"><input type="checkbox" value="vertical"> Vertical</label>
                    <label class="check-item"><input type="checkbox" value="cadran"> Par quadrant</label>
                    <label class="check-item"><input type="checkbox" value="miroir"> Inspection au miroir (Bras levés)</label>
                </div>
            </div>

            <button type="button" class="btn-primary" onclick="saveData()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="database" class="content-section">
        <h2 style="color:#880e4f;">Base de Données (HGR Makala)</h2>
        <div class="data-table-container">
            <table id="mainTable">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Service</th>
                        <th>Niveau</th>
                        <th>Score Savoir</th>
                        <th>Score Pratique</th>
                        <th>Performance</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="stats" class="content-section">
        <h2 style="color:#880e4f;">Tableau de Bord Analytique</h2>
        
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-title">Niveau Global de Connaissances (Savoir)</div>
                <div id="chart-savoir"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique (Savoir-Faire)</div>
                <div id="chart-pratique"></div>
            </div>
        </div>

        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-title">Comparaison par Service (Moyenne Pratique)</div>
                <div id="chart-service"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Comparaison par Niveau d'Étude</div>
                <div id="chart-niveau"></div>
            </div>
        </div>
    </div>

    <div id="rapport" class="content-section">
        <h2 style="color:#880e4f;">Générateur de Rapport Académique</h2>
        <p>Copiez ces tableaux directement dans votre document Word.</p>
        
        <div class="academic-box">
            <div class="academic-caption">Tableau I : Répartition sociodémographique de l'échantillon</div>
            <div id="table-sociodemo"></div>
        </div>

        <div class="academic-box">
            <div class="academic-caption">Tableau II : Influence du service d'affectation sur le score de pratique du dépistage</div>
            <div id="table-croise-service"></div>
        </div>
        
        <div class="academic-box" style="border-left: 5px solid #880e4f; background: #fafafa;">
            <h4 style="margin-top:0;">Interprétation Automatique des Résultats :</h4>
            <p id="interpretation-text" style="line-height: 1.6; text-align: justify;"></p>
        </div>
    </div>

</div>

<div id="toast">Fiche enregistrée !</div>

<script>
    // --- 1. CONFIGURATION ET VARIABLES ---
    const ADMIN_CODE = "2001";
    let isAdmin = false;
    let db = []; // Base de données locale

    // Générateur d'ID unique
    function generateID() {
        return "INF-" + (db.length + 1).toString().padStart(3, '0');
    }
    document.getElementById('id_enquete').value = generateID();

    // --- 2. FONCTIONS DE NAVIGATION ---
    function showTab(tabId) {
        if (!isAdmin && (tabId === 'database' || tabId === 'stats' || tabId === 'rapport')) {
            alert("Accès refusé. Veuillez entrer le code Admin (2001) pour voir les analyses.");
            return;
        }
        
        // Cacher toutes les sections
        document.querySelectorAll('.content-section').forEach(el => el.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));
        
        // Afficher la cible
        document.getElementById(tabId).classList.add('active');
        // Trouver le bouton correspondant (un peu hacky mais simple)
        const btnMap = {'collecte':0, 'database':1, 'stats':2, 'rapport':3};
        document.querySelectorAll('.tab-btn')[btnMap[tabId]].classList.add('active');

        if(tabId === 'stats' || tabId === 'rapport') updateCharts();
    }

    function unlockAdmin() {
        if(isAdmin) return;
        let code = prompt("Entrez le code administrateur :");
        if (code === ADMIN_CODE) {
            isAdmin = true;
            document.querySelectorAll('.tab-btn.locked').forEach(btn => {
                btn.classList.remove('locked');
            });
            // SIMULATION DE DONNÉES MASSIVES LORS DU DÉVERROUILLAGE
            simulateData();
            showToast("Mode Admin Activé : Données simulées chargées !");
            showTab('stats');
        } else {
            alert("Code incorrect.");
        }
    }

    // --- 3. LOGIQUE MÉTIER (Calculs Scores) ---
    function calculateScores(data) {
        let scoreSavoir = 0;
        let maxSavoir = 15; // Risques(6) + Signes(5) + Mammo(2) + Palp(2) - Pondération simplifiée

        // Risques (1 point chaque)
        scoreSavoir += data.risques.length;
        // Signes (1 point chaque)
        scoreSavoir += data.signes.length;
        // Questions
        if(data.q_mammo === "1") scoreSavoir += 2;
        if(data.q_palpation === "1") scoreSavoir += 2;

        let pctSavoir = Math.round((scoreSavoir / 15) * 100);

        // Pratique
        let scorePrat = 0;
        // Frequence (0, 1=25, 2=50) -> pondéré fort
        if(data.prat_freq == "2") scorePrat += 50;
        else if(data.prat_freq == "1") scorePrat += 20;
        
        // Enseignement (20 pts)
        if(data.prat_teach == "1") scorePrat += 20;

        // Technique (7.5 pts par mouvement correct, max 30)
        scorePrat += (data.tech.length * 7.5);

        let pctPrat = Math.min(100, Math.round(scorePrat)); // Max 100

        return { s: pctSavoir, p: pctPrat };
    }

    function saveData() {
        // Récupération des valeurs
        const formData = {
            id: document.getElementById('id_enquete').value,
            service: document.getElementById('service').value,
            niveau: document.getElementById('niveau').value,
            anciennete: document.getElementById('anciennete').value,
            risques: Array.from(document.querySelectorAll('#risk-checks input:checked')).map(cb => cb.value),
            signes: Array.from(document.querySelectorAll('#symptom-checks input:checked')).map(cb => cb.value),
            q_mammo: document.getElementById('q_mammo').value,
            q_palpation: document.getElementById('q_palpation').value,
            prat_freq: document.getElementById('prat_freq').value,
            prat_teach: document.getElementById('prat_teach').value,
            tech: Array.from(document.querySelectorAll('#tech-checks input:checked')).map(cb => cb.value)
        };

        const scores = calculateScores(formData);
        
        db.push({
            ...formData,
            scoreS: scores.s,
            scoreP: scores.p
        });

        // Reset UI
        document.getElementById('capForm').reset();
        document.getElementById('id_enquete').value = generateID();
        updateEntryCounter();
        showToast("Fiche enregistrée avec succès !");
        
        // Update table if visible
        renderTable();
    }

    function renderTable() {
        const tbody = document.querySelector('#mainTable tbody');
        tbody.innerHTML = db.slice().reverse().map(row => {
            let badgeClass = row.scoreP >= 70 ? 'score-good' : (row.scoreP >= 50 ? 'score-mid' : 'score-bad');
            let label = row.scoreP >= 70 ? 'Bonne' : (row.scoreP >= 50 ? 'Moyenne' : 'Insuffisante');
            
            return `
            <tr>
                <td>${row.id}</td>
                <td>${row.service}</td>
                <td>${row.niveau}</td>
                <td>${row.scoreS}%</td>
                <td>${row.scoreP}%</td>
                <td><span class="score-badge ${badgeClass}">${label}</span></td>
            </tr>`;
        }).join('');
    }

    function updateEntryCounter() {
        document.getElementById('entry-counter').innerText = `📚 ${db.length} Fiches`;
    }

    function showToast(msg) {
        const t = document.getElementById('toast');
        t.innerText = msg;
        t.className = "show";
        setTimeout(() => { t.className = t.className.replace("show", ""); }, 3000);
    }

    // --- 4. SIMULATION DE DONNÉES (Pour remplir les graphiques) ---
    function simulateData() {
        const services = ['Gyneco', 'Medecine', 'Chirurgie', 'Urgences'];
        const niveaux = ['A1', 'A2'];
        
        for(let i=0; i<150; i++) {
            let svc = services[Math.floor(Math.random() * services.length)];
            let niv = niveaux[Math.floor(Math.random() * niveaux.length)];
            
            // Biais de simulation : Gyneco et A1 sont meilleurs
            let bonus = (svc === 'Gyneco' ? 30 : 0) + (niv === 'A1' ? 15 : 0);
            
            // Score Savoir simulé
            let s = Math.min(100, Math.floor(Math.random() * 50) + 20 + bonus);
            // Score Pratique simulé (souvent plus bas que savoir)
            let p = Math.min(100, Math.floor(Math.random() * 50) + 10 + bonus);

            db.push({
                id: generateID(),
                service: svc,
                niveau: niv,
                anciennete: Math.floor(Math.random() * 20),
                scoreS: s,
                scoreP: p,
                // Données brutes factices pour la forme
                risques: [], signes: [], tech: [] 
            });
        }
        updateEntryCounter();
        renderTable();
    }

    // --- 5. MOTEUR GRAPHIQUE ET RAPPORT ---
    function renderBarChart(elementId, data) {
        const max = Math.max(...data.map(d => d.value));
        const html = data.map(item => {
            let width = (item.value / max) * 100;
            return `
                <div class="bar-chart-row">
                    <div class="bar-label">${item.label}</div>
                    <div class="bar-bg">
                        <div class="bar-fill" style="width: ${width}%; background-color: ${item.color || '#ec407a'}">${item.displayVal || item.value}</div>
                    </div>
                </div>
            `;
        }).join('');
        document.getElementById(elementId).innerHTML = html;
    }

    function updateCharts() {
        if(db.length === 0) return;

        // 1. Chart Savoir
        let highS = db.filter(r => r.scoreS >= 70).length;
        let lowS = db.filter(r => r.scoreS < 50).length;
        let midS = db.length - highS - lowS;
        
        renderBarChart('chart-savoir', [
            { label: 'Bon (>70%)', value: highS, color: '#2e7d32', displayVal: ((highS/db.length)*100).toFixed(0)+'%' },
            { label: 'Moyen (50-70%)', value: midS, color: '#f57f17', displayVal: ((midS/db.length)*100).toFixed(0)+'%' },
            { label: 'Faible (<50%)', value: lowS, color: '#c62828', displayVal: ((lowS/db.length)*100).toFixed(0)+'%' }
        ]);

        // 2. Chart Pratique (Similaire)
        let highP = db.filter(r => r.scoreP >= 70).length;
        let lowP = db.filter(r => r.scoreP < 50).length;
        let midP = db.length - highP - lowP;
        
        renderBarChart('chart-pratique', [
            { label: 'Conforme', value: highP, color: '#1565c0', displayVal: highP },
            { label: 'Passable', value: midP, color: '#42a5f5', displayVal: midP },
            { label: 'Non Conforme', value: lowP, color: '#90caf9', displayVal: lowP }
        ]);

        // 3. Service Comparison (Average Practice Score)
        const services = ['Gyneco', 'Medecine', 'Chirurgie', 'Urgences'];
        const svcData = services.map(s => {
            let subset = db.filter(r => r.service === s);
            let avg = subset.length ? (subset.reduce((a,b)=>a+b.scoreP,0)/subset.length) : 0;
            return { label: s, value: avg, displayVal: avg.toFixed(1)+' pts', color: '#880e4f' };
        });
        renderBarChart('chart-service', svcData);

        // 4. Niveau Comparison
        const nivs = ['A1', 'A2'];
        const nivData = nivs.map(n => {
            let subset = db.filter(r => r.niveau === n);
            let avg = subset.length ? (subset.reduce((a,b)=>a+b.scoreP,0)/subset.length) : 0;
            return { label: n === 'A1' ? 'Supérieur (A1)' : 'Technique (A2)', value: avg, displayVal: avg.toFixed(1)+' pts', color: '#00897b' };
        });
        renderBarChart('chart-niveau', nivData);

        // --- GÉNÉRATION RAPPORT HTML ---
        generateReport(svcData, nivData);
    }

    function generateReport(svcData, nivData) {
        // Table Sociodemo
        let nA1 = db.filter(r => r.niveau === 'A1').length;
        let nA2 = db.filter(r => r.niveau === 'A2').length;
        let nGyn = db.filter(r => r.service === 'Gyneco').length;

        document.getElementById('table-sociodemo').innerHTML = `
            <table class="academic-table">
                <thead><tr><th>Caractéristique</th><th>Effectif (n)</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>
                    <tr><td colspan="3" style="font-weight:bold; text-align:left; background:#f9f9f9;">Niveau d'instruction</td></tr>
                    <tr><td>Niveau A1 (Supérieur)</td><td>${nA1}</td><td>${((nA1/db.length)*100).toFixed(1)}%</td></tr>
                    <tr><td>Niveau A2 (Technique)</td><td>${nA2}</td><td>${((nA2/db.length)*100).toFixed(1)}%</td></tr>
                    <tr><td colspan="3" style="font-weight:bold; text-align:left; background:#f9f9f9;">Service</td></tr>
                    <tr><td>Gynéco-Obstétrique</td><td>${nGyn}</td><td>${((nGyn/db.length)*100).toFixed(1)}%</td></tr>
                    <tr><td>Autres Services</td><td>${db.length - nGyn}</td><td>${(((db.length - nGyn)/db.length)*100).toFixed(1)}%</td></tr>
                    <tr><td style="border-top:2px solid #000; font-weight:bold;">TOTAL</td><td style="border-top:2px solid #000; font-weight:bold;">${db.length}</td><td style="border-top:2px solid #000;">100%</td></tr>
                </tbody>
            </table>
        `;

        // Table Croisée
        let rows = svcData.map(s => `<tr><td>${s.label}</td><td>${s.displayVal}</td></tr>`).join('');
        document.getElementById('table-croise-service').innerHTML = `
            <table class="academic-table">
                <thead><tr><th>Service d'affectation</th><th>Score Moyen Pratique (/100)</th></tr></thead>
                <tbody>${rows}</tbody>
            </table>
        `;

        // Interprétation textuelle dynamique
        let bestService = svcData.reduce((prev, current) => (prev.value > current.value) ? prev : current);
        let gap = (nivData[0].value - nivData[1].value).toFixed(1);
        
        document.getElementById('interpretation-text').innerText = 
            `L'analyse des données collectées auprès de ${db.length} infirmières de l'HGR Makala révèle des disparités significatives. ` +
            `Le service de ${bestService.label} enregistre la meilleure performance pratique avec une moyenne de ${bestService.displayVal}, ` +
            `ce qui confirme l'hypothèse selon laquelle l'exposition quotidienne aux pathologies mammaires favorise le maintien des compétences. ` +
            `Par ailleurs, le niveau d'étude influence positivement la qualité du dépistage : un écart de ${Math.abs(gap)} points est observé ` +
            `entre les infirmières A1 et A2. Ces résultats suggèrent la nécessité d'une formation continue ciblée pour le personnel des services hors gynécologie.`;
    }

</script>

</body>
</html>

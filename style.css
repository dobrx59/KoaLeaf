import confetti from "https://cdn.skypack.dev/canvas-confetti";

document.addEventListener('DOMContentLoaded', () => {
    let score = 0;
    const date = new Date();
    const idMois = `knotes-${date.getFullYear()}-${date.getMonth()}`;
    
    const quotes = [
        "Un koala dort 20h par jour, respecte ton repos.",
        "Même l'eucalyptus prend son temps pour grandir.",
        "Ta journée est une feuille de ton arbre.",
        "Le calme est le meilleur des guides.",
        "Reste accroché à tes rêves, comme un koala à sa branche."
    ];

    const btnsKoala = document.querySelectorAll('.btn-koala');
    const btnSauvegarder = document.getElementById('btn-sauvegarder');
    const btnRetour = document.getElementById('btn-retour');
    const modal = document.getElementById('modal-details');
    const btnCloseModal = document.getElementById('close-modal');

    btnsKoala.forEach(btn => {
        btn.onclick = () => {
            btnsKoala.forEach(b => b.classList.remove('selected'));
            btn.classList.add('selected');
            score = parseInt(btn.dataset.score);
        };
    });

    btnSauvegarder.onclick = () => {
        if (score === 0) return alert("Choisis ton Koala ! 🐨");
        const dataMois = JSON.parse(localStorage.getItem(idMois)) || {};
        dataMois[date.getDate()] = {
            score,
            plus: document.getElementById('note-plus').value,
            moins: document.getElementById('note-moins').value
        };
        localStorage.setItem(idMois, JSON.stringify(dataMois));

        const couleurs = ['#FF8B94', '#FFD3B6', '#FFF9C4', '#DCEDC1', '#A8E6CF'];
        confetti({ particleCount: 150, spread: 70, origin: { y: 0.6 }, colors: [couleurs[score - 1]] });

        setTimeout(afficherArbre, 1000);
    };

    btnCloseModal.onclick = () => modal.classList.add('cache');
    window.onclick = (e) => { if (e.target == modal) modal.classList.add('cache'); };
    btnRetour.onclick = () => {
        document.getElementById('ecran-calendrier').classList.add('cache');
        document.getElementById('ecran-saisie').classList.remove('cache');
    };

    function afficherArbre() {
        document.getElementById('ecran-saisie').classList.add('cache');
        document.getElementById('ecran-calendrier').classList.remove('cache');
        
        const container = document.getElementById('branches-target');
        container.innerHTML = "";
        
        const dataMois = JSON.parse(localStorage.getItem(idMois)) || {};
        const nbJours = new Date(date.getFullYear(), date.getMonth() + 1, 0).getDate();

        const branches = [];
        for (let i = 0; i < 4; i++) {
            const b = document.createElement('div');
            b.className = 'branche-semaine';
            container.appendChild(b);
            branches.push(b);
        }

        for (let i = 1; i <= nbJours; i++) {
            const indexBranche = Math.min(Math.floor((i - 1) / 8), 3);
            const d = dataMois[i];
            const f = document.createElement('div');
            
            f.className = `feuille ${d ? 'f-' + d.score : 'f-0'}`;
            f.innerText = i;
            
            if (d) {
                f.onclick = () => {
                    document.getElementById('modal-date').innerText = `Jour ${i}`;
                    document.getElementById('modal-plus').innerText = d.plus || "🌿";
                    document.getElementById('modal-moins').innerText = d.moins || "🐨";
                    modal.classList.remove('cache');
                };
            }
            branches[indexBranche].appendChild(f);
        }
        document.getElementById('koala-quote-text').innerText = `"${quotes[Math.floor(Math.random() * quotes.length)]}"`;
    }

    if ((JSON.parse(localStorage.getItem(idMois)) || {})[date.getDate()]) afficherArbre();
});

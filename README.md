# vindeux.github.io
<!DOCTYPE html>
<html>
<head>
    <title>Tableau des Compagnies</title>
    <style>
        table {
            border-collapse: collapse;
            width: 60%;
            margin: 20px;
        }

        th, td {
            border: 1px solid black;
            padding: 8px;
            text-align: center;
        }

        button {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>Tableau des Compagnies</h1>

    <table id="tableau">
        <tr>
            <th>Nom</th>
            <th>Cotisation</th>
            <th>Ajouter/Retirer</th>
            <th>Actions</th>
        </tr>
        
        <!-- Lignes du tableau avec des noms fixes et cotisation 10 -->
        <tr>
            <td>CIE National des Eaux</td>
            <td id="cotisation1">10</td>
            <td><input type="number" id="valeurModif1" placeholder="Valeur"></td>
            <td>
                <button onclick="ajouterRetirerCotisation(1, 'ajouter')">Ajouter</button>
                <button onclick="ajouterRetirerCotisation(1, 'retirer')">Retirer</button>
            </td>
        </tr>
        <tr>
            <td>Nom2</td>
            <td id="cotisation2">10</td>
            <td><input type="number" id="valeurModif2" placeholder="Valeur"></td>
            <td>
                <button onclick="ajouterRetirerCotisation(2, 'ajouter')">Ajouter</button>
                <button onclick="ajouterRetirerCotisation(2, 'retirer')">Retirer</button>
            </td>
        </tr>
        <!-- Répétez pour les lignes 3 à 10 -->
        <!-- ... -->

    </table>

    <button onclick="varierCotisations()">Varier les Cotisations</button>
    <button onclick="chuteCotisations()">Chute</button>
    <button onclick="essorCotisations()">Essor</button>

    <script>
        var cotisationsInitiales = [10, 10, 10, 10, 10, 10, 10, 10, 10, 10];
        var historiqueVariations = [];

        function ajouterRetirerCotisation(index, action) {
            var tableau = document.getElementById("tableau");
            var celluleCotisation = tableau.rows[index].cells[1];
            var inputValeurModif = document.getElementById("valeurModif" + index);

            var valeurModif = parseFloat(inputValeurModif.value) || 0;

            if (action === 'ajouter') {
                celluleCotisation.innerHTML = (parseFloat(celluleCotisation.innerHTML) + valeurModif).toFixed(2);
            } else {
                celluleCotisation.innerHTML = (parseFloat(celluleCotisation.innerHTML) - valeurModif).toFixed(2);
            }
        }

        function varierCotisations() {
            var tableau = document.getElementById("tableau");

            for (var i = 1; i <= 10; i++) {
                var celluleCotisation = tableau.rows[i].cells[1];

                var variation = Math.random() * 0.2 - 0.1;
                var cotisationActuelle = parseFloat(celluleCotisation.innerHTML);
                var nouvelleCotisation = cotisationActuelle * (1 + variation);

                celluleCotisation.innerHTML = nouvelleCotisation.toFixed(2);

                if (!historiqueVariations[i - 1]) {
                    historiqueVariations[i - 1] = [];
                }
                historiqueVariations[i - 1].push({
                    variation: variation,
                    nouvelleCotisation: nouvelleCotisation
                });
            }
            console.log(historiqueVariations);
        }

        function chuteCotisations() {
            var tableau = document.getElementById("tableau");

            for (var i = 1; i <= 10; i++) {
                var celluleCotisation = tableau.rows[i].cells[1];

                var chute = Math.random() * 0.3 + 0.1;
                var cotisationActuelle = parseFloat(celluleCotisation.innerHTML);
                var nouvelleCotisation = cotisationActuelle * (1 - chute);

                celluleCotisation.innerHTML = nouvelleCotisation.toFixed(2);

                if (!historiqueVariations[i - 1]) {
                    historiqueVariations[i - 1] = [];
                }
                historiqueVariations[i - 1].push({
                    variation: -chute,
                    nouvelleCotisation: nouvelleCotisation
                });
            }
            console.log(historiqueVariations);
        }

        function essorCotisations() {
            var tableau = document.getElementById("tableau");

            for (var i = 1; i <= 10; i++) {
                var celluleCotisation = tableau.rows[i].cells[1];

                var essor = Math.random() * 0.3 + 0.1;
                var cotisationActuelle = parseFloat(celluleCotisation.innerHTML);
                var nouvelleCotisation = cotisationActuelle * (1 + essor);

                celluleCotisation.innerHTML = nouvelleCotisation.toFixed(2);

                if (!historiqueVariations[i - 1]) {
                    historiqueVariations[i - 1] = [];
                }
                historiqueVariations[i - 1].push({
                    variation: essor,
                    nouvelleCotisation: nouvelleCotisation
                });
            }
            console.log(historiqueVariations);
        }
 // Fonction pour stocker les cotisations dans le localStorage
        function storeCotisations(cotisations) {
            localStorage.setItem("cotisations", JSON.stringify(cotisations));
        }

        // Fonction pour récupérer les cotisations depuis le localStorage
        function loadCotisations() {
            var storedCotisations = localStorage.getItem("cotisations");
            if (storedCotisations) {
                return JSON.parse(storedCotisations).map(Number);
            }
            return [10, 10, 10, 10, 10, 10, 10, 10, 10, 10]; // Valeurs par défaut
        }
    </script>
</body>
</html>

# PAYOFF
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Grafico Payoff Long Call</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f0f0f0;
        }
        canvas {
            max-width: 800px;
            margin: 0 auto;
        }
        .tooltip {
            position: relative;
            display: inline-block;
        }
        .tooltip .tooltiptext {
            visibility: hidden;
            width: 200px;
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 5px;
            border-radius: 5px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            margin-left: -100px;
            opacity: 0;
            transition: opacity 0.3s;
        }
        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }
        .input-container {
            margin-bottom: 20px;
            text-align: center;
        }
        .input-container label {
            margin-right: 10px;
        }
        .input-container input {
            padding: 5px;
            margin-right: 10px;
            width: 100px;
        }
    </style>
</head>
<body>
    <h2>Grafico Payoff Long Call</h2>
    <div class="input-container">
        <label for="strikePrice">Prezzo di esercizio (K): </label>
        <input type="number" id="strikePrice" value="50" step="1">
        <label for="premium">Premio pagato (C): </label>
        <input type="number" id="premium" value="5" step="0.1">
    </div>
    <div class="tooltip">
        <canvas id="payoffChart" width="800" height="400"></canvas>
        <span class="tooltiptext">Payoff netto di una Long Call: profitto sopra il punto di pareggio</span>
    </div>

    <script>
        // Parametri iniziali della Long Call
        let K = 50;  // Prezzo di esercizio
        let C = 5;   // Premio pagato
        const maxPrice = 100;  // Prezzo massimo dell'attività (valore fisso)
        const step = 1;        // Incremento del prezzo (valore fisso)
        const minPrice = 0;    // Prezzo minimo dell'attività

        // Inizializzazione del grafico
        const ctx = document.getElementById('payoffChart').getContext('2d');
        let payoffChart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: [],
                datasets: [
                    {
                        label: 'Payoff Netto Long Call (€)',
                        data: [],
                        borderColor: 'rgb(75, 192, 192)',
                        tension: 0.1,
                        fill: false
                    }
                ]
            },
            options: {
                scales: {
                    x: {
                        title: {
                            display: true,
                            text: 'Prezzo dell\'attività sottostante'
                        },
                        grid: {
                            drawOnChartArea: true
                        }
                    },
                    y: {
                        title: {
                            display: true,
                            text: 'Payoff Netto (€)'
                        },
                        beginAtZero: true
                    }
                },
                plugins: {
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                let label = context.dataset.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                label += context.parsed.y + ' €';
                                return label;
                            }
                        }
                    },
                    annotation: {
                        annotations: {
                            strikeLine: {
                                type: 'line',
                                xMin: K,
                                xMax: K,
                                borderColor: 'rgba(255, 99, 132, 0.5)',
                                borderWidth: 2,
                                borderDash: [5, 5],
                                label: {
                                    display: true,
                                    content: 'Strike Price',
                                    position: 'start',
                                    backgroundColor: 'rgba(255, 99, 132, 0.8)',
                                    color: 'white'
                                }
                            },
                            breakEvenLine: {
                                type: 'line',
                                xMin: K + C,
                                xMax: K + C,
                                borderColor: 'rgba(54, 162, 235, 0.5)',
                                borderWidth: 2,
                                borderDash: [5, 5],
                                label: {
                                    display: true,
                                    content: 'Break-Even Point',
                                    position: 'start',
                                    backgroundColor: 'rgba(54, 162, 235, 0.8)',
                                    color: 'white'
                                }
                            }
                        }
                    }
                }
            }
        });

        // Funzione per calcolare e aggiornare il grafico
        function updateChart() {
            // Leggi i valori dagli input
            K = parseFloat(document.getElementById('strikePrice').value) || 50;
            C = parseFloat(document.getElementById('premium').value) || 5;

            // Calcolo dei dati del payoff
            const labels = [];
            const payoffData = [];
            for (let S_T = minPrice; S_T <= maxPrice; S_T += step) {
                labels.push(S_T.toFixed(2));
                const payoffLordo = Math.max(0, S_T - K); // Payoff lordo
                const payoffNetto = payoffLordo - C;      // Payoff netto
                payoffData.push(payoffNetto);
            }

            // Aggiorna il grafico
            payoffChart.data.labels = labels;
            payoffChart.data.datasets[0].data = payoffData;

            // Aggiorna le linee di annotazione (strike price e break-even point)
            payoffChart.options.plugins.annotation.annotations.strikeLine.xMin = K;
            payoffChart.options.plugins.annotation.annotations.strikeLine.xMax = K;
            payoffChart.options.plugins.annotation.annotations.breakEvenLine.xMin = K + C;
            payoffChart.options.plugins.annotation.annotations.breakEvenLine.xMax = K + C;

            payoffChart.update();
        }

        // Aggiungi listener per aggiornare il grafico automaticamente quando gli input cambiano
        document.getElementById('strikePrice').addEventListener('input', updateChart);
        document.getElementById('premium').addEventListener('input', updateChart);

        // Disegna il grafico iniziale
        updateChart();
    </script>
</body>
</html>

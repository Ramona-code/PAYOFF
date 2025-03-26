<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Payoff Insieme</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        canvas {
            border: 1px solid black;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Put Short, Put Long, Call Long, Call Short</h1>
    <canvas id="payoffCanvas" width="600" height="400"></canvas>
    <script>
        function drawPayoff(){
            const canvas = document.getElementById("payoffCanvas");
            const ctx = canvas.getContext("2d");

            // Pulizia del canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Definizione del payoff
            const width = canvas.width;
            const height = canvas.height;
            const strikePrice1 = width / 8;
            const strikePrice2 = width * 3 / 8;
            const strikePrice3 = width * 5 / 8;
            const strikePrice4 = width * 7 / 8;
            const profitHeight = height * 2 / 3;
            const lossHeight1 = height / 2 + 5;
            const lossHeight2 = height * 3 / 4 - 5;
            const lossHeight3 = height * 3 / 4 + 5;
            const lossHeight4 = height / 2 - 5;

            // Disegno degli assi
            ctx.beginPath();
            // Asse X
            ctx.moveTo(0, profitHeight);
            ctx.lineTo(width, profitHeight);
            // No asse Y
            ctx.strokeStyle = "black";
            ctx.stroke();

            // Disegno delle rette degli Strike
            ctx.beginPath();
            ctx.moveTo(strikePrice1, 0);
            ctx.lineTo(strikePrice1, height);
            ctx.moveTo(strikePrice2, 0);
            ctx.lineTo(strikePrice2, height);
            ctx.moveTo(strikePrice3, 0);
            ctx.lineTo(strikePrice3, height);
            ctx.moveTo(strikePrice4, 0);
            ctx.lineTo(strikePrice4, height);
            ctx.strokeStyle = "red";
            ctx.setLineDash([5, 5]); // Linea tratteggiata
            ctx.stroke();
            ctx.setLineDash([]); //Ripristina lo stile normale

            // Disegno payoff put short
            ctx.beginPath();
            ctx.moveTo(strikePrice2-20, lossHeight1);
            ctx.lineTo(strikePrice1+(-lossHeight1+profitHeight), lossHeight1);
            ctx.lineTo(strikePrice1+(-lossHeight1+profitHeight) - 200, lossHeight1 + 200);
            ctx.strokeStyle = "blue";
            ctx.lineWidth = 2;
            ctx.stroke();

            // Disegno payoff put long
            ctx.beginPath();
            ctx.moveTo(strikePrice3-20, lossHeight2);
            ctx.lineTo(strikePrice2+(lossHeight2-profitHeight), lossHeight2);
            ctx.lineTo(strikePrice2+(lossHeight2-profitHeight) - 200, lossHeight2 - 200);
            ctx.strokeStyle = "green";
            ctx.lineWidth = 2;
            ctx.stroke();

            // Disegno payoff call long
            ctx.beginPath();
            ctx.moveTo(strikePrice2+20, lossHeight3);
            ctx.lineTo(strikePrice3-(lossHeight3-profitHeight), lossHeight3);
            ctx.lineTo(strikePrice3-(lossHeight3-profitHeight) + 200, lossHeight3 - 200);
            ctx.strokeStyle = "yellow";
            ctx.lineWidth = 2;
            ctx.stroke();

            // Disegno payoff call short
            ctx.beginPath();
            ctx.moveTo(strikePrice3+20, lossHeight4);
            ctx.lineTo(strikePrice4-(-lossHeight4+profitHeight), lossHeight4);
            ctx.lineTo(strikePrice4-(-lossHeight4+profitHeight) + 200, lossHeight4 + 200);
            ctx.strokeStyle = "orange";
            ctx.lineWidth = 2;
            ctx.stroke();


            // Aggiunta etichette sugli assi
            ctx.font = "14px Arial";
            ctx.fillStyle = "black";
            // Asse X
            ctx.fillText("Prezzo",width - 50, profitHeight - 10);
            ctx.fillText("100", strikePrice1 - 20, profitHeight - 5);
            ctx.fillText("200", strikePrice2 - 20, profitHeight - 5);
            ctx.fillText("300", strikePrice3 - 20, profitHeight - 5);
            ctx.fillText("400", strikePrice4 - 20, profitHeight - 5);


        }
    </script>
    <br>
    <button onclick="drawPayoff()">Disegna Payoff</button>
</body>
</html>

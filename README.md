<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AntiSense Blue</title>
    <style>
        :root {
            --ocean: #0077be;
            --cyan: #00f2ff;
            --bg: #050a10;
        }

        body {
            background: var(--bg);
            color: white;
            font-family: 'Segoe UI', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background: radial-gradient(circle at center, #0a1f35 0%, #050a10 100%);
        }

        .container {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(15px);
            padding: 30px;
            border-radius: 20px;
            width: 360px;
            border: 1px solid rgba(0, 242, 255, 0.2);
            box-shadow: 0 0 40px rgba(0,0,0,0.7);
            text-align: center;
        }

        h2 { color: var(--cyan); letter-spacing: 3px; font-weight: 300; text-transform: uppercase; }

        input, select {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border-radius: 10px;
            border: 1px solid #1a3a5a;
            background: rgba(0,0,0,0.5);
            color: white;
            box-sizing: border-box;
            outline: none;
        }

        button {
            width: 100%;
            padding: 15px;
            margin-top: 10px;
            border-radius: 10px;
            border: none;
            background: linear-gradient(135deg, var(--ocean), var(--cyan));
            color: #000;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            text-transform: uppercase;
        }

        button:hover { transform: scale(1.02); filter: brightness(1.1); }

        .range-box { margin: 20px 0; text-align: left; }
        input[type="range"] { width: 100%; accent-color: var(--cyan); margin-top: 8px; }

        .grid-res {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 20px;
            display: none;
        }

        .card {
            background: rgba(0, 119, 190, 0.1);
            padding: 10px;
            border-radius: 10px;
            border-left: 2px solid var(--cyan);
            text-align: left;
        }

        .label { font-size: 0.65rem; color: var(--cyan); text-transform: uppercase; letter-spacing: 1px; }
        .val { display: block; font-size: 1.1rem; font-weight: bold; }

        #appSection { display: none; }
    </style>
</head>
<body>

    <div id="loginSection" class="container">
        <h2>ANTISENSE</h2>
        <p style="font-size: 0.8rem; color: #888; margin-bottom: 20px;">DIGITE A SENHA</p>
        <input type="password" id="passInput" placeholder="Digite aqui...">
        <button onclick="logar()">ENTRAR</button>
    </div>

    <div id="appSection" class="container">
        <h2>DASHBOARD</h2>

        <select id="celular">
            <option value="infinix">Infinix</option>
            <option value="iphone">iPhone</option>
            <option value="zte">ZTE</option>
            <option value="intel">Intel</option>
            <option value="samsung">Samsung</option>
            <option value="xiaomi">Xiaomi</option>
        </select>

        <div class="range-box">
            <span class="label">Velocidade do Cursor</span>
            <input type="range" min="1" max="100" value="50">
        </div>

        <button onclick="gerarSensi()">GERAR SENSIBILIDADE</button>

        <div id="painel" class="grid-res">
            <div class="card"><span class="label">Geral</span><span id="g1" class="val"></span></div>
            <div class="card"><span class="label">Red Dot</span><span id="g2" class="val"></span></div>
            <div class="card"><span class="label">Mira 2x</span><span id="g3" class="val"></span></div>
            <div class="card"><span class="label">Mira 4x</span><span id="g4" class="val"></span></div>
            <div class="card"><span class="label">AWM</span><span id="g5" class="val"></span></div>
            <div class="card"><span class="label">Olhadinha</span><span id="g6" class="val"></span></div>
            
            <div id="cardDinamico" class="card" style="grid-column: span 2; border-color: #fff;">
                <span id="lblDinamico" class="label">DPI</span>
                <span id="valDinamico" class="val" style="color: #00ffaa;"></span>
            </div>

            <div class="card" style="grid-column: span 2; border-color: yellow;">
                <span class="label">Tamanho do Botão</span>
                <span id="valBtn" class="val" style="color: yellow;"></span>
            </div>
        </div>
    </div>

    <script>
        function logar() {
            const senha = document.getElementById('passInput').value;
            if(senha === "2012") {
                document.getElementById('loginSection').style.display = 'none';
                document.getElementById('appSection').style.display = 'block';
            } else {
                alert("Senha incorreta!");
            }
        }

        function n(min, max) { return Math.floor(Math.random() * (max - min + 1)) + min; }

        function gerarSensi() {
            document.getElementById('painel').style.display = 'grid';
            
            for(let i=1; i<=6; i++) {
                document.getElementById('g'+i).innerText = n(130, 200);
            }

            document.getElementById('valBtn').innerText = n(30, 60) + "%";

            const marca = document.getElementById('celular').value;
            const cardD = document.getElementById('cardDinamico');
            const lbl = document.getElementById('lblDinamico');
            const val = document.getElementById('valDinamico');

            if(marca === "zte") {
                cardD.style.display = "none";
            } else {
                cardD.style.display = "block";
                if(marca === "iphone") {
                    lbl.innerText = "CICLOS (iOS)";
                    val.innerText = n(2, 10);
                } else {
                    // Intel agora gera entre 400 e 1000 igual Samsung, Xiaomi e Infinix
                    lbl.innerText = "DPI";
                    val.innerText = n(400, 1000);
                }
            }
        }
    </script>
</body>
</html>

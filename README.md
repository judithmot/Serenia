<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MindBoost - Bienestar Diario</title>
    <style>
        body { font-family: Arial, sans-serif; background: linear-gradient(to bottom, #87CEEB, #FFF); text-align: center; padding: 20px; margin: 0; }
        .container { max-width: 400px; margin: auto; background: white; padding: 20px; border-radius: 15px; box-shadow: 0 0 20px rgba(0,0,0,0.1); }
        h1 { color: #4CAF50; }
        button { background: #4CAF50; color: white; border: none; padding: 12px 20px; border-radius: 8px; cursor: pointer; margin: 5px; font-size: 14px; }
        textarea { width: 100%; height: 100px; margin: 10px 0; border-radius: 8px; padding: 10px; }
        #ad { background: #f0f0f0; padding: 10px; margin: 10px 0; border-radius: 8px; }
        .premium { background: #FFD700; color: black; }
        .login-btn { background: #2196F3; }
        .logout-btn { background: #f44336; }
        input { padding: 10px; margin: 5px; border-radius: 8px; border: 1px solid #ccc; }
    </style>
</head>
<body>
    <div class="container">
        <h1>🌿 MindBoost</h1>
        
        <!-- Sección de Login -->
        <div id="authSection">
            <p><strong>Inicia sesión para guardar tus datos</strong></p>
            <input type="email" id="email" placeholder="Tu email" style="width: 70%;"><br>
            <input type="password" id="password" placeholder="Tu contraseña" style="width: 70%;"><br>
            <button class="login-btn" onclick="login()">Entrar</button>
            <button class="login-btn" onclick="register()">Registrarse</button>
        </div>
        
        <div id="userSection" style="display:none;">
            <p>👤 <span id="userEmail"></span></p>
            <button class="logout-btn" onclick="logout()">Cerrar Sesión</button>
        </div>
        
        <hr>
        
        <h2>💡 Tip del Día</h2>
        <p id="tip" style="font-size: 18px; color: #333;">Respira profundo y enfócate en el presente.</p>
        <button onclick="newTip()">Nuevo Tip</button>
        
        <h2>📓 Diario de Gratitud</h2>
        <textarea id="diary" placeholder="Escribe algo por lo que estés agradecido hoy..."></textarea>
        <button onclick="saveDiary()">💾 Guardar</button>
        <p id="savedMsg"></p>
        
        <div id="ad">
            <p style="color: #888; font-size: 12px;">📢 Espacio para publicidad</p>
        </div>
        
        <hr>
        
        <h2>📚 Mi Libro en Amazon</h2>
        <a href="https://www.amazon.com" target="_blank">
            <button style="background: #FF9900;">Comprar en Amazon 🛒</button>
        </a>
        
        <h2>⭐ Actualizar a Premium</h2>
        <p>Sin anuncios + tips ilimitados por $1.99/mes</p>
        <button class="premium" onclick="upgrade()">¡Actualizar Ahora!</button>
        
        <br><br>
        <p style="color: #888; font-size: 12px;">© 2024 MindBoost - Tu bienestar primero</p>
    </div>
    
    <script>
        // Simulación de base de datos local
        let currentUser = null;
        
        const tips = [
            "Practica mindfulness 5 minutos hoy.",
            "Escribe 3 cosas por las que estés agradecido.",
            "Llama a un amigo o familiar.",
            "Sal a caminar 15 minutos al aire libre.",
            "Respira profundo: inhale 4s, exhale 6s.",
            "Evita redes sociales por 1 hora.",
            "Escucha música que te haga feliz.",
            "Bebe agua y come saludable hoy."
        ];
        
        function newTip() {
            const randomTip = tips[Math.floor(Math.random() * tips.length)];
            document.getElementById('tip').textContent = randomTip;
        }
        
        function saveDiary() {
            const entry = document.getElementById('diary').value;
            if (!entry) {
                alert("¡Escribe algo primero!");
                return;
            }
            
            if (currentUser) {
                // Simulación: guardar en "nube"
                localStorage.setItem('diary_' + currentUser, entry);
                document.getElementById('savedMsg').textContent = "✓ Guardado en la nube (simulado)";
            } else {
                // Guardar local
                localStorage.setItem('diary_guest', entry);
                document.getElementById('savedMsg').textContent = "✓ Guardado en tu dispositivo";
            }
            alert("¡Guardado!");
        }
        
        function login() {
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            
            if (email && password) {
                currentUser = email;
                document.getElementById('authSection').style.display = 'none';
                document.getElementById('userSection').style.display = 'block';
                document.getElementById('userEmail').textContent = email;
                
                // Cargar diario guardado
                const savedDiary = localStorage.getItem('diary_' + email);
                if (savedDiary) document.getElementById('diary').value = savedDiary;
            } else {
                alert("¡Ingresa email y contraseña!");
            }
        }
        
        function register() {
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            
            if (email && password) {
                alert("¡Registro exitoso! Ahora inicia sesión.");
            } else {
                alert("¡Ingresa email y contraseña para registrarte!");
            }
        }
        
        function logout() {
            currentUser = null;
            document.getElementById('authSection').style.display = 'block';
            document.getElementById('userSection').style.display = 'none';
            document.getElementById('email').value = '';
            document.getElementById('password').value = '';
        }
        
        function upgrade() {
            alert("🎉 ¡Gracias por tu interés en Premium! \n\nEn la versión completa, esto redirigirá a pago con Google Play. ¿Quieres seguir usando la app gratis?");
        }
        
        // Cargar diario de invitado al iniciar
        window.onload = () => {
            const guestDiary = localStorage.getItem('diary_guest');
            if (guestDiary) document.getElementById('diary').value = guestDiary;
        };
    </script>
</body>
</html>

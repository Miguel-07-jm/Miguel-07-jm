
<!---
Miguel-07-jm/Miguel-07-jm is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        #wheel {
            width: 300px;
            height: 300px;
            border-radius: 50%;
            border: 5px solid #000;
            position: relative;
            overflow: hidden;
            transform: rotate(0deg);
            transition: transform 5s ease-out;
        }
        .section {
            width: 50%;
            height: 50%;
            position: absolute;
            transform-origin: 100% 100%;
            clip-path: polygon(100% 0, 100% 100%, 50% 50%);
        }
        .section:nth-child(1) { background-color: yellow; transform: rotate(0deg); }
        .section:nth-child(2) { background-color: blue; transform: rotate(36deg); }
        .section:nth-child(3) { background-color: red; transform: rotate(72deg); }
        .section:nth-child(4) { background-color: green; transform: rotate(108deg); }
        .section:nth-child(5) { background-color: purple; transform: rotate(144deg); }
        .section:nth-child(6) { background-color: orange; transform: rotate(180deg); }
        .section:nth-child(7) { background-color: white; transform: rotate(216deg); }
        .section:nth-child(8) { background-color: black; transform: rotate(252deg); }
        .section:nth-child(9) { background-color: lime; transform: rotate(288deg); }
        .section:nth-child(10) { background-color: lightblue; transform: rotate(324deg); }
        #result {
            margin-top: 20px;
            font-size: 24px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div id="wheel">
        <div class="section"></div>
        <div class="section"></div>
        <div class="section"></div>
        <div class="section"></div>
        <div class="section"></div>
        <div class="section"></div>
        <div class="section"></div>
        <div class="section"></div>
        <div class="section"></div>
        <div class="section"></div>
    </div>
    <div id="result"></div>
    <button onclick="spin()">Girar la Ruleta</button>

    <script>
        const wheel = document.getElementById("wheel");
        const result = document.getElementById("result");
        let sections = [
            { color: 'AMARILLO', theme: 'MINIONS' },
            { color: 'AZUL', theme: 'PITUFOS' },
            { color: 'ROJO', theme: 'LOS INCREÍBLES' },
            { color: 'VERDE', theme: 'EL ENCANTO' },
            { color: 'MORADO', theme: 'HOTEL TRANSILVANIA' },
            { color: 'NARANJA', theme: 'INTENSAMENTE' },
            { color: 'BLANCO', theme: 'KUNG FU PANDA' },
            { color: 'NEGRO', theme: 'COCO' },
            { color: 'VERDE LIMÓN', theme: 'TOY STORY' },
            { color: 'AZUL CELESTE', theme: 'MONSTERS UNIVERSITY' }
        ];

        function spin() {
            if (sections.length === 0) {
                alert("No quedan más temáticas.");
                return;
            }

            let deg = Math.floor(5000 + Math.random() * 5000);
            wheel.style.transform = `rotate(${deg}deg)`;

            setTimeout(() => {
                let normalizedDeg = deg % 360; // Normaliza el ángulo
                let anglePerSection = 360 / sections.length;
                let selectedIndex = Math.floor(normalizedDeg / anglePerSection);

                let selectedSection = sections[selectedIndex];
                result.innerText = `Color: ${selectedSection.color} - Temática: ${selectedSection.theme}`;

                // Elimina la sección seleccionada
                sections.splice(selectedIndex, 1);
                const sectionElements = document.querySelectorAll('.section');
                sectionElements[selectedIndex].style.display = 'none';

                // Vuelve a ajustar las rotaciones de las secciones restantes
                let angle = 360 / sections.length;
                sectionElements.forEach((section, index) => {
                    if (section.style.display !== 'none') {
                        section.style.transform = `rotate(${index * angle}deg)`;
                    }
                });

            }, 5000);  // 5 segundos de espera antes de mostrar la temática
        }
    </script>
</body>
</html>

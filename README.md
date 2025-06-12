# Consultor-a-Liderazgo
Pagina para que el alumno valide su tipo de tendencia a liderazgo
<!DOCTYPE html>

<html lang="es" class="scroll-smooth">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Explorador Interactivo de Estilos de Liderazgo</title>

    <script src="https://cdn.tailwindcss.com"></script>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <link rel="preconnect" href="https://fonts.googleapis.com">

    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">

    <!-- Chosen Palette: Calm Authority -->

    <!-- Application Structure Plan: La aplicación está diseñada como una SPA de varias secciones con una barra de navegación fija para facilitar el acceso no lineal. La estructura es: 1) Inicio: Una bienvenida y resumen. 2) Explorar Estilos: Un diseño de tarjetas interactivas para descubrir cada modelo de liderazgo, evitando la sobrecarga de información. 3) Compáralos: Una herramienta de comparación visual con un gráfico de radar dinámico para analizar las diferencias clave, superando una tabla estática. 4) Autoevaluación: Una implementación interactiva del cuestionario del informe con resultados visuales (gráficos de barras) para una autocomprensión inmediata. 5) Desarrollo: Consejos prácticos presentados en un formato de acordeón para una fácil digestión. Esta arquitectura transforma el informe lineal en una herramienta de aprendizaje experiencial, guiando al usuario desde el conocimiento general hasta la autoevaluación y el desarrollo personal de una manera lógica e intuitiva. -->

    <!-- Visualization & Content Choices: 1) Modelos de Liderazgo -> Goal: Informar/Explorar -> Viz: Tarjetas interactivas (HTML/CSS) que revelan contenido detallado -> Interaction: Click para expandir -> Justification: Presentación limpia y organizada. 2) Comparación de Estilos -> Goal: Comparar/Analizar -> Viz: Gráfico de Radar (Chart.js) -> Interaction: Selección de estilos mediante checkboxes para actualizar el gráfico dinámicamente -> Justification: El radar permite una comparación multidimensional instantánea (control, autonomía, etc.), que es más perspicaz que una tabla. 3) Cuestionario SAIF -> Goal: Autoevaluación -> Viz: Formulario interactivo y Gráfico de Barras de resultados (Chart.js) -> Interaction: El usuario responde y presiona un botón para ver sus puntuaciones visualizadas -> Justification: Convierte un test estático en una experiencia personalizada y atractiva, con resultados fáciles de interpretar. 4) Rejilla de Blake y Mouton -> Goal: Organizar/Explicar -> Viz: Rejilla 2x2 interactiva (HTML/CSS) -> Interaction: Hover para ver tooltip, Click para ver detalle -> Justification: Una representación visual-espacial es superior al texto para explicar un modelo bidimensional. -->

    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <style>

        body {

            font-family: 'Inter', sans-serif;

            background-color: #FDFBF7;

            color: #2c3e50;

        }

        .chart-container {

            position: relative;

            width: 100%;

            max-width: 600px;

            margin-left: auto;

            margin-right: auto;

            height: 400px;

            max-height: 50vh;

        }

        @media (min-width: 768px) {

            .chart-container {

                height: 500px;

            }

        }

        .nav-link {

            transition: color 0.3s, border-bottom-color 0.3s;

            border-bottom: 2px solid transparent;

        }

        .nav-link:hover, .nav-link.active {

            color: #b49b6b;

            border-bottom-color: #b49b6b;

        }

        .btn-primary {

            background-color: #2c3e50;

            color: #FDFBF7;

            transition: background-color 0.3s;

        }

        .btn-primary:hover {

            background-color: #3e5670;

        }

        .card {

            background-color: #FFFFFF;

            border: 1px solid #e0e0e0;

            transition: transform 0.3s, box-shadow 0.3s;

        }

        .card:hover {

            transform: translateY(-5px);

            box-shadow: 0 10px 20px rgba(0,0,0,0.08);

        }

        .blake-mouton-grid-item {

            border: 2px solid #e0e0e0;

            transition: background-color 0.3s, border-color 0.3s;

        }

        .blake-mouton-grid-item:hover {

            background-color: #f0f5f9;

            border-color: #b49b6b;

        }

    </style>

</head>

<body class="antialiased">



    <header id="main-header" class="bg-white/80 backdrop-blur-md shadow-sm sticky top-0 z-50">

        <nav class="container mx-auto px-6 py-4 flex justify-between items-center">

            <h1 class="text-xl md:text-2xl font-bold text-gray-800">Liderazgo Interactivo</h1>

            <div class="hidden md:flex items-center space-x-6">

                <a href="#inicio" class="nav-link px-2 py-1">Inicio</a>

                <a href="#explorar" class="nav-link px-2 py-1">Explorar Estilos</a>

                <a href="#comparar" class="nav-link px-2 py-1">Compáralos</a>

                <a href="#autoevaluacion" class="nav-link px-2 py-1">Autoevaluación</a>

                <a href="#desarrollo" class="nav-link px-2 py-1">Desarrollo</a>

            </div>

            <button id="mobile-menu-button" class="md:hidden focus:outline-none">

                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>

            </button>

        </nav>

        <div id="mobile-menu" class="hidden md:hidden">

            <a href="#inicio" class="block py-2 px-6 text-sm hover:bg-gray-100">Inicio</a>

            <a href="#explorar" class="block py-2 px-6 text-sm hover:bg-gray-100">Explorar Estilos</a>

            <a href="#comparar" class="block py-2 px-6 text-sm hover:bg-gray-100">Compáralos</a>

            <a href="#autoevaluacion" class="block py-2 px-6 text-sm hover:bg-gray-100">Autoevaluación</a>

            <a href="#desarrollo" class="block py-2 px-6 text-sm hover:bg-gray-100">Desarrollo</a>

        </div>

    </header>



    <main>

        <section id="inicio" class="py-20 bg-white">

            <div class="container mx-auto px-6 text-center">

                <h2 class="text-4xl font-bold mb-4">Descubre el Poder del Liderazgo</h2>

                <p class="text-lg text-gray-600 max-w-3xl mx-auto mb-8">El liderazgo efectivo es clave para el éxito organizacional. No existe un único estilo "ideal"; el mejor enfoque depende de la situación y del equipo. Esta herramienta interactiva está diseñada para ayudarte a explorar los diferentes estilos de liderazgo, entender sus matices y descubrir cuál resuena más contigo.</p>

                <a href="#autoevaluacion" class="btn-primary font-bold py-3 px-8 rounded-full inline-block">Comienza tu Autoevaluación</a>

            </div>

        </section>



        <section id="explorar" class="py-20">

            <div class="container mx-auto px-6">

                <div class="text-center mb-12">

                    <h2 class="text-3xl font-bold">Explora los Modelos de Liderazgo</h2>

                    <p class="text-md text-gray-600 max-w-2xl mx-auto mt-2">Haz clic en cada tarjeta para desplegar la información detallada de cada modelo y sus estilos asociados. Comprender estas teorías es el primer paso para convertirte en un líder más adaptable y efectivo.</p>

                </div>

                <div id="styles-container" class="space-y-8"></div>

            </div>

        </section>

       

        <section id="comparar" class="py-20 bg-white">

            <div class="container mx-auto px-6">

                <div class="text-center mb-12">

                    <h2 class="text-3xl font-bold">Compara Estilos de Liderazgo</h2>

                    <p class="text-md text-gray-600 max-w-2xl mx-auto mt-2">Selecciona al menos dos estilos de la lista para ver una comparación visual de sus características principales en el gráfico de radar. Esto te ayudará a entender rápidamente sus fortalezas y debilidades relativas.</p>

                </div>

                <div class="flex flex-col md:flex-row gap-8">

                    <div id="comparison-options" class="w-full md:w-1/3">

                        <h3 class="font-bold mb-4 text-lg">Selecciona estilos para comparar:</h3>

                        <div class="space-y-2"></div>

                    </div>

                    <div class="w-full md:w-2/3">

                         <div class="chart-container">

                            <canvas id="comparison-chart"></canvas>

                        </div>

                    </div>

                </div>

            </div>

        </section>



        <section id="autoevaluacion" class="py-20">

            <div class="container mx-auto px-6">

                 <div class="text-center mb-12">

                    <h2 class="text-3xl font-bold">Cuestionario de Autoevaluación</h2>

                    <p class="text-md text-gray-600 max-w-2xl mx-auto mt-2">Este cuestionario te ayudará a identificar tu estilo de liderazgo predominante. Responde honestamente basándote en tu comportamiento habitual. No hay respuestas correctas o incorrectas; el objetivo es la autoconciencia.</p>

                </div>

                <div class="max-w-4xl mx-auto">

                    <div id="questionnaire-form" class="bg-white p-8 rounded-xl shadow-md"></div>

                    <div id="results-section" class="hidden mt-12">

                        <h3 class="text-2xl font-bold text-center mb-6">Tus Resultados</h3>

                         <div class="bg-white p-8 rounded-xl shadow-md">

                            <div class="chart-container h-80 max-h-[40vh]">

                                <canvas id="results-chart"></canvas>

                            </div>

                            <div id="results-interpretation" class="mt-8 space-y-4"></div>

                            <button id="get-llm-advice-button" class="btn-primary font-bold py-3 px-8 rounded-full inline-block mt-8 w-full">Obtener Consejos de Desarrollo ✨</button>

                            <div id="llm-development-advice" class="mt-8 p-4 bg-gray-50 rounded-lg hidden">

                                <p class="text-gray-600 text-center" id="llm-advice-text">Generando consejos...</p>

                            </div>

                        </div>

                    </div>

                </div>

            </div>

        </section>



        <section id="desarrollo" class="py-20 bg-white">

             <div class="container mx-auto px-6">

                <div class="text-center mb-12">

                    <h2 class="text-3xl font-bold">Claves para el Desarrollo del Liderazgo</h2>

                    <p class="text-md text-gray-600 max-w-2xl mx-auto mt-2">Identificar tu estilo es solo el comienzo. Un liderazgo efectivo requiere un desarrollo continuo. Aquí tienes estrategias prácticas que puedes implementar para mejorar tus habilidades y adaptarte a cualquier desafío.</p>

                </div>

                <div id="development-container" class="max-w-3xl mx-auto space-y-4"></div>

            </div>

        </section>

    </main>



    <footer class="bg-gray-800 text-white py-8">

        <div class="container mx-auto px-6 text-center">

            <p>&copy; 2025 Explorador de Liderazgo Interactivo. Creado a partir del informe de investigación.</p>

            <p class="text-sm text-gray-400 mt-2">Todos los contenidos se basan en el "Reporte Exhaustivo sobre Estilos de Liderazgo y Herramienta de Autoevaluación".</p>

        </div>

    </footer>



    <script>

        document.addEventListener('DOMContentLoaded', function() {

           

            const data = {

                leadershipModels: [

                    {

                        title: "Estilos Basados en la Autoridad",

                        description: "Estos estilos se diferencian por el grado de control que el líder ejerce sobre la toma de decisiones. Representan un espectro desde el control total hasta la autonomía completa del equipo.",

                        styles: [

                            { name: "Autocrático", content: "<strong>Características:</strong> El líder toma todas las decisiones de forma unilateral, centralizando el poder. La comunicación es descendente y no se busca el consenso.<br><strong>Ventajas:</strong> Toma de decisiones rápida y eficiente, especialmente en crisis. Claridad en las directrices.<br><strong>Desventajas:</strong> Reduce la motivación, creatividad y autonomía del equipo. Puede generar un ambiente de trabajo tenso.<br><strong>Ideal para:</strong> Situaciones de emergencia, equipos sin experiencia o tareas que requieren una ejecución precisa y rápida." },

                            { name: "Democrático", content: "<strong>Características:</strong> El líder fomenta la participación del equipo en la toma de decisiones. Se valoran las ideas y la comunicación es bidireccional.<br><strong>Ventajas:</strong> Aumenta el compromiso, la satisfacción y la innovación. Genera un mejor clima laboral.<br><strong>Desventajas:</strong> El proceso de decisión puede ser más lento. Requiere habilidad para gestionar desacuerdos.<br><strong>Ideal para:</strong> Definir estrategias a largo plazo, resolver problemas complejos y en equipos con expertos maduros." },

                            { name: "Laissez-Faire (Dejar hacer)", content: "<strong>Características:</strong> El líder delega casi toda la autoridad en el equipo, interviniendo mínimamente. Otorga total libertad y autonomía.<br><strong>Ventajas:</strong> Fomenta al máximo la creatividad y la responsabilidad individual. Alta satisfacción en equipos auto-gestionados.<br><strong>Desventajas:</strong> Riesgo de caos, falta de dirección y baja productividad si el equipo no es maduro o proactivo. Puede haber falta de responsabilidad.<br><strong>Ideal para:</strong> Equipos de alto rendimiento, compuestos por expertos altamente cualificados y motivados." }

                        ]

                    },

                    {

                        title: "Estilos Orientados a la Conducta",

                        description: "Estos modelos no se centran en la autoridad, sino en los comportamientos observables del líder, principalmente en su enfoque hacia las tareas o hacia las personas.",

                        content: `<div class="mt-6">

                            <h4 class="font-bold text-lg mb-4 text-center">La Rejilla Gerencial de Blake y Mouton</h4>

                            <p class="text-center text-sm text-gray-500 mb-4">Este modelo mapea el liderazgo en dos ejes: preocupación por las personas (vertical) y por las tareas (horizontal). Haz clic en un cuadrante para ver el detalle.</p>

                            <div class="relative max-w-lg mx-auto aspect-square">

                                <div class="absolute bottom-0 left-0 right-0 text-center font-semibold p-2">Preocupación por las Tareas →</div>

                                <div class="absolute top-0 bottom-0 left-0 text-center font-semibold p-2" style="writing-mode: vertical-rl; transform: rotate(180deg);">Preocupación por las Personas →</div>

                                <div class="grid grid-cols-2 grid-rows-2 w-full h-full pt-10 pl-10">

                                    <div data-style="Country Club" class="blake-mouton-grid-item flex items-center justify-center p-4 text-center cursor-pointer"><span>1.9<br>Club Social</span></div>

                                    <div data-style="Team Leader" class="blake-mouton-grid-item flex items-center justify-center p-4 text-center cursor-pointer font-bold bg-teal-50"><span>9.9<br>Líder de Equipo</span></div>

                                    <div data-style="Impoverished" class="blake-mouton-grid-item flex items-center justify-center p-4 text-center cursor-pointer"><span>1.1<br>Liderazgo Ajeno</span></div>

                                    <div data-style="Authoritarian" class="blake-mouton-grid-item flex items-center justify-center p-4 text-center cursor-pointer"><span>9.1<br>Autoritario</span></div>

                                </div>

                                  <div data-style="Middle of the Road" class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-1/3 h-1/3 blake-mouton-grid-item flex items-center justify-center p-2 text-center cursor-pointer bg-gray-100"><span>5.5<br>Intermedio</span></div>

                            </div>

                            <div id="blake-mouton-detail" class="mt-6 p-4 bg-gray-50 rounded-lg text-sm transition-opacity duration-300 opacity-0"></div>

                        </div>`

                    },

                    {

                        title: "Enfoques Situacionales y de Contingencia",

                        description: "La premisa central es que no hay un único estilo de liderazgo 'mejor'. La efectividad depende de la situación, especialmente de la madurez y preparación de los miembros del equipo.",

                        styles: [

                            { name: "Liderazgo Situacional (Hersey-Blanchard)", content: "Este modelo sugiere adaptar el estilo de liderazgo (combinando comportamiento de tarea y de relación) al nivel de desarrollo del colaborador para una tarea específica.<br><br><strong>E1 - Dirigir:</strong> Alta tarea, baja relación. Para colaboradores con baja competencia y bajo compromiso.<br><strong>E2 - Persuadir/Entrenar:</strong> Alta tarea, alta relación. Para colaboradores con algo de competencia pero bajo compromiso.<br><strong>E3 - Participar/Apoyar:</strong> Baja tarea, alta relación. Para colaboradores con alta competencia pero compromiso variable o falta de confianza.<br><strong>E4 - Delegar:</strong> Baja tarea, baja relación. Para colaboradores con alta competencia y alto compromiso." }

                        ]

                    },

                    {

                        title: "Estilos Modernos de Influencia",

                        description: "Estos estilos se enfocan en cómo el líder motiva a sus seguidores y en la naturaleza de la relación que construye con ellos para alcanzar objetivos.",

                        styles: [

                            { name: "Transformacional", content: "<strong>Características:</strong> Inspira y motiva al equipo a lograr resultados extraordinarios, a menudo superando sus propios intereses por el bien del grupo. Fomenta la innovación y el desarrollo personal.<br><strong>Ventajas:</strong> Aumenta significativamente el rendimiento, la productividad y la retención de talento. Fomenta una cultura de crecimiento.<br><strong>Desventajas:</strong> Puede crear dependencia del carisma del líder. Requiere una gran energía y visión.<br><strong>Ideal para:</strong> Industrias dinámicas y cambiantes que requieren innovación constante, como la tecnología." },

                            { name: "Transaccional", content: "<strong>Características:</strong> Se basa en un intercambio de recompensas por rendimiento. El líder clarifica roles y tareas, y utiliza premios y castigos para motivar.<br><strong>Ventajas:</strong> Es muy efectivo para lograr objetivos a corto plazo y asegurar la consistencia en los procesos.<br><strong>Desventajas:</strong> Puede limitar la creatividad y la iniciativa más allá de lo estrictamente requerido. Menos inspirador.<br><strong>Ideal para:</strong> Entornos altamente estructurados donde la consistencia y el cumplimiento de procedimientos son cruciales, como la manufactura." },

                            { name: "Coach", content: "<strong>Características:</strong> Actúa como un facilitador que ayuda a los miembros del equipo a descubrir y desarrollar su potencial. Se centra en el crecimiento a largo plazo.<br><strong>Ventajas:</strong> Crea un ambiente altamente motivador y desarrolla habilidades clave en el equipo.<br><strong>Desventajas:</strong> Requiere mucho tiempo y paciencia por parte del líder. No es efectivo si el colaborador no es receptivo.<br><strong>Ideal para:</strong> Desarrollo de talento y en equipos que buscan un crecimiento profesional continuo." },

                             { name: "Mentor", content: "<strong>Características:</strong> El líder es un ejemplo a seguir que guía y comparte su experiencia y conocimientos para promover el potencial de los demás.<br><strong>Ventajas:</strong> Facilita el cumplimiento de objetivos y acelera la integración de nuevos miembros.<br><strong>Desventajas:</strong> La observación continua puede generar estrés. Un enfoque excesivo en los resultados puede limitar la creatividad.<br><strong>Ideal para:</strong> Procesos de gestión del talento y para la rápida inclusión de nuevos colaboradores en la organización." }

                        ]

                    },

                ],

                blakeMoutonStyles: {

                    "Impoverished": "<strong>1.1 - Liderazgo Ajeno (Empobrecido):</strong> El líder muestra bajo interés tanto en las personas como en las tareas. Delega al máximo y evita tomar responsabilidades. El resultado es a menudo la desorganización y la insatisfacción.",

                    "Country Club": "<strong>1.9 - Club Social:</strong> Alta preocupación por las personas y baja por las tareas. El líder crea un ambiente cómodo y amigable, pero a expensas de la productividad y los resultados.",

                    "Authoritarian": "<strong>9.1 - Autoritario (Producir o Perecer):</strong> Alta preocupación por las tareas y baja por las personas. El líder se enfoca exclusivamente en la eficiencia y los resultados, a menudo tratando a los empleados como meros instrumentos.",

                    "Team Leader": "<strong>9.9 - Líder de Equipo:</strong> Alta preocupación tanto por las tareas como por las personas. Considerado el estilo más efectivo, fomenta el trabajo en equipo, el compromiso y la alta productividad a través de la confianza y el respeto mutuo.",

                    "Middle of the Road": "<strong>5.5 - Intermedio:</strong> El líder busca un equilibrio, conformándose con un rendimiento adecuado sin presionar demasiado. Evita el conflicto, pero rara vez alcanza la excelencia."

                },

                questionnaire: [

                    { q: "Los trabajadores necesitan supervisión de cerca, o probablemente no harían sus trabajos.", style: "autocratic" },

                    { q: "Los trabajadores quieren ser parte del proceso de tomar decisiones.", style: "democratic" },

                    { q: "En situaciones complicadas, los supervisores deberían permitir a los trabajadores resolver sus propios problemas.", style: "laissez-faire" },

                    { q: "Es justo decir que la mayoría de los trabajadores son perezosos.", style: "autocratic" },

                    { q: "Guiar a los trabajadores sin presión es la clave para ser un buen supervisor.", style: "democratic" },

                    { q: "El requisito de los líderes es no meterse con los trabajadores mientras realizan sus trabajos.", style: "laissez-faire" },

                    { q: "Por lo general, los supervisores deben premiar o castigar para motivar a los trabajadores a cumplir con los objetivos organizativos.", style: "autocratic" },

                    { q: "La mayoría de los trabajadores quieren comunicación frecuente y alentadora de parte de los supervisores.", style: "democratic" },

                    { q: "Por lo general, los líderes deberían permitir a los trabajadores evaluar sus propios trabajos.", style: "laissez-faire" },

                    { q: "La mayoría de los trabajadores se siente inseguro en sus trabajos y necesita instrucciones.", style: "autocratic" },

                    { q: "Los supervisores necesitan ayudar a los trabajadores a aceptar la responsabilidad de completar sus trabajos.", style: "democratic" },

                    { q: "Los supervisores deberían dar a los trabajadores la libertad de resolver los problemas por sí mismos.", style: "laissez-faire" },

                    { q: "El supervisor es el juez de logros para los miembros de cuadrillas (grupo de trabajadores).", style: "autocratic" },

                    { q: "El trabajo del supervisor es ayudar a los trabajadores con sus “pasiones”.", style: "democratic" },

                    { q: "En la mayoría de las situaciones, los trabajadores prefieren pocas sugerencias de sus supervisores.", style: "laissez-faire" },

                    { q: "Los supervisores eficaces dan instrucciones y aclaran los procedimientos.", style: "autocratic" },

                    { q: "Las personas son fundamentalmente competentes y si se les asigna una tarea, realizarán un buen trabajo.", style: "democratic" },

                    { q: "Por lo general, es mejor dejar a los trabajadores solos y permitirles que hagan sus trabajos.", style: "laissez-faire" }

                ],

                questionnaireInterpretation: {

                    autocratic: "<strong>Estilo Autocrático:</strong> Una puntuación alta sugiere una preferencia por el control, la dirección explícita y la toma de decisiones centralizada. Valoras la disciplina y crees que los resultados se logran mejor mediante la supervisión directa.",

                    democratic: "<strong>Estilo Democrático:</strong> Una puntuación alta indica una inclinación hacia la colaboración y la participación. Fomentas la comunicación abierta y buscas construir compromiso al involucrar a los trabajadores en las decisiones.",

                    "laissez-faire": "<strong>Estilo Laissez-Faire:</strong> Una puntuación alta sugiere una fuerte creencia en la autonomía y autogestión del equipo. Prefieres delegar la autoridad y confías en la competencia de los trabajadores para lograr los objetivos."

                },

                comparisonData: {

                    labels: ['Control del Líder', 'Autonomía del Equipo', 'Foco en Tareas', 'Foco en Personas', 'Ritmo de Decisión', 'Fomento de Innovación'],

                    styles: {

                        'Autocrático': [9, 1, 9, 2, 9, 2],

                        'Democrático': [5, 7, 6, 8, 3, 8],

                        'Laissez-Faire': [1, 9, 3, 5, 5, 7],

                        'Transformacional': [6, 8, 8, 9, 6, 9],

                        'Transaccional': [7, 4, 8, 4, 7, 4],

                        'Coach': [4, 7, 5, 9, 4, 6],

                        'Mentor': [5, 6, 7, 8, 5, 7],

                    }

                },

                developmentStrategies: [

                    { title: "Establecer y Comunicar una Visión Clara", content: "Articula la visión y misión de la empresa de manera clara y motivadora para inspirar al equipo. Esto crea un sentido de pertenencia y motivación grupal." },

                    { title: "Fomentar la Comunicación Abierta", content: "Genera un ambiente donde todos los miembros del equipo se sientan cómodos expresando sus ideas, opiniones y preocupaciones." },

                    { title: "Delegar Tareas Adecuadamente", content: "Identifica las fortalezas y habilidades individuales del equipo y asigna responsabilidades que se alineen con ellas, empoderando a los colaboradores." },

                    { title: "Ser un Ejemplo a Seguir", content: "Demuestra un comportamiento ético, profesional y coherente con los valores deseados, sirviendo de modelo para el equipo." },

                    { title: "Motivar y Reconocer los Logros", content: "Celebra y reconoce activamente los éxitos individuales y colectivos para mantener la moral y el compromiso." },

                    { title: "Fomentar el Desarrollo Personal y Profesional", content: "Apoya y brinda oportunidades continuas de capacitación, mentoría y desarrollo a los colaboradores." },

                    { title: "Promover la Retroalimentación Constructiva", content: "Genera un ambiente donde la retroalimentación sea bienvenida, tanto la que se da como la que se recibe, utilizando las críticas constructivas como una oportunidad para la mejora continua." }

                ]

            };

           

            const stylesContainer = document.getElementById('styles-container');

            data.leadershipModels.forEach(model => {

                const modelCard = document.createElement('div');

                modelCard.className = 'card rounded-xl overflow-hidden';

                let contentHTML = '';

                if(model.styles) {

                    contentHTML = model.styles.map(style => `

                        <div class="p-4 border-t border-gray-200">

                           <h4 class="font-bold text-lg text-gray-800">${style.name}</h4>

                           <p class="text-sm text-gray-600 mt-2">${style.content}</p>

                        </div>

                    `).join('');

                } else if(model.content) {

                     contentHTML = `<div class="p-6">${model.content}</div>`;

                }



                modelCard.innerHTML = `

                    <div class="p-6 cursor-pointer bg-white flex justify-between items-center">

                        <div>

                            <h3 class="text-xl font-bold">${model.title}</h3>

                            <p class="text-gray-500 text-sm mt-1">${model.description}</p>

                        </div>

                        <svg class="w-6 h-6 transition-transform transform" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path></svg>

                    </div>

                    <div class="hidden bg-gray-50/50">

                        ${contentHTML}

                    </div>

                `;

                stylesContainer.appendChild(modelCard);

            });



            stylesContainer.addEventListener('click', (e) => {

                const header = e.target.closest('.p-6.cursor-pointer');

                if (header) {

                    const content = header.nextElementSibling;

                    const icon = header.querySelector('svg');

                    content.classList.toggle('hidden');

                    icon.classList.toggle('rotate-180');

                }

            });



            const blakeMoutonGrid = document.querySelector('.blake-mouton-grid-item')?.parentElement;

            if (blakeMoutonGrid) {

                const detailBox = document.getElementById('blake-mouton-detail');

                blakeMoutonGrid.addEventListener('click', (e) => {

                    const item = e.target.closest('.blake-mouton-grid-item');

                    if(item) {

                        const styleKey = item.dataset.style;

                        detailBox.innerHTML = data.blakeMoutonStyles[styleKey];

                        detailBox.classList.remove('opacity-0');

                    }

                });

            }



            const comparisonOptionsContainer = document.querySelector('#comparison-options .space-y-2');

            const comparisonChartCanvas = document.getElementById('comparison-chart');

            let comparisonChart;

           

            function updateComparisonChart() {

                const selectedStyles = Array.from(comparisonOptionsContainer.querySelectorAll('input:checked')).map(input => input.value);

               

                if (comparisonChart) {

                    comparisonChart.data.datasets = selectedStyles.map((styleName, index) => {

                        const colors = ['rgba(44, 62, 80, 0.8)', 'rgba(180, 155, 107, 0.8)', 'rgba(26, 188, 156, 0.8)', 'rgba(52, 152, 219, 0.8)'];

                        return {

                            label: styleName,

                            data: data.comparisonData.styles[s

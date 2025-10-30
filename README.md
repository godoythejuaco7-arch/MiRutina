# MiRutina
Creador de rutinas de ejercicios gratis
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Generador de Rutina Personalizada</title>
<style>
    :root {
        --turq:#11c5c6;
        --turq-dark:#0ea7a8;
        --bg:#ffffff;
        --text:#1a1a1a;
        --card:#ffffff;
        --border:#d9d9d9;
        --radius-lg:20px;
        --radius-sm:10px;
    }

    *{
        box-sizing:border-box;
        -webkit-font-smoothing:antialiased;
        font-family: system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Ubuntu,"Helvetica Neue",sans-serif;
        margin:0;
        padding:0;
    }

    body{
        background:var(--bg);
        color:var(--text);
        display:flex;
        justify-content:center;
        padding:2rem 1rem 6rem;
    }

    .app{
        width:100%;
        max-width:900px;
        display:flex;
        flex-direction:column;
        gap:1.5rem;
    }

    header{
        text-align:center;
    }

    .badge{
        display:inline-block;
        background:var(--turq);
        color:#fff;
        padding:.4rem .75rem;
        font-size:.8rem;
        font-weight:600;
        border-radius:999px;
        margin-bottom:.5rem;
    }

    h1{
        font-size:1.4rem;
        font-weight:700;
        line-height:1.2;
        color:var(--text);
        margin-bottom:.4rem;
    }

    .subtitle{
        font-size:.9rem;
        line-height:1.4;
        color:#555;
        max-width:480px;
        margin:0 auto;
    }

    /* cards */
    .card{
        background:var(--card);
        border:1px solid var(--border);
        border-radius:var(--radius-lg);
        box-shadow:0 24px 40px -12px rgba(0,0,0,.08);
        padding:1rem 1rem 1.25rem;
    }

    .card h2{
        font-size:1rem;
        font-weight:600;
        color:var(--text);
        display:flex;
        align-items:flex-start;
        gap:.5rem;
        margin-bottom:1rem;
    }
    .card h2 span.icon{
        background:var(--turq);
        color:#fff;
        font-size:.8rem;
        line-height:1rem;
        min-width:1.6rem;
        height:1.6rem;
        border-radius:.5rem;
        display:flex;
        align-items:center;
        justify-content:center;
        font-weight:700;
    }

    form{
        display:grid;
        gap:1rem;
    }

    .field{
        display:flex;
        flex-direction:column;
        gap:.4rem;
    }
    .field-row{
        display:flex;
        flex-wrap:wrap;
        gap:.75rem;
    }
    @media(min-width:600px){
        .field-row .field{
            flex:1;
        }
    }

    label{
        font-size:.8rem;
        font-weight:600;
        color:#222;
        display:flex;
        justify-content:space-between;
        flex-wrap:wrap;
        line-height:1.3;
    }
    label small{
        font-weight:400;
        color:#777;
        font-size:.7rem;
    }

    input, select, textarea{
        width:100%;
        background:#fff;
        border:1px solid var(--border);
        border-radius:var(--radius-sm);
        padding:.7rem .8rem;
        font-size:.9rem;
        color:#000;
        outline:none;
    }
    input:focus, select:focus, textarea:focus{
        border-color:var(--turq);
        box-shadow:0 0 0 3px rgb(17 197 198 / .2);
    }

    textarea{
        resize:none;
        min-height:60px;
    }

    /* botón generar */
    .btn-main{
        background:var(--turq);
        color:#fff;
        border:none;
        border-radius:var(--radius-sm);
        padding:.9rem 1rem;
        font-size:1rem;
        font-weight:600;
        cursor:pointer;
        text-align:center;
        box-shadow:0 16px 24px -8px rgba(17,197,198,.5);
        transition:all .15s;
        width:100%;
    }
    .btn-main:active{
        transform:scale(.98);
        background:var(--turq-dark);
    }

    /* Rutina resultado */
    .routine-card{
        background:#fff;
        border:2px solid var(--turq);
        border-radius:var(--radius-lg);
        box-shadow:0 32px 56px -16px rgba(0,0,0,.15);
        padding:1rem;
    }

    .routine-header{
        display:flex;
        flex-direction:column;
        gap:.5rem;
        margin-bottom:1rem;
    }

    .routine-header-top{
        display:flex;
        flex-wrap:wrap;
        gap:.5rem;
        align-items:center;
        justify-content:space-between;
    }

    .routine-title{
        font-size:1.1rem;
        font-weight:700;
        color:#000;
    }

    .routine-meta{
        font-size:.75rem;
        line-height:1.3;
        color:#444;
        display:flex;
        flex-wrap:wrap;
        gap:.5rem;
    }
    .routine-chip{
        background:var(--turq);
        color:#fff;
        font-weight:600;
        border-radius:999px;
        padding:.3rem .6rem;
        font-size:.7rem;
        line-height:1;
    }

    .routine-block{
        border:1px solid var(--border);
        border-radius:var(--radius-sm);
        padding:.8rem;
        margin-bottom:1rem;
    }
    .routine-block h3{
        font-size:.9rem;
        font-weight:600;
        color:#000;
        display:flex;
        justify-content:space-between;
        align-items:flex-start;
        flex-wrap:wrap;
        margin-bottom:.6rem;
    }
    .routine-muscle{
        font-size:.7rem;
        font-weight:500;
        background:#eefefe;
        color:#0a5c5c;
        border:1px solid #0ea7a833;
        border-radius:999px;
        padding:.2rem .5rem;
        line-height:1.2;
    }

    .exercise-list{
        display:grid;
        gap:.8rem;
    }

    .exercise-item{
        display:flex;
        gap:.8rem;
        align-items:flex-start;
    }

    .exercise-img{
        width:80px;
        height:80px;
        min-width:80px;
        border-radius:var(--radius-sm);
        overflow:hidden;
        border:1px solid var(--border);
        background:#f8f8f8;
        display:flex;
        align-items:center;
        justify-content:center;
        font-size:.7rem;
        font-weight:500;
        color:#666;
    }
    .exercise-img img{
        width:100%;
        height:100%;
        object-fit:cover;
    }

    .exercise-info{
        flex:1;
        display:flex;
        flex-direction:column;
        gap:.25rem;
    }

    .exercise-name{
        font-size:.9rem;
        font-weight:600;
        color:#000;
        line-height:1.2;
    }
    .exercise-sets{
        font-size:.8rem;
        color:#333;
    }
    .exercise-extra{
        font-size:.7rem;
        color:#666;
        line-height:1.3;
    }

    .note-box{
        background:#f8ffff;
        border:1px solid #0ea7a822;
        border-radius:var(--radius-sm);
        padding:.7rem .8rem;
        font-size:.75rem;
        color:#044;
        line-height:1.4;
        margin-top:.5rem;
    }

    footer{
        text-align:center;
        font-size:.7rem;
        color:#888;
        padding-bottom:3rem;
    }

    /* mobile spacing fix for bottom */
    @media(min-width:768px){
        body{
            padding:3rem 1rem 6rem;
        }
        h1{
            font-size:1.8rem;
        }
        .subtitle{
            font-size:1rem;
        }
        .card{
            padding:1.25rem 1.25rem 1.5rem;
        }
        .routine-card{
            padding:1.25rem 1.25rem 1.5rem;
        }
    }
</style>
</head>
<body>
<div class="app">

    <header>
        <div class="badge">Rutina personalizada</div>
        <h1>Plan de Entrenamiento Casa / Gimnasio</h1>
        <p class="subtitle">
            Completa el formulario. Te genero una rutina de cuerpo completo con series, repeticiones y ejemplos visuales.
        </p>
    </header>

    <!-- FORM -->
    <section class="card">
        <h2><span class="icon">1</span>Datos personales básicos 🧍‍♂️</h2>
        <form id="fitnessForm">
            <div class="field-row">
                <div class="field">
                    <label>Género</label>
                    <select id="genero" required>
                        <option value="">Elige...</option>
                        <option value="femenino">Femenino</option>
                        <option value="masculino">Masculino</option>
                        <option value="otro">Otro / Prefiero no decir</option>
                    </select>
                </div>
                <div class="field">
                    <label>Edad (años)</label>
                    <input type="number" id="edad" min="10" max="100" placeholder="20, 30, 40..." required />
                </div>
            </div>

            <div class="field-row">
                <div class="field">
                    <label>Peso (kg)</label>
                    <input type="number" id="peso" min="20" max="300" placeholder="Ej: 72" required />
                </div>
                <div class="field">
                    <label>Altura (cm)</label>
                    <input type="number" id="altura" min="120" max="230" placeholder="Ej: 175" required />
                </div>
            </div>

            <div class="field">
                <label>Objetivo principal <small>(elige el más importante)</small></label>
                <select id="objetivo" required>
                    <option value="">Elige...</option>
                    <option value="bajar grasa">Bajar de peso / grasa</option>
                    <option value="musculo">Ganar masa muscular</option>
                    <option value="tonificar">Tonificar / marcar</option>
                    <option value="resistencia">Mejorar resistencia</option>
                    <option value="salud">Moverme y estar más saludable</option>
                </select>
            </div>

            <hr style="border:none;border-top:1px solid var(--border);" />

            <h2><span class="icon">2</span>Estado físico y salud ❤️</h2>

            <div class="field">
                <label>Lesiones o limitaciones físicas</label>
                <textarea id="lesiones" placeholder="Rodilla izquierda, lumbar, hombro derecho... o 'ninguna'"></textarea>
            </div>

            <div class="field">
                <label>Condición médica a considerar</label>
                <textarea id="condicion" placeholder="Hipertensión, asma, etc... o 'ninguna'"></textarea>
            </div>

            <div class="field-row">
                <div class="field">
                    <label>¿Hace cuánto no entrenas?</label>
                    <select id="tiempoSinEntrenar">
                        <option value="0-3 meses">0-3 meses</option>
                        <option value="3-12 meses">3-12 meses</option>
                        <option value="1-3 años">1-3 años</option>
                        <option value="más de 3 años">Más de 3 años</option>
                    </select>
                </div>
                <div class="field">
                    <label>Nivel físico actual</label>
                    <select id="nivel" required>
                        <option value="">Elige...</option>
                        <option value="bajo">Bajo</option>
                        <option value="medio">Medio</option>
                        <option value="alto">Alto</option>
                    </select>
                </div>
            </div>

            <hr style="border:none;border-top:1px solid var(--border);" />

            <h2><span class="icon">3</span>Disponibilidad y entorno 🕓</h2>

            <div class="field-row">
                <div class="field">
                    <label>Días por semana</label>
                    <select id="dias" required>
                        <option value="">Elige...</option>
                        <option value="2">2 días</option>
                        <option value="3">3 días</option>
                        <option value="4">4 días</option>
                        <option value="5">5 días</option>
                        <option value="6">6 días</option>
                        <option value="7">7 días</option>
                    </select>
                </div>
                <div class="field">
                    <label>Duración por sesión</label>
                    <select id="duracion" required>
                        <option value="">Elige...</option>
                        <option value="20 min">20 min</option>
                        <option value="30 min">30 min</option>
                        <option value="45 min">45 min</option>
                        <option value="1 hora">1 hora</option>
                        <option value="+1 hora">Más de 1 hora</option>
                    </select>
                </div>
            </div>

            <div class="field-row">
                <div class="field">
                    <label>Horario favorito</label>
                    <select id="horario" required>
                        <option value="">Elige...</option>
                        <option value="mañana">Mañana</option>
                        <option value="tarde">Tarde</option>
                        <option value="noche">Noche</option>
                    </select>
                </div>
                <div class="field">
                    <label>¿Dónde vas a entrenar?</label>
                    <select id="lugar" required>
                        <option value="">Elige...</option>
                        <option value="casa">Casa</option>
                        <option value="gimnasio">Gimnasio</option>
                        <option value="mixto">A veces casa / a veces gym</option>
                    </select>
                </div>
            </div>

            <div class="field">
                <label>Espacio en casa</label>
                <select id="espacio">
                    <option value="pequeño">Pequeño (1-2 m², apenas colchoneta)</option>
                    <option value="normal">Normal (2x2 m puedo moverme)</option>
                    <option value="amplio">Amplio (puedo saltar / desplazarme)</option>
                </select>
            </div>

            <div class="field">
                <label>Equipo disponible</label>
                <textarea id="equipo" placeholder="Mancuernas 5kg, banda elástica, colchoneta... o 'solo peso corporal'"></textarea>
            </div>

            <hr style="border:none;border-top:1px solid var(--border);" />

            <h2><span class="icon">4</span>Preferencias y motivación ⚙️</h2>

            <div class="field">
                <label>Tipo de ejercicios que prefieres</label>
                <select id="preferencia">
                    <option value="fuerza">Fuerza / pesas</option>
                    <option value="cardio">Cardio / quema calorías</option>
                    <option value="hiit">HIIT (rápido e intenso)</option>
                    <option value="movilidad">Movilidad / postura / espalda sana</option>
                    <option value="mix">Un poco de todo</option>
                </select>
            </div>

            <div class="field-row">
                <div class="field">
                    <label>Experiencia previa entrenando</label>
                    <select id="experiencia">
                        <option value="nuevo">Nunca he seguido una rutina</option>
                        <option value="basico">Algo básico en casa o gym</option>
                        <option value="intermedio">Entrené varios meses antes</option>
                        <option value="avanzado">Años entrenando serio</option>
                    </select>
                </div>
                <div class="field">
                    <label>Motivación actual (1-10)</label>
                    <input type="number" id="motivacion" min="1" max="10" value="7" />
                </div>
            </div>

            <div class="field-row">
                <div class="field">
                    <label>Estilo de rutina</label>
                    <select id="intensidad">
                        <option value="suave">Suave y progresiva</option>
                        <option value="balanceada">Balanceada</option>
                        <option value="explosiva">Intensa y corta</option>
                    </select>
                </div>
                <div class="field">
                    <label>¿Quieres acompañamiento musical / app?</label>
                    <select id="acompanamiento">
                        <option value="musica">Con música motivante</option>
                        <option value="silencio">Prefiero silencio / foco</option>
                        <option value="app">Con guía tipo app / temporizador HIIT</option>
                    </select>
                </div>
            </div>

            <hr style="border:none;border-top:1px solid var(--border);" />

            <h2><span class="icon">5</span>Seguimiento y metas 📈</h2>

            <div class="field">
                <label>Plazo/meta temporal</label>
                <select id="plazo">
                    <option value="1 mes">Quiero arrancar el hábito (1 mes)</option>
                    <option value="3 meses">Notar cambios físicos (3 meses)</option>
                    <option value="6 meses">Cambio más notorio (6 meses)</option>
                    <option value="largo plazo">Mantener salud / largo plazo</option>
                </select>
            </div>

            <div class="field-row">
                <div class="field">
                    <label>¿Registrar avances?</label>
                    <select id="seguimiento">
                        <option value="si">Sí, peso / medidas / energía</option>
                        <option value="progreso-fotos">Solo fotos de progreso</option>
                        <option value="rendimiento">Solo rendimiento (más repeticiones)</option>
                        <option value="no">No quiero seguimiento</option>
                    </select>
                </div>
                <div class="field">
                    <label>Motivación especial</label>
                    <input id="motivacionEspecial" placeholder="Postura, verano, estrés, autoestima, etc." />
                </div>
            </div>

            <!-- Botón generar rutina -->
            <button type="button" class="btn-main" id="generarBtn">GENERAR MI RUTINA 🔥</button>
        </form>
    </section>

    <!-- RUTINA RESULTADO -->
    <section id="routineSection" class="routine-card" style="display:none;">
        <div class="routine-header">
            <div class="routine-header-top">
                <div class="routine-title">Tu Rutina Personalizada</div>
                <div class="routine-chip" id="chipLugar">Casa</div>
            </div>
            <div class="routine-meta" id="routineMeta">
                <!-- Se rellena con JS -->
            </div>
            <div class="note-box" id="alertaLesion" style="display:none;">
                ⚠ Recomendación médica: indicaste lesión/condición. Mantén técnica suave,
                evita dolor agudo y considera consulta profesional antes de forzar.
            </div>
        </div>

        <div id="routineBlocks">
            <!-- bloques de ejercicios se rellenan con JS -->
        </div>

        <div class="note-box" id="extraNotas">
            Respira entre series (60-90s fuerza / 30-45s cardio). Calienta 5 min (movilidad de cuello,
            hombros, cadera, rodillas) y termina con estiramientos suaves.
        </div>
    </section>

    <footer>
        Hecho para ti 💪 | Blanco + turquesa | Cuerpo completo
    </footer>
</div>

<script>
/*
    Mini "base de datos" de ejercicios
    Cada ejercicio tiene:
    - nombre
    - musculo
    - img (ejemplo ilustrativo con URLs genéricas a contenidos fitness libres/stock)
    - tipo ("fuerza","cardio","core","piernas","espalda","pecho","hombro","gluteos")
    - casa / gym accesibilidad
*/
const EXERCISES = [
    {
        nombre:"Sentadilla libre",
        musculo:"Piernas / Glúteos",
        tipo:"piernas",
        lugar:"casa",
        img:"https://images.pexels.com/photos/4761780/pexels-photo-4761780.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Espalda recta, rodillas alineadas con pies. Baja controlado."
    },
    {
        nombre:"Peso muerto con mancuernas",
        musculo:"Isquios / Glúteos",
        tipo:"piernas",
        lugar:"gimnasio",
        img:"https://images.pexels.com/photos/841130/pexels-photo-841130.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Empuja caderas atrás, no redondees la espalda."
    },
    {
        nombre:"Zancadas alternadas",
        musculo:"Piernas / Estabilidad",
        tipo:"piernas",
        lugar:"casa",
        img:"https://images.pexels.com/photos/4047042/pexels-photo-4047042.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Paso largo, rodilla trasera cerca del suelo."
    },
    {
        nombre:"Flexiones de pecho",
        musculo:"Pecho / Tríceps / Hombro frontal",
        tipo:"pecho",
        lugar:"casa",
        img:"https://images.pexels.com/photos/416778/pexels-photo-416778.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Manos debajo del pecho, cuerpo en línea recta. Rodillas al suelo si es difícil."
    },
    {
        nombre:"Press banca con mancuernas",
        musculo:"Pecho / Tríceps",
        tipo:"pecho",
        lugar:"gimnasio",
        img:"https://images.pexels.com/photos/1552103/pexels-photo-1552103.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Controla la bajada, no rebotes con el pecho."
    },
    {
        nombre:"Remo inclinado con mancuerna/banda",
        musculo:"Espalda alta / Bíceps",
        tipo:"espalda",
        lugar:"casa",
        img:"https://images.pexels.com/photos/5327538/pexels-photo-5327538.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Codos pegados al cuerpo, aprieta escápulas atrás."
    },
    {
        nombre:"Jalón al pecho / polea",
        musculo:"Espalda dorsal",
        tipo:"espalda",
        lugar:"gimnasio",
        img:"https://images.pexels.com/photos/7676409/pexels-photo-7676409.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Pecho arriba, tira con espalda no solo con brazos."
    },
    {
        nombre:"Plancha isométrica",
        musculo:"Core / Abdomen profundo",
        tipo:"core",
        lugar:"casa",
        img:"https://images.pexels.com/photos/4056723/pexels-photo-4056723.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Cadera ni muy alta ni muy baja. Mira al piso."
    },
    {
        nombre:"Crunch / Abdominales cortos",
        musculo:"Abdomen superior",
        tipo:"core",
        lugar:"casa",
        img:"https://images.pexels.com/photos/414029/pexels-photo-414029.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Sube controlado, no tires del cuello."
    },
    {
        nombre:"Elevación lateral mancuernas",
        musculo:"Hombro lateral / Deltoides medio",
        tipo:"hombro",
        lugar:"gimnasio",
        img:"https://images.pexels.com/photos/7676464/pexels-photo-7676464.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Codos ligeramente flexionados, sube hasta nivel hombro."
    },
    {
        nombre:"Fondos en banco / silla",
        musculo:"Tríceps",
        tipo:"brazo",
        lugar:"casa",
        img:"https://images.pexels.com/photos/4662352/pexels-photo-4662352.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Codos atrás, baja lento. Más difícil: pies más lejos."
    },
    {
        nombre:"Jumping jacks",
        musculo:"Cardio general",
        tipo:"cardio",
        lugar:"casa",
        img:"https://images.pexels.com/photos/6453399/pexels-photo-6453399.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Mantén ritmo constante, aterriza suave."
    },
    {
        nombre:"Bicicleta estática / elíptica",
        musculo:"Cardio bajo impacto",
        tipo:"cardio",
        lugar:"gimnasio",
        img:"https://images.pexels.com/photos/3823039/pexels-photo-3823039.jpeg?auto=compress&cs=tinysrgb&h=200&w=200",
        tips:"Mantén respiración constante, no bloquees rodillas."
    }
];

/*
    lógica para decidir series / repeticiones / tiempo
*/
function getSetsReps(nivel, objetivo, tipoEjercicio){
    // nivel bajo = menos repeticiones, objetivo musculo = más series fuerza, etc.
    let baseSeries = 3;
    let baseReps = "12-15 repeticiones";
    let baseHold = "30-45 seg";

    if(nivel==="bajo"){
        baseSeries = 2;
        baseReps = "10-12 repeticiones";
        baseHold = "20-30 seg";
    } else if(nivel==="alto"){
        baseSeries = 4;
        baseReps = "15-20 repeticiones";
        baseHold = "45-60 seg";
    }

    // si el objetivo es "musculo", más series en fuerza
    if(objetivo==="musculo" && (tipoEjercicio==="piernas"||tipoEjercicio==="pecho"||tipoEjercicio==="espalda"||tipoEjercicio==="hombro"||tipoEjercicio==="brazo")){
        baseSeries += 1;
    }

    // si objetivo es "bajar grasa" o "resistencia", cardio más largo
    if((objetivo==="bajar grasa"||objetivo==="resistencia") && tipoEjercicio==="cardio"){
        baseHold = "40-60 seg ritmo constante";
    }

    // para core usamos hold en planchas
    if(tipoEjercicio==="core"){
        return {
            series: baseSeries,
            reps: baseHold
        };
    }

    // por defecto fuerza
    return {
        series: baseSeries,
        reps: baseReps
    };
}

/*
    Construir bloque visual
*/
function renderExerciseItem(ejercicio, config){
    return `
    <div class="exercise-item">
        <div class="exercise-img">
            <img src="${ejercicio.img}" alt="${ejercicio.nombre}" />
        </div>
        <div class="exercise-info">
            <div class="exercise-name">${ejercicio.nombre}</div>
            <div class="exercise-sets"><strong>${config.series} series</strong> · ${config.reps}</div>
            <div class="exercise-extra">${ejercicio.tips}</div>
        </div>
    </div>`;
}

function renderBlock(titulo, musculoLabel, ejerciciosHTML){
    return `
    <div class="routine-block">
        <h3>
            <span>${titulo}</span>
            <span class="routine-muscle">${musculoLabel}</span>
        </h3>
        <div class="exercise-list">
            ${ejerciciosHTML}
        </div>
    </div>`;
}

/*
    Generar rutina principal
*/
function generarRutina(data){
    // 1. Filtramos ejercicios según lugar principal
    const lugarPreferido = data.lugar === "mixto" ? "casa" : data.lugar; // si mixto, prioriza casa por seguridad
    const ejerciciosFiltrados = EXERCISES.filter(ex => ex.lugar === lugarPreferido || data.lugar==="mixto");

    // 2. Elegimos grupos principales:
    // Piernas/gluteos, Pecho/Tríceps, Espalda/Bíceps, Core/Abdomen, Cardio/Calentamiento
    const grupos = {
        piernas: ejerciciosFiltrados.filter(e=>e.tipo==="piernas").slice(0,2),
        pecho: ejerciciosFiltrados.filter(e=>e.tipo==="pecho").slice(0,1),
        espalda: ejerciciosFiltrados.filter(e=>e.tipo==="espalda").slice(0,1),
        core: ejerciciosFiltrados.filter(e=>e.tipo==="core").slice(0,2),
        cardio: ejerciciosFiltrados.filter(e=>e.tipo==="cardio").slice(0,1),
        brazo: ejerciciosFiltrados.filter(e=>e.tipo==="brazo").slice(0,1),
        hombro: ejerciciosFiltrados.filter(e=>e.tipo==="hombro").slice(0,1)
    };

    // 3. Armar bloques HTML dinámicamente
    let blocksHTML = "";

    // Piernas / glúteos
    if(grupos.piernas.length){
        let inner = "";
        grupos.piernas.forEach(ex=>{
            const cfg = getSetsReps(data.nivel, data.objetivo, ex.tipo);
            inner += renderExerciseItem(ex,cfg);
        });
        blocksHTML += renderBlock("Piernas & Glúteos", "Fuerza inferior", inner);
    }

    // Pecho / tríceps
    if(grupos.pecho.length){
        let inner = "";
        grupos.pecho.forEach(ex=>{
            const cfg = getSetsReps(data.nivel, data.objetivo, ex.tipo);
            inner += renderExerciseItem(ex,cfg);
        });
        // agregar tríceps silla si es casa o si no hay otra cosa
        if(grupos.brazo.length){
            grupos.brazo.forEach(ex=>{
                const cfg = getSetsReps(data.nivel, data.objetivo, ex.tipo);
                inner += renderExerciseItem(ex,cfg);
            });
        }
        blocksHTML += renderBlock("Pecho & Tríceps", "Empuje", inner);
    }

    // Espalda / bíceps / hombro
    if(grupos.espalda.length){
        let inner = "";
        grupos.espalda.forEach(ex=>{
            const cfg = getSetsReps(data.nivel, data.objetivo, ex.tipo);
            inner += renderExerciseItem(ex,cfg);
        });
        if(grupos.hombro.length){
            grupos.hombro.forEach(ex=>{
                const cfg = getSetsReps(data.nivel, data.objetivo, ex.tipo);
                inner += renderExerciseItem(ex,cfg);
            });
        }
        blocksHTML += renderBlock("Espalda & Hombros", "Tirón / Estabilidad", inner);
    }

    // Core
    if(grupos.core.length){
        let inner = "";
        grupos.core.forEach(ex=>{
            const cfg = getSetsReps(data.nivel, data.objetivo, ex.tipo);
            inner += renderExerciseItem(ex,cfg);
        });
        blocksHTML += renderBlock("Zona Media (Core)", "Abdomen / Lumbares", inner);
    }

    // Cardio / activación
    if(grupos.cardio.length){
        let inner = "";
        grupos.cardio.forEach(ex=>{
            const cfg = getSetsReps(data.nivel, data.objetivo, ex.tipo);
            inner += renderExerciseItem(ex,cfg);
        });
        blocksHTML += renderBlock("Cardio / Activación", "Resistencia / Quema grasa", inner);
    }

    // 4. Info meta
    const metaParts = [];
    metaParts.push(`${data.dias} días/semana`);
    metaParts.push(`${data.duracion} por sesión`);
    metaParts.push(`Objetivo: ${data.objetivo}`);
    metaParts.push(`Nivel: ${data.nivel}`);
    const metaString = metaParts.join(" • ");

    // 5. Poner todo en la página
    document.getElementById("chipLugar").textContent = data.lugar.toUpperCase();
    document.getElementById("routineMeta").textContent = metaString;
    document.getElementById("routineBlocks").innerHTML = blocksHTML;

    // 6. Advertencia si hay lesiones o condiciones
    const showAlerta =
        (data.lesiones && data.lesiones.trim().toLowerCase() !== "ninguna") ||
        (data.condicion && data.condicion.trim().toLowerCase() !== "ninguna");
    document.getElementById("alertaLesion").style.display = showAlerta ? "block" : "none";

    // mostrar sección rutina
    document.getElementById("routineSection").style.display = "block";

    // scroll suave hacia la rutina
    document.getElementById("routineSection").scrollIntoView({behavior:"smooth"});
}

/*
    Capturar datos del formulario y llamar a generarRutina()
*/
document.getElementById("generarBtn").addEventListener("click", ()=>{
    const data = {
        genero: document.getElementById("genero").value,
        edad: document.getElementById("edad").value,
        peso: document.getElementById("peso").value,
        altura: document.getElementById("altura").value,
        objetivo: document.getElementById("objetivo").value,
        lesiones: document.getElementById("lesiones").value,
        condicion: document.getElementById("condicion").value,
        tiempoSinEntrenar: document.getElementById("tiempoSinEntrenar").value,
        nivel: document.getElementById("nivel").value,
        dias: document.getElementById("dias").value,
        duracion: document.getElementById("duracion").value,
        horario: document.getElementById("horario").value,
        lugar: document.getElementById("lugar").value,
        espacio: document.getElementById("espacio").value,
        equipo: document.getElementById("equipo").value,
        preferencia: document.getElementById("preferencia").value,
        experiencia: document.getElementById("experiencia").value,
        motivacion: document.getElementById("motivacion").value,
        intensidad: document.getElementById("intensidad").value,
        acompanamiento: document.getElementById("acompanamiento").value,
        plazo: document.getElementById("plazo").value,
        seguimiento: document.getElementById("seguimiento").value,
        motivacionEspecial: document.getElementById("motivacionEspecial").value
    };

    // validaciones mínimas
    if(!data.genero || !data.edad || !data.peso || !data.altura || !data.objetivo || !data.nivel || !data.dias || !data.duracion || !data.horario || !data.lugar){
        alert("Por favor completa los campos obligatorios marcados (listas principales).");
        return;
    }

    generarRutina(data);
});
</script>
</body>
</html>

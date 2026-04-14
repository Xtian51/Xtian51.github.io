<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Semana 10 — ViewModel + LiveData · Android Studio + Kotlin</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Playfair+Display:wght@700;900&family=Source+Sans+3:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #faf9f7;
    --bg2: #f2f0ec;
    --surface: #ffffff;
    --surface2: #f7f5f2;
    --border: #e0dbd3;
    --border2: #cdc8bf;
    --accent: #7c3aed;
    --accent2: #059669;
    --accent3: #dc2626;
    --accent4: #d97706;
    --text: #1c1917;
    --text-dim: #57534e;
    --text-muted: #a8a29e;
    --kotlin: #7f52ff;
    --xml: #c2410c;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Source Sans 3', sans-serif;
    font-weight: 300;
    line-height: 1.75;
  }

  /* ── HERO ── */
  .hero {
    background: var(--text);
    padding: 56px 48px 48px;
    position: relative;
    overflow: hidden;
  }
  .hero::after {
    content: 'MVVM';
    position: absolute;
    bottom: -30px; right: -10px;
    font-family: 'Playfair Display', serif;
    font-size: 180px;
    font-weight: 900;
    color: rgba(255,255,255,0.04);
    line-height: 1;
    pointer-events: none;
    user-select: none;
  }

  .week-tag {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    border: 1px solid rgba(124,58,237,0.4);
    background: rgba(124,58,237,0.1);
    color: #c4b5fd;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    padding: 5px 14px;
    border-radius: 20px;
    margin-bottom: 20px;
    width: fit-content;
  }

  .hero h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.4rem, 6vw, 4.2rem);
    font-weight: 900;
    color: #fff;
    line-height: 1.05;
    margin-bottom: 8px;
  }
  .hero h1 span { color: #c4b5fd; }

  .hero-sub {
    color: #a8a29e;
    font-size: 1rem;
    max-width: 600px;
    margin-bottom: 32px;
    line-height: 1.65;
  }

  .meta-strip {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
    border-top: 1px solid rgba(255,255,255,0.08);
    padding-top: 24px;
  }
  .meta-chip {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: #78716c;
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .meta-chip strong { color: #d6d3d1; font-weight: 600; }

  /* ── LAYOUT ── */
  .container { max-width: 980px; margin: 0 auto; padding: 0 28px 100px; }

  /* ── CLASE HEADER ── */
  .clase-header {
    margin: 60px 0 28px;
    padding-bottom: 16px;
    border-bottom: 2px solid var(--border);
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    gap: 16px;
  }
  .clase-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.8rem;
    font-weight: 700;
    color: var(--text);
    line-height: 1.15;
  }
  .clase-title span { color: var(--accent); }
  .clase-badge {
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    background: var(--accent);
    color: #fff;
    padding: 5px 14px;
    border-radius: 4px;
    white-space: nowrap;
    flex-shrink: 0;
  }

  /* ── OBJETIVO ── */
  .objetivo {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-left: 4px solid var(--accent2);
    border-radius: 6px;
    padding: 16px 20px;
    margin-bottom: 30px;
    font-size: 0.9rem;
  }
  .objetivo strong {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--accent2);
    display: block;
    margin-bottom: 5px;
  }
  .objetivo p { margin: 0; color: var(--text-dim); }

  /* ── SECTION ── */
  .section { margin-bottom: 38px; }
  .section-title {
    font-family: 'Source Sans 3', sans-serif;
    font-size: 0.95rem;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 14px;
    display: flex;
    align-items: center;
    gap: 10px;
    text-transform: uppercase;
    letter-spacing: 0.06em;
  }
  .section-title .tag {
    background: var(--text);
    color: var(--bg);
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    font-weight: 700;
    padding: 2px 8px;
    border-radius: 3px;
  }
  .section-title .tag.kotlin { background: var(--kotlin); color: #fff; }
  .section-title .tag.xml    { background: var(--xml); color: #fff; }

  p { margin-bottom: 12px; color: var(--text-dim); font-size: 0.93rem; }

  /* ── MVVM DIAGRAM ── */
  .mvvm-diagram {
    display: grid;
    grid-template-columns: 1fr auto 1fr auto 1fr;
    align-items: center;
    gap: 0;
    margin: 20px 0;
    background: var(--text);
    border-radius: 12px;
    padding: 28px 24px;
  }
  .mvvm-box {
    border-radius: 8px;
    padding: 18px 14px;
    text-align: center;
  }
  .mvvm-box .layer-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    margin-bottom: 8px;
    display: block;
  }
  .mvvm-box h4 {
    font-family: 'Playfair Display', serif;
    font-size: 1.1rem;
    font-weight: 700;
    margin-bottom: 6px;
  }
  .mvvm-box p { font-size: 0.78rem; margin: 0; line-height: 1.5; }

  .box-view     { background: rgba(124,58,237,0.15); border: 1px solid rgba(124,58,237,0.3); }
  .box-view     .layer-label { color: #c4b5fd; }
  .box-view     h4, .box-view p { color: #e9d5ff; }

  .box-vm       { background: rgba(5,150,105,0.15); border: 1px solid rgba(5,150,105,0.3); }
  .box-vm       .layer-label { color: #6ee7b7; }
  .box-vm       h4, .box-vm p { color: #a7f3d0; }

  .box-model    { background: rgba(217,119,6,0.15); border: 1px solid rgba(217,119,6,0.3); }
  .box-model    .layer-label { color: #fcd34d; }
  .box-model    h4, .box-model p { color: #fde68a; }

  .mvvm-arrow {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
    padding: 0 12px;
  }
  .mvvm-arrow .line {
    width: 40px;
    height: 1px;
    background: rgba(255,255,255,0.2);
    position: relative;
  }
  .mvvm-arrow .arrow-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 8px;
    color: rgba(255,255,255,0.3);
    letter-spacing: 0.08em;
    text-align: center;
    white-space: nowrap;
  }

  /* ── CONCEPTS GRID ── */
  .concepts {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
    gap: 12px;
    margin: 18px 0;
  }
  .concept-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 16px;
    border-top: 3px solid var(--accent);
  }
  .concept-card.green { border-top-color: var(--accent2); }
  .concept-card.orange { border-top-color: var(--accent4); }
  .concept-card .icon { font-size: 1.3rem; margin-bottom: 8px; }
  .concept-card h4 {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.78rem;
    color: var(--accent);
    margin-bottom: 5px;
    font-weight: 700;
  }
  .concept-card.green h4 { color: var(--accent2); }
  .concept-card.orange h4 { color: var(--accent4); }
  .concept-card p { font-size: 0.82rem; margin: 0; }

  /* ── CODE BLOCK ── */
  .code-block {
    background: #1c1917;
    border: 1px solid #2d2825;
    border-radius: 8px;
    overflow: hidden;
    margin: 18px 0;
    font-size: 0.84rem;
  }
  .code-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 9px 16px;
    background: #252220;
    border-bottom: 1px solid #2d2825;
  }
  .code-lang {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    padding: 2px 9px;
    border-radius: 3px;
  }
  .lang-kotlin { background: rgba(127,82,255,0.2); color: #b08fff; border: 1px solid rgba(127,82,255,0.3); }
  .lang-xml    { background: rgba(194,65,12,0.2);  color: #fb923c; border: 1px solid rgba(194,65,12,0.3); }
  .lang-gradle { background: rgba(5,150,105,0.2);  color: #6ee7b7; border: 1px solid rgba(5,150,105,0.3); }
  .code-filename { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #57534e; }
  .code-body { padding: 18px 20px; overflow-x: auto; }
  pre {
    font-family: 'JetBrains Mono', monospace;
    line-height: 1.65;
    white-space: pre;
    color: #d6d3d1;
    background: transparent;
  }

  .kw  { color: #c792ea; }
  .fn  { color: #82aaff; }
  .str { color: #c3e88d; }
  .cm  { color: #4a4541; font-style: italic; }
  .num { color: #f78c6c; }
  .cls { color: #ffcb6b; }
  .op  { color: #89ddff; }
  .tag { color: #e06c75; }
  .attr{ color: #c3e88d; }
  .val { color: #f78c6c; }
  .an  { color: #89ddff; }

  /* ── ALERT ── */
  .alert {
    border-radius: 6px;
    padding: 13px 17px;
    margin: 14px 0;
    font-size: 0.87rem;
    display: flex;
    gap: 12px;
    align-items: flex-start;
  }
  .alert-purple { background: rgba(124,58,237,0.06); border: 1px solid rgba(124,58,237,0.2); }
  .alert-green  { background: rgba(5,150,105,0.06);  border: 1px solid rgba(5,150,105,0.2); }
  .alert-red    { background: rgba(220,38,38,0.06);  border: 1px solid rgba(220,38,38,0.2); }
  .alert-orange { background: rgba(217,119,6,0.06);  border: 1px solid rgba(217,119,6,0.2); }
  .alert-icon { font-size: 1.1rem; flex-shrink: 0; margin-top: 1px; }
  .alert p { margin: 0; }

  /* ── DIVIDER ── */
  .divider {
    margin: 56px 0 0;
    height: 1px;
    background: linear-gradient(to right, var(--accent), var(--border), transparent);
  }

  /* ── TAREA ── */
  .tarea {
    background: var(--text);
    border-radius: 12px;
    padding: 36px;
    margin-top: 56px;
    color: #fff;
    position: relative;
    overflow: hidden;
  }
  .tarea::before {
    content: '';
    position: absolute;
    top: -60px; right: -60px;
    width: 300px; height: 300px;
    background: radial-gradient(circle, rgba(124,58,237,0.15) 0%, transparent 70%);
    pointer-events: none;
  }
  .tarea-badge {
    display: inline-block;
    background: var(--accent);
    color: #fff;
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    padding: 4px 12px;
    border-radius: 3px;
    margin-bottom: 14px;
  }
  .tarea h2 {
    font-family: 'Playfair Display', serif;
    font-size: 1.9rem;
    font-weight: 900;
    margin-bottom: 10px;
  }
  .tarea-desc { color: #a8a29e; margin-bottom: 22px; font-size: 0.93rem; }
  .reqs { display: flex; flex-direction: column; gap: 11px; margin-bottom: 24px; }
  .req { display: flex; gap: 12px; align-items: flex-start; font-size: 0.89rem; color: #d6d3d1; }
  .req-num {
    min-width: 22px; height: 22px;
    background: var(--accent);
    color: #fff;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    border-radius: 3px;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0; margin-top: 2px;
  }
  .req-num.star { background: var(--accent2); }
  .entrega {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 6px;
    padding: 13px 17px;
    font-size: 0.84rem;
  }
  .entrega strong {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    color: #c4b5fd;
    text-transform: uppercase;
    letter-spacing: 0.12em;
    display: block;
    margin-bottom: 4px;
  }
  .entrega p { color: #78716c; margin: 0; }

  ::-webkit-scrollbar { width: 5px; height: 5px; }
  ::-webkit-scrollbar-track { background: #1c1917; }
  ::-webkit-scrollbar-thumb { background: #44403c; border-radius: 3px; }
</style>
</head>
<body>

<!-- HERO -->
<div class="hero">
  <div class="week-tag">📅 Semana 10 de 16</div>
  <h1>ViewModel<br><span>+ LiveData</span></h1>
  <p class="hero-sub">Separa la lógica de la UI con el patrón MVVM. Tus datos sobreviven la rotación de pantalla y la interfaz reacciona automáticamente a los cambios.</p>
  <div class="meta-strip">
    <div class="meta-chip">Clases <strong>2 × 2 hrs</strong></div>
    <div class="meta-chip">Lenguaje <strong>Kotlin</strong></div>
    <div class="meta-chip">Layout <strong>ConstraintLayout</strong></div>
    <div class="meta-chip">Prereq <strong>Semanas 7, 8 y 9</strong></div>
  </div>
</div>

<div class="container">

  <!-- ══════════════════ CLASE 1 ══════════════════ -->
  <div class="clase-header">
    <div class="clase-title">El problema del <span>estado en rotación</span></div>
    <span class="clase-badge">Clase 01</span>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Entender por qué los datos se pierden al rotar la pantalla, qué es el patrón MVVM y cómo ViewModel resuelve este problema. Construir un primer ejemplo funcional.</p>
  </div>

  <!-- Concepto: el problema -->
  <div class="section">
    <div class="section-title"><span class="tag">CONCEPTO</span> ¿Por qué necesitamos ViewModel?</div>
    <p>Cuando el usuario rota el dispositivo, Android <strong>destruye y recrea</strong> la Activity completa. Todo lo que guardaste en variables de instancia se pierde. El ViewModel resuelve esto al vivir fuera del ciclo de vida de la Activity.</p>

    <div class="concepts">
      <div class="concept-card">
        <div class="icon">💀</div>
        <h4>Sin ViewModel</h4>
        <p>Variables en Activity → rotación → Activity destruida → datos perdidos → el usuario pierde su progreso.</p>
      </div>
      <div class="concept-card green">
        <div class="icon">🧠</div>
        <h4>ViewModel</h4>
        <p>Almacena y gestiona datos de UI. Sobrevive a rotaciones. Se destruye solo cuando la Activity termina definitivamente.</p>
      </div>
      <div class="concept-card orange">
        <div class="icon">👁️</div>
        <h4>LiveData</h4>
        <p>Dato observable. Notifica automáticamente a los observers cuando su valor cambia. Solo emite si el observer está activo.</p>
      </div>
    </div>
  </div>

  <!-- Diagrama MVVM -->
  <div class="section">
    <div class="section-title"><span class="tag">CONCEPTO</span> Arquitectura MVVM</div>
    <div class="mvvm-diagram">
      <div class="mvvm-box box-view">
        <span class="layer-label">Vista</span>
        <h4>View</h4>
        <p>Activity / Fragment<br>Solo muestra datos.<br>No contiene lógica.</p>
      </div>
      <div class="mvvm-arrow">
        <div class="line"></div>
        <div class="arrow-label">observa<br>LiveData</div>
        <div class="line"></div>
        <div class="arrow-label">llama<br>métodos</div>
      </div>
      <div class="mvvm-box box-vm">
        <span class="layer-label">Vista-Modelo</span>
        <h4>ViewModel</h4>
        <p>Lógica de UI.<br>Expone LiveData.<br>Sobrevive rotación.</p>
      </div>
      <div class="mvvm-arrow">
        <div class="line"></div>
        <div class="arrow-label">obtiene<br>datos</div>
        <div class="line"></div>
        <div class="arrow-label">retorna<br>resultados</div>
      </div>
      <div class="mvvm-box box-model">
        <span class="layer-label">Modelo</span>
        <h4>Model</h4>
        <p>Datos / Repositorio.<br>Room, API REST,<br>SharedPreferences.</p>
      </div>
    </div>
  </div>

  <!-- Código 1: build.gradle -->
  <div class="section">
    <div class="section-title"><span class="tag">GRADLE</span> Código 1 — Dependencias</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-gradle">Gradle · Kotlin DSL</span>
        <span class="code-filename">build.gradle.kts (Module)</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="fn">dependencies</span> {
    <span class="cm">// ViewModel y LiveData (Lifecycle)</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.lifecycle:lifecycle-livedata-ktx:2.7.0"</span>)

    <span class="cm">// Activity KTX — habilita viewModels() delegate en Activity</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.activity:activity-ktx:1.9.0"</span>)

    <span class="cm">// Fragment KTX — habilita viewModels() y activityViewModels() en Fragment</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.fragment:fragment-ktx:1.7.0"</span>)

    <span class="cm">// Core KTX — habilita addTextChangedListener y otras extensiones</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.core:core-ktx:1.13.0"</span>)
}</pre></div>
    </div>
  </div>

  <!-- Código 2: activity_contador.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 2 — Layout del Contador</div>
    <p>Ejemplo base: un contador que <strong>no pierde su valor al rotar</strong> la pantalla.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_contador.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"24dp"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvContador"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"0"</span>
        <span class="attr">android:textSize</span>=<span class="val">"72sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toTopOf</span>=<span class="val">"@id/btnIncrementar"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnIncrementar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"+ Incrementar"</span>
        <span class="attr">android:layout_marginBottom</span>=<span class="val">"12dp"</span>
        <span class="attr">app:layout_constraintBottom_toTopOf</span>=<span class="val">"@id/btnDecrementar"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnDecrementar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"− Decrementar"</span>
        <span class="attr">android:layout_marginBottom</span>=<span class="val">"12dp"</span>
        <span class="attr">app:layout_constraintBottom_toTopOf</span>=<span class="val">"@id/btnReset"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnReset"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Resetear"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 3: ContadorViewModel.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 3 — ContadorViewModel.kt</div>
    <p>El ViewModel expone los datos como <code>LiveData</code> y contiene toda la lógica. La Activity no sabe cómo se calcula el contador, solo lo observa.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">ContadorViewModel.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.lifecycle.LiveData
<span class="kw">import</span> androidx.lifecycle.MutableLiveData
<span class="kw">import</span> androidx.lifecycle.ViewModel

<span class="kw">class</span> <span class="cls">ContadorViewModel</span> : <span class="cls">ViewModel</span>() {

    <span class="cm">// MutableLiveData: puede cambiar su valor — solo visible dentro del ViewModel</span>
    <span class="kw">private val</span> _contador = <span class="cls">MutableLiveData</span>&lt;<span class="cls">Int</span>&gt;(<span class="num">0</span>)

    <span class="cm">// LiveData (inmutable): lo que expone la Activity — solo puede leer, no modificar</span>
    <span class="kw">val</span> contador: <span class="cls">LiveData</span>&lt;<span class="cls">Int</span>&gt; = _contador

    <span class="cm">// Lógica del negocio — la Activity solo llama estos métodos</span>
    <span class="kw">fun</span> <span class="fn">incrementar</span>() {
        _contador.value = (_contador.value <span class="op">?:</span> <span class="num">0</span>) + <span class="num">1</span>
    }

    <span class="kw">fun</span> <span class="fn">decrementar</span>() {
        _contador.value = (_contador.value <span class="op">?:</span> <span class="num">0</span>) - <span class="num">1</span>
    }

    <span class="kw">fun</span> <span class="fn">resetear</span>() {
        _contador.value = <span class="num">0</span>
    }
}</pre></div>
    </div>
    <div class="alert alert-purple">
      <span class="alert-icon">💡</span>
      <p><strong>Convención de nombres:</strong> el prefijo <code>_</code> en <code>_contador</code> indica que es privado y mutable. Se expone públicamente como <code>contador</code> de tipo <code>LiveData</code> (solo lectura). Este patrón es estándar en todo proyecto Android profesional.</p>
    </div>
  </div>

  <!-- Código 4: ContadorActivity.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 4 — ContadorActivity.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">ContadorActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.activity.viewModels

<span class="kw">class</span> <span class="cls">ContadorActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="cm">// Delegate viewModels(): obtiene o crea el ViewModel asociado a esta Activity.
    // Si la Activity se recrea por rotación, recupera el MISMO ViewModel existente.</span>
    <span class="kw">private val</span> viewModel: <span class="cls">ContadorViewModel</span> <span class="kw">by</span> <span class="fn">viewModels</span>()

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_contador)

        <span class="kw">val</span> tvContador    = <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvContador)
        <span class="kw">val</span> btnIncrementar = <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnIncrementar)
        <span class="kw">val</span> btnDecrementar = <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnDecrementar)
        <span class="kw">val</span> btnReset       = <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnReset)

        <span class="cm">// Observar el LiveData: cada vez que _contador cambie, este bloque se ejecuta</span>
        viewModel.contador.<span class="fn">observe</span>(<span class="kw">this</span>) { nuevoValor <span class="op">-&gt;</span>
            tvContador.text = nuevoValor.toString()
        }

        <span class="cm">// La Activity solo delega al ViewModel — no maneja lógica aquí</span>
        btnIncrementar.<span class="fn">setOnClickListener</span> { viewModel.<span class="fn">incrementar</span>() }
        btnDecrementar.<span class="fn">setOnClickListener</span> { viewModel.<span class="fn">decrementar</span>() }
        btnReset.<span class="fn">setOnClickListener</span>       { viewModel.<span class="fn">resetear</span>() }
    }
}</pre></div>
    </div>
    <div class="alert alert-green">
      <span class="alert-icon">🔄</span>
      <p><strong>Prueba en clase:</strong> Incrementar el contador a 10, luego rotar el emulador (Ctrl+F11). El valor <strong>no se pierde</strong>. Comparar con una versión sin ViewModel donde la variable vive en la Activity — el contraste es inmediato y muy didáctico.</p>
    </div>
  </div>

  <!-- Código 5: AndroidManifest -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 5 — AndroidManifest.xml</div>
    <p>Toda Activity debe estar declarada en el Manifest. Si <code>ContadorActivity</code> es la principal, se declara con el intent-filter. Si <code>TareasActivity</code> es secundaria, se declara sin él.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">app/src/main/AndroidManifest.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;manifest</span> <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;application</span>
        <span class="attr">android:allowBackup</span>=<span class="val">"true"</span>
        <span class="attr">android:theme</span>=<span class="val">"@style/Theme.AppCompat.Light.DarkActionBar"</span><span class="tag">&gt;</span>

        <span class="cm">&lt;!-- Activity principal (Clase 1) --&gt;</span>
        <span class="tag">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".ContadorActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"true"</span><span class="tag">&gt;</span>
            <span class="tag">&lt;intent-filter&gt;</span>
                <span class="tag">&lt;action</span> <span class="attr">android:name</span>=<span class="val">"android.intent.action.MAIN"</span> <span class="tag">/&gt;</span>
                <span class="tag">&lt;category</span> <span class="attr">android:name</span>=<span class="val">"android.intent.category.LAUNCHER"</span> <span class="tag">/&gt;</span>
            <span class="tag">&lt;/intent-filter&gt;</span>
        <span class="tag">&lt;/activity&gt;</span>

        <span class="cm">&lt;!-- Activity secundaria (Clase 2) --&gt;</span>
        <span class="tag">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".TareasActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"false"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;/application&gt;</span>

<span class="tag">&lt;/manifest&gt;</span></pre></div>
    </div>
    <div class="alert alert-orange">
      <span class="alert-icon">⚠️</span>
      <p><strong>android:exported</strong> es obligatorio desde Android 12 (API 31). La Activity principal debe tener <code>exported="true"</code> porque el sistema necesita lanzarla. Las Activities secundarias usan <code>exported="false"</code> ya que solo se abren desde dentro de la misma app.</p>
    </div>
  </div>

  <!-- ══════════════════ CLASE 2 ══════════════════ -->
  <div class="divider"></div>

  <div class="clase-header">
    <div class="clase-title">LiveData con <span>listas y formularios</span></div>
    <span class="clase-badge">Clase 02</span>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Usar ViewModel y LiveData con datos más complejos: una lista observable que alimenta un RecyclerView y un formulario cuyos valores persisten durante la rotación.</p>
  </div>

  <!-- Código 6: Tarea.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 6 — Data class Tarea</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">Tarea.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">data class</span> <span class="cls">Tarea</span>(
    <span class="kw">val</span> id:          <span class="cls">Int</span>,
    <span class="kw">val</span> titulo:      <span class="cls">String</span>,
    <span class="kw">val</span> completada:  <span class="cls">Boolean</span> = <span class="kw">false</span>
)</pre></div>
    </div>
  </div>

  <!-- Código 7: TareasViewModel.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 7 — TareasViewModel.kt</div>
    <p>Cuando el LiveData contiene una lista, hay que reasignar la referencia completa para que los observers sean notificados. No basta con modificar la lista internamente.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">TareasViewModel.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.lifecycle.LiveData
<span class="kw">import</span> androidx.lifecycle.MutableLiveData
<span class="kw">import</span> androidx.lifecycle.ViewModel

<span class="kw">class</span> <span class="cls">TareasViewModel</span> : <span class="cls">ViewModel</span>() {

    <span class="kw">private val</span> _tareas = <span class="cls">MutableLiveData</span>&lt;<span class="cls">List</span>&lt;<span class="cls">Tarea</span>&gt;&gt;(<span class="fn">emptyList</span>())
    <span class="kw">val</span> tareas: <span class="cls">LiveData</span>&lt;<span class="cls">List</span>&lt;<span class="cls">Tarea</span>&gt;&gt; = _tareas

    <span class="kw">private val</span> _textoInput = <span class="cls">MutableLiveData</span>&lt;<span class="cls">String</span>&gt;(<span class="str">""</span>)
    <span class="kw">val</span> textoInput: <span class="cls">LiveData</span>&lt;<span class="cls">String</span>&gt; = _textoInput

    <span class="kw">private var</span> nextId = <span class="num">1</span>

    <span class="kw">fun</span> <span class="fn">agregarTarea</span>(titulo: <span class="cls">String</span>) {
        <span class="kw">if</span> (titulo.<span class="fn">isBlank</span>()) <span class="kw">return</span>
        <span class="cm">// Crear lista nueva con la tarea añadida — LiveData detecta el cambio</span>
        <span class="kw">val</span> listaActual = _tareas.value.<span class="fn">orEmpty</span>()
        _tareas.value = listaActual + <span class="cls">Tarea</span>(id = nextId++, titulo = titulo)
        _textoInput.value = <span class="str">""</span>  <span class="cm">// Limpiar el campo después de agregar</span>
    }

    <span class="kw">fun</span> <span class="fn">toggleCompletada</span>(tarea: <span class="cls">Tarea</span>) {
        <span class="cm">// Mapear la lista: invertir solo la tarea que coincide con el id</span>
        _tareas.value = _tareas.value.<span class="fn">orEmpty</span>().<span class="fn">map</span> {
            <span class="kw">if</span> (it.id == tarea.id) it.<span class="fn">copy</span>(completada = <span class="op">!</span>it.completada) <span class="kw">else</span> it
        }
    }

    <span class="kw">fun</span> <span class="fn">eliminarTarea</span>(tarea: <span class="cls">Tarea</span>) {
        _tareas.value = _tareas.value.<span class="fn">orEmpty</span>().<span class="fn">filter</span> { it.id <span class="op">!=</span> tarea.id }
    }

    <span class="kw">fun</span> <span class="fn">actualizarTextoInput</span>(texto: <span class="cls">String</span>) {
        _textoInput.value = texto
    }
}</pre></div>
    </div>
    <div class="alert alert-orange">
      <span class="alert-icon">⚠️</span>
      <p><strong>Error común:</strong> Hacer <code>_tareas.value?.add(nuevaTarea)</code> modifica la lista en memoria pero <strong>no notifica</strong> a los observers porque la referencia del LiveData no cambia. Siempre reasignar: <code>_tareas.value = listaActual + nuevaTarea</code>.</p>
    </div>
  </div>

  <!-- Código 8: item_tarea.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 8 — Layout del ítem de tarea</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/item_tarea.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
    <span class="attr">android:padding</span>=<span class="val">"12dp"</span>
    <span class="attr">android:background</span>=<span class="val">"?attr/selectableItemBackground"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;CheckBox</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/checkTarea"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvTituloTarea"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"16sp"</span>
        <span class="attr">android:layout_marginStart</span>=<span class="val">"8dp"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toEndOf</span>=<span class="val">"@id/checkTarea"</span>
        <span class="attr">app:layout_constraintEnd_toStartOf</span>=<span class="val">"@id/btnEliminar"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnEliminar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"✕"</span>
        <span class="attr">android:textSize</span>=<span class="val">"12sp"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 9: TareaAdapter.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 9 — TareaAdapter.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">TareaAdapter.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> android.graphics.Paint
<span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.CheckBox
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">TareaAdapter</span>(
    <span class="kw">private var</span> tareas: <span class="cls">List</span>&lt;<span class="cls">Tarea</span>&gt; = <span class="fn">emptyList</span>(),
    <span class="kw">private val</span> onToggle:  (<span class="cls">Tarea</span>) <span class="op">-&gt;</span> <span class="cls">Unit</span>,
    <span class="kw">private val</span> onEliminar: (<span class="cls">Tarea</span>) <span class="op">-&gt;</span> <span class="cls">Unit</span>
) : <span class="cls">RecyclerView</span>.<span class="cls">Adapter</span>&lt;<span class="cls">TareaAdapter</span>.<span class="cls">TareaViewHolder</span>&gt;() {

    <span class="kw">inner class</span> <span class="cls">TareaViewHolder</span>(itemView: <span class="cls">View</span>) : <span class="cls">RecyclerView</span>.<span class="cls">ViewHolder</span>(itemView) {
        <span class="kw">val</span> check:     <span class="cls">CheckBox</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.checkTarea)
        <span class="kw">val</span> tvTitulo:  <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvTituloTarea)
        <span class="kw">val</span> btnElim:   <span class="cls">Button</span>   = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.btnEliminar)
    }

    <span class="kw">override fun</span> <span class="fn">onCreateViewHolder</span>(parent: <span class="cls">ViewGroup</span>, viewType: <span class="cls">Int</span>) =
        <span class="cls">TareaViewHolder</span>(
            <span class="cls">LayoutInflater</span>.<span class="fn">from</span>(parent.context)
                .<span class="fn">inflate</span>(<span class="cls">R</span>.layout.item_tarea, parent, <span class="kw">false</span>)
        )

    <span class="kw">override fun</span> <span class="fn">onBindViewHolder</span>(holder: <span class="cls">TareaViewHolder</span>, position: <span class="cls">Int</span>) {
        <span class="kw">val</span> tarea = tareas[position]

        holder.tvTitulo.text = tarea.titulo
        holder.check.isChecked = tarea.completada

        <span class="cm">// Texto tachado si la tarea está completada</span>
        <span class="kw">val</span> flag = <span class="kw">if</span> (tarea.completada)
            holder.tvTitulo.paintFlags <span class="op">or</span> <span class="cls">Paint</span>.STRIKE_THRU_TEXT_FLAG
        <span class="kw">else</span>
            holder.tvTitulo.paintFlags <span class="op">and</span> <span class="cls">Paint</span>.STRIKE_THRU_TEXT_FLAG.<span class="fn">inv</span>()
        holder.tvTitulo.paintFlags = flag

        <span class="cm">// Evitar disparar el listener al hacer bind</span>
        holder.check.<span class="fn">setOnCheckedChangeListener</span>(<span class="kw">null</span>)
        holder.check.<span class="fn">setOnCheckedChangeListener</span> { _, _ <span class="op">-&gt;</span> <span class="fn">onToggle</span>(tarea) }
        holder.btnElim.<span class="fn">setOnClickListener</span> { <span class="fn">onEliminar</span>(tarea) }
    }

    <span class="kw">override fun</span> <span class="fn">getItemCount</span>() = tareas.size

    <span class="cm">// Método para actualizar la lista desde el observer de LiveData</span>
    <span class="kw">fun</span> <span class="fn">actualizarLista</span>(nuevaLista: <span class="cls">List</span>&lt;<span class="cls">Tarea</span>&gt;) {
        tareas = nuevaLista
        <span class="fn">notifyDataSetChanged</span>()
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 10: activity_tareas.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 10 — Layout de TareasActivity</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_tareas.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;EditText</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/etNuevaTarea"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:hint</span>=<span class="val">"Nueva tarea..."</span>
        <span class="attr">android:padding</span>=<span class="val">"12dp"</span>
        <span class="attr">android:inputType</span>=<span class="val">"textCapSentences"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toStartOf</span>=<span class="val">"@id/btnAgregar"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnAgregar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Agregar"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBaseline_toBaselineOf</span>=<span class="val">"@id/etNuevaTarea"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvContadorTareas"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">android:textSize</span>=<span class="val">"13sp"</span>
        <span class="attr">android:textColor</span>=<span class="val">"#888"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/etNuevaTarea"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;androidx.recyclerview.widget.RecyclerView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/recyclerTareas"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">android:clipToPadding</span>=<span class="val">"false"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvContadorTareas"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 11: TareasActivity.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 11 — TareasActivity.kt</div>
    <p>La Activity observa <strong>dos</strong> LiveData: la lista de tareas y el texto del campo de entrada. Esto permite que el contenido del EditText también sobreviva la rotación.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">TareasActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.EditText
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.activity.viewModels
<span class="kw">import</span> androidx.core.widget.addTextChangedListener
<span class="kw">import</span> androidx.recyclerview.widget.LinearLayoutManager
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">TareasActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">private val</span> viewModel: <span class="cls">TareasViewModel</span> <span class="kw">by</span> <span class="fn">viewModels</span>()

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_tareas)

        <span class="kw">val</span> etNuevaTarea      = <span class="fn">findViewById</span>&lt;<span class="cls">EditText</span>&gt;(<span class="cls">R</span>.id.etNuevaTarea)
        <span class="kw">val</span> btnAgregar        = <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnAgregar)
        <span class="kw">val</span> tvContadorTareas  = <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvContadorTareas)
        <span class="kw">val</span> recyclerView      = <span class="fn">findViewById</span>&lt;<span class="cls">RecyclerView</span>&gt;(<span class="cls">R</span>.id.recyclerTareas)

        <span class="cm">// Configurar RecyclerView</span>
        <span class="kw">val</span> adapter = <span class="cls">TareaAdapter</span>(
            onToggle   = { tarea <span class="op">-&gt;</span> viewModel.<span class="fn">toggleCompletada</span>(tarea) },
            onEliminar = { tarea <span class="op">-&gt;</span> viewModel.<span class="fn">eliminarTarea</span>(tarea) }
        )
        recyclerView.layoutManager = <span class="cls">LinearLayoutManager</span>(<span class="kw">this</span>)
        recyclerView.adapter = adapter

        <span class="cm">// Observer 1: actualizar RecyclerView y contador cuando cambia la lista</span>
        viewModel.tareas.<span class="fn">observe</span>(<span class="kw">this</span>) { lista <span class="op">-&gt;</span>
            adapter.<span class="fn">actualizarLista</span>(lista)
            <span class="kw">val</span> completadas = lista.<span class="fn">count</span> { it.completada }
            tvContadorTareas.text = <span class="str">"${lista.size} tareas · $completadas completadas"</span>
        }

        <span class="cm">// Observer 2: mantener el EditText sincronizado con el ViewModel</span>
        viewModel.textoInput.<span class="fn">observe</span>(<span class="kw">this</span>) { texto <span class="op">-&gt;</span>
            <span class="kw">if</span> (etNuevaTarea.text.toString() <span class="op">!=</span> texto) {
                etNuevaTarea.<span class="fn">setText</span>(texto)
                etNuevaTarea.<span class="fn">setSelection</span>(texto.length)
            }
        }

        <span class="cm">// Notificar al ViewModel cada vez que el usuario escribe</span>
        etNuevaTarea.<span class="fn">addTextChangedListener</span> { editable <span class="op">-&gt;</span>
            viewModel.<span class="fn">actualizarTextoInput</span>(editable.toString())
        }

        btnAgregar.<span class="fn">setOnClickListener</span> {
            viewModel.<span class="fn">agregarTarea</span>(etNuevaTarea.text.toString())
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-purple">
      <span class="alert-icon">💡</span>
      <p><strong>Punto de discusión:</strong> ¿Por qué la condición <code>if (etNuevaTarea.text.toString() != texto)</code> antes de llamar <code>setText()</code>? Sin ella, el observer y el <code>addTextChangedListener</code> entran en un loop infinito: el observer escribe → el listener dispara → el ViewModel actualiza → el observer escribe…</p>
    </div>
    <div class="alert alert-green">
      <span class="alert-icon">🔗</span>
      <p><strong>Conexión con semanas anteriores:</strong> El mismo <code>TareasViewModel</code> puede usarse dentro de un Fragment (Semana 9). En ese caso, usar <code>viewModels()</code> dentro del Fragment da una instancia por Fragment, mientras que <code>activityViewModels()</code> comparte el mismo ViewModel entre todos los Fragments de la Activity.</p>
    </div>
  </div>

  <!-- Código 12: ViewModel en Fragment -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 12 — ViewModel desde un Fragment</div>
    <p>Cuando el ViewModel vive en un Fragment, los imports y el delegate cambian según si se quiere una instancia propia o compartida con la Activity.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">TareasFragment.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> androidx.fragment.app.Fragment
<span class="kw">import</span> androidx.fragment.app.viewModels          <span class="cm">// instancia propia del Fragment</span>
<span class="kw">import</span> androidx.fragment.app.activityViewModels  <span class="cm">// instancia compartida con la Activity</span>
<span class="kw">import</span> androidx.recyclerview.widget.LinearLayoutManager
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">TareasFragment</span> : <span class="cls">Fragment</span>() {

    <span class="cm">// Opción A: ViewModel propio — se destruye cuando el Fragment se destruye</span>
    <span class="kw">private val</span> viewModelPropio: <span class="cls">TareasViewModel</span> <span class="kw">by</span> <span class="fn">viewModels</span>()

    <span class="cm">// Opción B: ViewModel compartido — el mismo que usa la Activity y otros Fragments</span>
    <span class="kw">private val</span> viewModelCompartido: <span class="cls">TareasViewModel</span> <span class="kw">by</span> <span class="fn">activityViewModels</span>()

    <span class="kw">override fun</span> <span class="fn">onCreateView</span>(
        inflater: <span class="cls">LayoutInflater</span>, container: <span class="cls">ViewGroup</span>?, savedInstanceState: <span class="cls">Bundle</span>?
    ): <span class="cls">View</span>? = inflater.<span class="fn">inflate</span>(<span class="cls">R</span>.layout.fragment_tareas, container, <span class="kw">false</span>)

    <span class="kw">override fun</span> <span class="fn">onViewCreated</span>(view: <span class="cls">View</span>, savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onViewCreated</span>(view, savedInstanceState)

        <span class="kw">val</span> recyclerView = view.<span class="fn">findViewById</span>&lt;<span class="cls">RecyclerView</span>&gt;(<span class="cls">R</span>.id.recyclerTareas)
        <span class="kw">val</span> adapter = <span class="cls">TareaAdapter</span>(
            onToggle   = { tarea <span class="op">-&gt;</span> viewModelCompartido.<span class="fn">toggleCompletada</span>(tarea) },
            onEliminar = { tarea <span class="op">-&gt;</span> viewModelCompartido.<span class="fn">eliminarTarea</span>(tarea) }
        )
        recyclerView.layoutManager = <span class="cls">LinearLayoutManager</span>(<span class="fn">requireContext</span>())
        recyclerView.adapter = adapter

        <span class="cm">// viewLifecycleOwner en lugar de 'this' — evita leaks cuando el Fragment
        // se recrea pero la Activity sigue viva</span>
        viewModelCompartido.tareas.<span class="fn">observe</span>(<span class="fn">viewLifecycleOwner</span>) { lista <span class="op">-&gt;</span>
            adapter.<span class="fn">actualizarLista</span>(lista)
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-purple">
      <span class="alert-icon">💡</span>
      <p><strong>viewLifecycleOwner vs this:</strong> En un Fragment siempre usar <code>viewLifecycleOwner</code> como owner del observer, no <code>this</code>. El Fragment puede existir sin tener una View activa (entre <code>onDestroyView</code> y <code>onCreateView</code>) y en ese estado recibir actualizaciones del LiveData causaría un crash al intentar acceder a vistas que ya no existen.</p>
    </div>
  </div>

  <!-- TAREA -->
  <div class="tarea">
    <div class="tarea-badge">📝 Práctica — Tarea</div>
    <h2>App: Gestor de Gastos Personales</h2>
    <p class="tarea-desc">Construye una app que gestione una lista de gastos usando ViewModel y LiveData. Los datos deben sobrevivir la rotación en todas las pantallas.</p>
    <div class="reqs">
      <div class="req">
        <div class="req-num">1</div>
        <div>Crear una <strong>data class <code>Gasto</code></strong> con: id (Int), descripcion (String), monto (Double) y categoria (String — ej: "Comida", "Transporte", "Ocio").</div>
      </div>
      <div class="req">
        <div class="req-num">2</div>
        <div>Crear <strong><code>GastoViewModel</code></strong> con LiveData para: la lista de gastos, el total acumulado (calculado automáticamente) y los campos del formulario de nuevo gasto.</div>
      </div>
      <div class="req">
        <div class="req-num">3</div>
        <div>La <strong>Activity principal</strong> muestra el total en la parte superior (se actualiza en tiempo real), un formulario para agregar gastos (descripción, monto, categoría) y el RecyclerView con la lista.</div>
      </div>
      <div class="req">
        <div class="req-num">4</div>
        <div>Al hacer clic en un gasto del RecyclerView, navegar a una <strong>Activity de detalle</strong> que también use ViewModel para mostrar los datos (no pasarlos solo por Intent).</div>
      </div>
      <div class="req">
        <div class="req-num">5</div>
        <div>Verificar que al <strong>rotar el dispositivo</strong> en cualquier pantalla, todos los datos y el texto escrito en los campos persisten correctamente.</div>
      </div>
      <div class="req">
        <div class="req-num star">⭐</div>
        <div><strong>Opcional:</strong> Agregar un LiveData <code>gastosPorCategoria</code> que calcule y exponga un <code>Map&lt;String, Double&gt;</code> con la suma de gastos por categoría, y mostrarlo en un TextView resumen.</div>
      </div>
    </div>
    <div class="entrega">
      <strong>📦 Entrega</strong>
      <p>Documento con breve descripción de la practica con capturas mostrando la lista de gastos, el formulario con datos escritos, y la misma pantalla después de rotar (datos intactos).</p>
    </div>
  </div>

</div>
</body>
</html>

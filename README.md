<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Semana 8 — Navegación entre Activities · Android Studio + Kotlin</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Fraunces:ital,wght@0,600;0,800;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #f5f0e8;
    --bg2: #ede8dc;
    --surface: #ffffff;
    --surface2: #faf8f4;
    --border: #d9d2c4;
    --border2: #c5bda8;
    --accent: #c84b2f;
    --accent2: #2d6a4f;
    --accent3: #1d3a5f;
    --gold: #b5892a;
    --text: #1a1612;
    --text-dim: #5c5549;
    --text-muted: #8c8070;
    --kotlin: #7f52ff;
    --xml: #c84b2f;
    --tag-bg: #1d3a5f;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    line-height: 1.75;
  }

  /* ── HERO ── */
  .hero {
    background: var(--accent3);
    padding: 64px 48px 52px;
    position: relative;
    overflow: hidden;
  }
  .hero::after {
    content: '02';
    position: absolute;
    right: -20px;
    top: -20px;
    font-family: 'Fraunces', serif;
    font-size: 220px;
    font-weight: 800;
    color: rgba(255,255,255,0.04);
    line-height: 1;
    pointer-events: none;
    user-select: none;
  }

  .week-tag {
    display: inline-block;
    background: var(--accent);
    color: #fff;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    padding: 5px 14px;
    border-radius: 2px;
    margin-bottom: 22px;
  }

  .hero h1 {
    font-family: 'Fraunces', serif;
    font-size: clamp(2.2rem, 5.5vw, 3.8rem);
    font-weight: 800;
    color: #fff;
    line-height: 1.08;
    margin-bottom: 16px;
    max-width: 700px;
  }
  .hero h1 em {
    font-style: italic;
    font-weight: 400;
    color: #a8c4d8;
  }

  .hero-sub {
    color: #8aafc7;
    font-size: 1rem;
    max-width: 580px;
    margin-bottom: 36px;
  }

  .meta-strip {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    border-top: 1px solid rgba(255,255,255,0.12);
    padding-top: 24px;
  }
  .meta-chip {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: #8aafc7;
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .meta-chip span {
    color: #fff;
    font-weight: 600;
  }

  /* ── LAYOUT ── */
  .container {
    max-width: 980px;
    margin: 0 auto;
    padding: 0 28px 100px;
  }

  /* ── CLASE HEADER ── */
  .clase-header {
    margin: 60px 0 30px;
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 0;
    border-left: 5px solid var(--accent3);
    padding-left: 20px;
  }
  .clase-eyebrow {
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 6px;
  }
  .clase-title {
    font-family: 'Fraunces', serif;
    font-size: 1.75rem;
    font-weight: 600;
    color: var(--text);
    line-height: 1.2;
  }
  .clase-title em {
    font-style: italic;
    color: var(--accent3);
  }

  /* ── OBJETIVO ── */
  .objetivo {
    background: var(--accent2);
    border-radius: 6px;
    padding: 16px 22px;
    margin-bottom: 32px;
    color: #fff;
    font-size: 0.9rem;
  }
  .objetivo strong {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    display: block;
    margin-bottom: 6px;
    color: #a8d5b5;
  }

  /* ── SECCIÓN ── */
  .section { margin-bottom: 38px; }
  .section-title {
    font-family: 'Fraunces', serif;
    font-size: 1.1rem;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 14px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  p { margin-bottom: 12px; color: var(--text-dim); font-size: 0.93rem; }

  /* ── DIAGRAMA BACK STACK ── */
  .stack-diagram {
    background: var(--accent3);
    border-radius: 10px;
    padding: 28px;
    margin: 20px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0;
  }
  .stack-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: #8aafc7;
    margin-bottom: 20px;
    align-self: flex-start;
  }
  .stack-row {
    display: flex;
    align-items: center;
    gap: 12px;
    width: 100%;
    margin-bottom: 6px;
  }
  .stack-box {
    flex: 1;
    background: rgba(255,255,255,0.1);
    border: 1px solid rgba(255,255,255,0.2);
    border-radius: 6px;
    padding: 10px 16px;
    color: #fff;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .stack-box.active {
    background: var(--accent);
    border-color: var(--accent);
  }
  .stack-box.top-label::after {
    content: '← TOP (visible)';
    font-size: 10px;
    color: #ffcba4;
    font-style: italic;
  }
  .stack-arrow {
    color: #8aafc7;
    font-size: 18px;
    text-align: center;
    width: 100%;
    margin: 2px 0;
  }
  .stack-base {
    width: 100%;
    border-top: 2px dashed rgba(255,255,255,0.2);
    padding-top: 10px;
    text-align: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    color: #8aafc7;
    letter-spacing: 0.1em;
  }

  /* ── CONCEPTS GRID ── */
  .concepts {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 14px;
    margin: 18px 0;
  }
  .concept-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 18px;
    border-top: 3px solid var(--accent3);
  }
  .concept-card .icon { font-size: 1.3rem; margin-bottom: 8px; }
  .concept-card h4 {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.78rem;
    color: var(--accent3);
    margin-bottom: 6px;
    font-weight: 700;
  }
  .concept-card p { font-size: 0.82rem; margin: 0; }

  /* ── CODE BLOCK ── */
  .code-block {
    background: #1a1612;
    border-radius: 10px;
    overflow: hidden;
    margin: 18px 0;
    font-size: 0.84rem;
    border: 1px solid #2d2820;
  }
  .code-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 18px;
    background: #221e19;
    border-bottom: 1px solid #2d2820;
  }
  .code-lang {
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 3px 10px;
    border-radius: 3px;
  }
  .lang-kotlin { background: rgba(127,82,255,0.2); color: #b08fff; border: 1px solid rgba(127,82,255,0.35); }
  .lang-xml    { background: rgba(200,75,47,0.2);  color: #e8836a; border: 1px solid rgba(200,75,47,0.35); }
  .code-filename {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: #6b6055;
  }
  .code-body { padding: 20px 22px; overflow-x: auto; }
  pre {
    font-family: 'JetBrains Mono', monospace;
    line-height: 1.65;
    white-space: pre;
    color: #e2ddd6;
  }

  /* Syntax */
  .kw  { color: #c792ea; }
  .fn  { color: #82aaff; }
  .str { color: #c3e88d; }
  .cm  { color: #4a453e; font-style: italic; }
  .num { color: #f78c6c; }
  .cls { color: #ffcb6b; }
  .op  { color: #89ddff; }
  .tag { color: #e06c75; }
  .attr{ color: #c3e88d; }
  .val { color: #f78c6c; }

  /* ── FLUJO COMPARATIVO ── */
  .compare-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    margin: 20px 0;
  }
  @media(max-width: 640px) { .compare-grid { grid-template-columns: 1fr; } }
  .compare-card {
    border-radius: 8px;
    padding: 18px;
    border: 1px solid var(--border);
  }
  .compare-card.old {
    background: #fff5f3;
    border-color: #f5c4bb;
  }
  .compare-card.new {
    background: #f3f9f5;
    border-color: #b8ddc4;
  }
  .compare-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    margin-bottom: 8px;
  }
  .compare-card.old .compare-label { color: var(--accent); }
  .compare-card.new .compare-label { color: var(--accent2); }
  .compare-card p { font-size: 0.83rem; margin: 0; }

  /* ── ALERT ── */
  .alert {
    border-radius: 6px;
    padding: 14px 18px;
    margin: 16px 0;
    font-size: 0.87rem;
    display: flex;
    gap: 12px;
    align-items: flex-start;
  }
  .alert-info { background: #edf4ff; border: 1px solid #bdd4f5; }
  .alert-warn { background: #fffbec; border: 1px solid #f0d98a; }
  .alert-icon { font-size: 1.1rem; flex-shrink: 0; }
  .alert p { margin: 0; color: var(--text-dim); }

  /* ── DIVIDER ── */
  .divider {
    border: none;
    border-top: 2px solid var(--border2);
    margin: 56px 0 0;
    position: relative;
  }
  .divider::after {
    content: '///';
    position: absolute;
    top: -11px;
    left: 50%;
    transform: translateX(-50%);
    background: var(--bg);
    padding: 0 12px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--text-muted);
    letter-spacing: 4px;
  }

  /* ── TAREA ── */
  .tarea {
    background: var(--accent3);
    border-radius: 12px;
    padding: 36px;
    margin-top: 56px;
    color: #fff;
    position: relative;
    overflow: hidden;
  }
  .tarea::before {
    content: 'TAREA';
    position: absolute;
    right: -10px; bottom: -20px;
    font-family: 'Fraunces', serif;
    font-size: 120px;
    font-weight: 800;
    color: rgba(255,255,255,0.04);
    line-height: 1;
    pointer-events: none;
  }
  .tarea-badge {
    display: inline-block;
    background: var(--gold);
    color: #fff;
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    padding: 4px 12px;
    border-radius: 2px;
    margin-bottom: 16px;
  }
  .tarea h2 {
    font-family: 'Fraunces', serif;
    font-size: 1.8rem;
    font-weight: 800;
    margin-bottom: 12px;
    color: #fff;
  }
  .tarea-desc { color: #8aafc7; margin-bottom: 24px; font-size: 0.93rem; }
  .reqs { display: flex; flex-direction: column; gap: 12px; margin-bottom: 26px; }
  .req {
    display: flex;
    gap: 12px;
    align-items: flex-start;
    font-size: 0.88rem;
    color: #c8dae8;
  }
  .req-num {
    min-width: 24px; height: 24px;
    background: rgba(255,255,255,0.1);
    border: 1px solid rgba(255,255,255,0.2);
    border-radius: 4px;
    display: flex; align-items: center; justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    color: #fff;
    flex-shrink: 0;
    margin-top: 2px;
  }
  .entrega {
    background: rgba(0,0,0,0.25);
    border-radius: 6px;
    padding: 14px 18px;
    font-size: 0.84rem;
  }
  .entrega strong {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    color: var(--gold);
    text-transform: uppercase;
    letter-spacing: 0.12em;
    display: block;
    margin-bottom: 5px;
  }
  .entrega p { color: #8aafc7; margin: 0; }

  ::-webkit-scrollbar { width: 5px; height: 5px; }
  ::-webkit-scrollbar-track { background: #221e19; }
  ::-webkit-scrollbar-thumb { background: #3d3630; border-radius: 3px; }
</style>
</head>
<body>

<!-- HERO -->
<div class="hero">
  <div class="week-tag">📅 Semana 8 de 16</div>
  <h1>Navegación entre<br><em>Activities</em> y Back Stack</h1>
  <p class="hero-sub">Flujo de pantallas complejo, manejo del Back Stack y retorno de resultados con ActivityResultLauncher.</p>
  <div class="meta-strip">
    <div class="meta-chip">Clases <span>2 × 2 hrs</span></div>
    <div class="meta-chip">Lenguaje <span>Kotlin</span></div>
    <div class="meta-chip">Layout <span>ConstraintLayout</span></div>
    <div class="meta-chip">Prereq <span>Semana 1 — RecyclerView</span></div>
  </div>
</div>

<div class="container">

  <!-- ══════════ CLASE 1 ══════════ -->
  <div class="clase-header">
    <div>
      <div class="clase-eyebrow">Clase 01 · Semana 8 de 16</div>
      <div class="clase-title">Back Stack y <em>navegación multi-pantalla</em></div>
    </div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo de la clase</strong>
    Comprender cómo Android gestiona el historial de pantallas (Back Stack) y construir un flujo de 3 Activities con navegación correcta hacia adelante y hacia atrás.
  </div>

  <!-- Concepto Back Stack -->
  <div class="section">
    <div class="section-title">¿Qué es el Back Stack?</div>
    <p>Android mantiene una pila de Activities abiertas. Cada vez que navegas a una nueva Activity, se apila encima. Al presionar "Atrás", la Activity del tope se destruye y vuelve la anterior.</p>

    <div class="stack-diagram">
      <div class="stack-title">// Estado del Back Stack al estar en PagoActivity</div>
      <div class="stack-row">
        <div class="stack-box active top-label">PagoActivity</div>
      </div>
      <div class="stack-arrow">↑ startActivity()</div>
      <div class="stack-row">
        <div class="stack-box">CarritoActivity</div>
      </div>
      <div class="stack-arrow">↑ startActivity()</div>
      <div class="stack-row">
        <div class="stack-box">MainActivity</div>
      </div>
      <div class="stack-base">— FONDO DEL STACK —</div>
    </div>

    <div class="concepts">
      <div class="concept-card">
        <div class="icon">⬅️</div>
        <h4>Botón "Atrás"</h4>
        <p>Llama automáticamente a <code>finish()</code> en la Activity actual y saca a la anterior del stack.</p>
      </div>
      <div class="concept-card">
        <div class="icon">🏠</div>
        <h4>finish()</h4>
        <p>Cierra la Activity actual programáticamente. Equivalente a presionar el botón Atrás.</p>
      </div>
      <div class="concept-card">
        <div class="icon">🚩</div>
        <h4>Flags del Intent</h4>
        <p>Controlan comportamientos especiales: limpiar el stack, traer Activity al frente, etc.</p>
      </div>
    </div>
  </div>

  <!-- Código 1: activity_main.xml -->
  <div class="section">
    <div class="section-title">Código 1 — Layout: Pantalla Principal</div>
    <p>App de una tienda con 3 pantallas: Lista de productos → Carrito → Pago.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_main.xml</span>
      </div>
      <div class="code-body"><pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"20dp"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvTitulo"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"🛍️ Tienda"</span>
        <span class="attr">android:textSize</span>=<span class="val">"28sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvProducto"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Laptop Pro 15 — $1,299.99"</span>
        <span class="attr">android:textSize</span>=<span class="val">"18sp"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"32dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvTitulo"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnAgregarCarrito"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Agregar al carrito →"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"24dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvProducto"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 2: activity_carrito.xml -->
  <div class="section">
    <div class="section-title">Código 2 — Layout: Carrito</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_carrito.xml</span>
      </div>
      <div class="code-body"><pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"20dp"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvTituloCarrito"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"🛒 Mi Carrito"</span>
        <span class="attr">android:textSize</span>=<span class="val">"26sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvItemCarrito"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"16sp"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"24dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvTituloCarrito"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnProcederPago"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Proceder al pago →"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"24dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvItemCarrito"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnVolverTienda"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"← Seguir comprando"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"12dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/btnProcederPago"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 3: activity_pago.xml -->
  <div class="section">
    <div class="section-title">Código 3 — Layout: Pantalla de Pago</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_pago.xml</span>
      </div>
      <div class="code-body"><pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"20dp"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvTituloPago"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"💳 Pago"</span>
        <span class="attr">android:textSize</span>=<span class="val">"26sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvResumenPago"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"16sp"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"24dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvTituloPago"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnConfirmarPago"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"✅ Confirmar Compra"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"32dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvResumenPago"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnCancelar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"✖ Cancelar y volver al inicio"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"12dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/btnConfirmarPago"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 4: MainActivity.kt -->
  <div class="section">
    <div class="section-title">Código 4 — MainActivity.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">MainActivity.kt</span>
      </div>
      <div class="code-body"><pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button

<span class="kw">class</span> <span class="cls">MainActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_main)

        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnAgregarCarrito).<span class="fn">setOnClickListener</span> {
            <span class="cm">// Ir al carrito enviando el producto como Extra</span>
            <span class="kw">val</span> intent = <span class="cls">Intent</span>(<span class="kw">this</span>, <span class="cls">CarritoActivity</span>::<span class="kw">class</span>.java)
            intent.<span class="fn">putExtra</span>(<span class="str">"PRODUCTO"</span>, <span class="str">"Laptop Pro 15"</span>)
            intent.<span class="fn">putExtra</span>(<span class="str">"PRECIO"</span>, <span class="num">1299.99</span>)
            <span class="fn">startActivity</span>(intent)
        }
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 5: CarritoActivity.kt -->
  <div class="section">
    <div class="section-title">Código 5 — CarritoActivity.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">CarritoActivity.kt</span>
      </div>
      <div class="code-body"><pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.TextView

<span class="kw">class</span> <span class="cls">CarritoActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_carrito)

        <span class="cm">// Recibir datos de la pantalla anterior</span>
        <span class="kw">val</span> producto = intent.<span class="fn">getStringExtra</span>(<span class="str">"PRODUCTO"</span>) <span class="op">?:</span> <span class="str">""</span>
        <span class="kw">val</span> precio   = intent.<span class="fn">getDoubleExtra</span>(<span class="str">"PRECIO"</span>, <span class="num">0.0</span>)

        <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvItemCarrito).text =
            <span class="str">"• $producto — ${"$"}${"%.2f".format(precio)}"</span>

        <span class="cm">// Avanzar a PagoActivity</span>
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnProcederPago).<span class="fn">setOnClickListener</span> {
            <span class="kw">val</span> intent = <span class="cls">Intent</span>(<span class="kw">this</span>, <span class="cls">PagoActivity</span>::<span class="kw">class</span>.java)
            intent.<span class="fn">putExtra</span>(<span class="str">"PRODUCTO"</span>, producto)
            intent.<span class="fn">putExtra</span>(<span class="str">"PRECIO"</span>, precio)
            <span class="fn">startActivity</span>(intent)
        }

        <span class="cm">// Volver a MainActivity usando finish()</span>
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnVolverTienda).<span class="fn">setOnClickListener</span> {
            <span class="fn">finish</span>()   <span class="cm">// Destruye esta Activity y vuelve a la anterior del stack</span>
        }
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 6: PagoActivity.kt -->
  <div class="section">
    <div class="section-title">Código 6 — PagoActivity.kt con FLAG para limpiar el stack</div>
    <p>Al confirmar la compra, queremos regresar a <code>MainActivity</code> <strong>limpiando todo el historial</strong> para que el usuario no pueda volver al carrito ni al pago con el botón Atrás.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">PagoActivity.kt</span>
      </div>
      <div class="code-body"><pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> android.widget.Toast

<span class="kw">class</span> <span class="cls">PagoActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_pago)

        <span class="kw">val</span> producto = intent.<span class="fn">getStringExtra</span>(<span class="str">"PRODUCTO"</span>) <span class="op">?:</span> <span class="str">""</span>
        <span class="kw">val</span> precio   = intent.<span class="fn">getDoubleExtra</span>(<span class="str">"PRECIO"</span>, <span class="num">0.0</span>)

        <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvResumenPago).text =
            <span class="str">"Producto: $producto\nTotal: ${"$"}${"%.2f".format(precio)}"</span>

        <span class="cm">// Confirmar: limpiar el Back Stack completo y volver al inicio</span>
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnConfirmarPago).<span class="fn">setOnClickListener</span> {
            <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"✅ ¡Compra confirmada!"</span>, <span class="cls">Toast</span>.LENGTH_LONG).<span class="fn">show</span>()

            <span class="kw">val</span> intent = <span class="cls">Intent</span>(<span class="kw">this</span>, <span class="cls">MainActivity</span>::<span class="kw">class</span>.java)
            <span class="cm">// FLAG_ACTIVITY_CLEAR_TOP: destruye todas las Activities encima de MainActivity</span>
            <span class="cm">// FLAG_ACTIVITY_NEW_TASK:  necesario al usar CLEAR_TOP en este contexto</span>
            intent.flags = <span class="cls">Intent</span>.FLAG_ACTIVITY_CLEAR_TOP <span class="op">or</span>
                           <span class="cls">Intent</span>.FLAG_ACTIVITY_NEW_TASK
            <span class="fn">startActivity</span>(intent)
            <span class="fn">finish</span>()
        }

        <span class="cm">// Cancelar: simplemente cerrar esta Activity (vuelve al carrito)</span>
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnCancelar).<span class="fn">setOnClickListener</span> {
            <span class="fn">finish</span>()
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-info">
      <span class="alert-icon">💡</span>
      <p><strong>FLAG_ACTIVITY_CLEAR_TOP</strong> es el patrón estándar para flujos de "compra exitosa", "login completado" o cualquier pantalla que no debe aparecer en el historial de Atrás.</p>
    </div>
  </div>

  <!-- ══════════ CLASE 2 ══════════ -->
  <hr class="divider">

  <div class="clase-header">
    <div>
      <div class="clase-eyebrow">Clase 02 · Semana 2</div>
      <div class="clase-title"><em>ActivityResultLauncher</em> — Retorno de resultados</div>
    </div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo de la clase</strong>
    Implementar comunicación bidireccional entre Activities: enviar datos hacia adelante <strong>y</strong> recibir un resultado de vuelta cuando la Activity secundaria cierra.
  </div>

  <!-- Comparativa -->
  <div class="section">
    <div class="section-title">El problema que resuelve</div>
    <p>¿Qué pasa cuando necesitas que la Activity B le devuelva información a la Activity A? Por ejemplo: el usuario edita su perfil en B y al volver a A queremos ver los cambios reflejados.</p>

    <div class="compare-grid">
      <div class="compare-card old">
        <div class="compare-label">❌ Método antiguo (deprecated)</div>
        <p><code>startActivityForResult()</code> + <code>onActivityResult()</code> — Deprecado desde API 29. No usar en código nuevo.</p>
      </div>
      <div class="compare-card new">
        <div class="compare-label">✅ Método actual</div>
        <p><code>ActivityResultLauncher</code> con <code>registerForActivityResult()</code> — Forma moderna, segura y recomendada por Google.</p>
      </div>
    </div>
  </div>

  <!-- Código 7: activity_editor.xml -->
  <div class="section">
    <div class="section-title">Código 7 — Layout: Editor de Perfil (Activity B)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_editor.xml</span>
      </div>
      <div class="code-body"><pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"20dp"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvEditorTitulo"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"✏️ Editar Perfil"</span>
        <span class="attr">android:textSize</span>=<span class="val">"24sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;EditText</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/etNuevoNombre"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:hint</span>=<span class="val">"Nuevo nombre"</span>
        <span class="attr">android:inputType</span>=<span class="val">"textPersonName"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"28dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvEditorTitulo"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;EditText</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/etNuevoEmail"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:hint</span>=<span class="val">"Nuevo email"</span>
        <span class="attr">android:inputType</span>=<span class="val">"textEmailAddress"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"14dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/etNuevoNombre"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnGuardar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Guardar cambios"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"24dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/etNuevoEmail"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnCancelarEditor"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Cancelar"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"10dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/btnGuardar"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 8: activity_perfil.xml -->
  <div class="section">
    <div class="section-title">Código 8 — Layout: Perfil (Activity A)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_perfil.xml</span>
      </div>
      <div class="code-body"><pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"20dp"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvPerfilTitulo"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"👤 Mi Perfil"</span>
        <span class="attr">android:textSize</span>=<span class="val">"26sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvNombreActual"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Nombre: Juan Pérez"</span>
        <span class="attr">android:textSize</span>=<span class="val">"18sp"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"28dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvPerfilTitulo"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvEmailActual"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Email: juan@email.com"</span>
        <span class="attr">android:textSize</span>=<span class="val">"16sp"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"10dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvNombreActual"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnEditarPerfil"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"✏️ Editar perfil"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"28dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvEmailActual"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 9: EditorActivity.kt -->
  <div class="section">
    <div class="section-title">Código 9 — EditorActivity.kt (Activity B: devuelve resultado)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">EditorActivity.kt</span>
      </div>
      <div class="code-body"><pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.app.Activity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.EditText

<span class="kw">class</span> <span class="cls">EditorActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_editor)

        <span class="kw">val</span> etNombre = <span class="fn">findViewById</span>&lt;<span class="cls">EditText</span>&gt;(<span class="cls">R</span>.id.etNuevoNombre)
        <span class="kw">val</span> etEmail  = <span class="fn">findViewById</span>&lt;<span class="cls">EditText</span>&gt;(<span class="cls">R</span>.id.etNuevoEmail)

        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnGuardar).<span class="fn">setOnClickListener</span> {
            <span class="kw">val</span> nombre = etNombre.text.toString()
            <span class="kw">val</span> email  = etEmail.text.toString()

            <span class="cm">// Preparar el Intent de resultado</span>
            <span class="kw">val</span> resultIntent = <span class="cls">Intent</span>()
            resultIntent.<span class="fn">putExtra</span>(<span class="str">"NUEVO_NOMBRE"</span>, nombre)
            resultIntent.<span class="fn">putExtra</span>(<span class="str">"NUEVO_EMAIL"</span>,  email)

            <span class="cm">// RESULT_OK indica que el usuario completó la acción exitosamente</span>
            <span class="fn">setResult</span>(<span class="cls">Activity</span>.RESULT_OK, resultIntent)
            <span class="fn">finish</span>()   <span class="cm">// Cierra EditorActivity y regresa a PerfilActivity</span>
        }

        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnCancelarEditor).<span class="fn">setOnClickListener</span> {
            <span class="cm">// RESULT_CANCELED: el usuario canceló, no hay datos que devolver</span>
            <span class="fn">setResult</span>(<span class="cls">Activity</span>.RESULT_CANCELED)
            <span class="fn">finish</span>()
        }
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 10: PerfilActivity.kt -->
  <div class="section">
    <div class="section-title">Código 10 — PerfilActivity.kt (Activity A: recibe el resultado)</div>
    <p>La clave está en registrar el launcher <strong>antes</strong> de que el usuario haga clic — se declara como propiedad de la clase, no dentro del <code>setOnClickListener</code>.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">PerfilActivity.kt</span>
      </div>
      <div class="code-body"><pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.app.Activity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> android.widget.Toast
<span class="kw">import</span> androidx.activity.result.contract.ActivityResultContracts

<span class="kw">class</span> <span class="cls">PerfilActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="cm">// ── 1. Registrar el launcher ANTES de onCreate ────────────────────────
    //    registerForActivityResult debe llamarse en la inicialización,
    //    no dentro de listeners o funciones que se ejecutan después.</span>
    <span class="kw">private val</span> editarPerfilLauncher = <span class="fn">registerForActivityResult</span>(
        <span class="cls">ActivityResultContracts</span>.<span class="cls">StartActivityForResult</span>()
    ) { result <span class="op">-&gt;</span>

        <span class="cm">// ── 2. Esta lambda se ejecuta cuando EditorActivity termina ──────</span>
        <span class="kw">if</span> (result.resultCode == <span class="cls">Activity</span>.RESULT_OK) {
            <span class="kw">val</span> data        = result.data
            <span class="kw">val</span> nuevoNombre = data<span class="op">?.</span><span class="fn">getStringExtra</span>(<span class="str">"NUEVO_NOMBRE"</span>) <span class="op">?:</span> <span class="str">""</span>
            <span class="kw">val</span> nuevoEmail  = data<span class="op">?.</span><span class="fn">getStringExtra</span>(<span class="str">"NUEVO_EMAIL"</span>)  <span class="op">?:</span> <span class="str">""</span>

            <span class="cm">// Actualizar la UI con los datos recibidos</span>
            <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvNombreActual).text = <span class="str">"Nombre: $nuevoNombre"</span>
            <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvEmailActual).text  = <span class="str">"Email: $nuevoEmail"</span>

            <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"✅ Perfil actualizado"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()

        } <span class="kw">else</span> {
            <span class="cm">// El usuario canceló o cerró el editor sin guardar</span>
            <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Edición cancelada"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()
        }
    }

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_perfil)

        <span class="cm">// ── 3. Usar el launcher al hacer clic en el botón ────────────────</span>
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnEditarPerfil).<span class="fn">setOnClickListener</span> {
            <span class="kw">val</span> intent = <span class="cls">Intent</span>(<span class="kw">this</span>, <span class="cls">EditorActivity</span>::<span class="kw">class</span>.java)
            editarPerfilLauncher.<span class="fn">launch</span>(intent)   <span class="cm">// Reemplaza startActivity()</span>
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-warn">
      <span class="alert-icon">⚠️</span>
      <p><strong>Error común:</strong> Si declaras el <code>registerForActivityResult</code> dentro de <code>onCreate()</code> en lugar de como propiedad de la clase, Android lanzará una excepción en tiempo de ejecución porque el registro debe ocurrir antes de que el ciclo de vida inicie.</p>
    </div>
    <div class="alert alert-info">
      <span class="alert-icon">💡</span>
      <p><strong>Conexión con Semana 1:</strong> El RecyclerView del ejemplo anterior puede usar este mismo patrón — al hacer clic en un ítem, abrir el editor con <code>launcher.launch(intent)</code>, editar el ítem y recibir el objeto modificado de vuelta para actualizar la lista.</p>
    </div>
  </div>

  <!-- ══════════ TAREA ══════════ -->
  <div class="tarea">
    <div class="tarea-badge">📝 Práctica — Tarea</div>
    <h2>App: Registro de Notas con edición</h2>
    <p class="tarea-desc">Desarrolla una app de 3 pantallas que gestione un registro de notas académicas, integrando RecyclerView (Semana 1) con el flujo de navegación y retorno de resultados de esta semana.</p>
    <div class="reqs">
      <div class="req"><div class="req-num">1</div><div><strong>MainActivity</strong>: muestra un RecyclerView con una lista de al menos 5 notas (materia + calificación). Cada ítem tiene un botón o clic que abre la pantalla de edición.</div></div>
      <div class="req"><div class="req-num">2</div><div><strong>EditarNotaActivity</strong>: recibe la nota actual como Extra, permite modificar la materia y la calificación con EditTexts, y al guardar devuelve los nuevos valores con <code>setResult(RESULT_OK, intent)</code>.</div></div>
      <div class="req"><div class="req-num">3</div><div>La <strong>MainActivity</strong> debe usar <code>ActivityResultLauncher</code> para recibir la nota editada y <strong>actualizar el ítem correspondiente en el RecyclerView</strong> sin recargar toda la lista.</div></div>
      <div class="req"><div class="req-num">4</div><div><strong>DetalleNotaActivity</strong>: al hacer clic largo (long click) sobre un ítem del RecyclerView, navegar a una tercera pantalla que muestre el historial de cambios del ítem (al menos la nota actual).</div></div>
      <div class="req"><div class="req-num">5</div><div>El flujo de navegación debe ser correcto: usar <code>finish()</code> al cancelar y manejar el botón Atrás del sistema adecuadamente en cada pantalla.</div></div>
      <div class="req"><div class="req-num">⭐</div><div><strong>Punto extra:</strong> Al presionar "Guardar" en la edición, si la nueva calificación es diferente a la anterior, mostrar un <code>Toast</code> en <strong>MainActivity</strong> indicando el cambio: <em>"Cálculo: 8.5 → 9.2"</em>.</div></div>
    </div>
    <div class="entrega">
      <strong>📦 Entrega</strong>
      <p>Lunes 23 de marzo, demostración en vivo para firma.</p>
    </div>
  </div>

</div>
</body>
</html>

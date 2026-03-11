# Xtian51.github.io

<!DOCTYPE html>
<html lang="es">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Semana 1 — RecyclerView · Android Studio + Kotlin</title>
  <link
    href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Syne:wght@400;700;800&family=Inter:wght@300;400;500&display=swap"
    rel="stylesheet">
  <style>
    :root {
      --bg: #0d0f14;
      --surface: #13161e;
      --surface2: #1a1e2a;
      --border: #252a38;
      --accent: #4f9eff;
      --accent2: #a78bfa;
      --accent3: #34d399;
      --warn: #fbbf24;
      --text: #e2e8f0;
      --text-muted: #64748b;
      --text-dim: #94a3b8;
      --kotlin: #7f52ff;
      --xml: #f97316;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Inter', sans-serif;
      font-weight: 300;
      line-height: 1.7;
    }

    .hero {
      background: linear-gradient(135deg, #0d0f14 0%, #111827 50%, #0d0f14 100%);
      border-bottom: 1px solid var(--border);
      padding: 60px 40px 50px;
      position: relative;
      overflow: hidden;
    }

    .hero::before {
      content: '';
      position: absolute;
      top: -80px;
      right: -80px;
      width: 400px;
      height: 400px;
      background: radial-gradient(circle, rgba(79, 158, 255, 0.08) 0%, transparent 70%);
    }

    .pill {
      display: inline-block;
      background: rgba(79, 158, 255, 0.12);
      border: 1px solid rgba(79, 158, 255, 0.3);
      color: var(--accent);
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      letter-spacing: 0.12em;
      padding: 4px 14px;
      border-radius: 20px;
      margin-bottom: 20px;
      text-transform: uppercase;
    }

    .hero h1 {
      font-family: 'Syne', sans-serif;
      font-size: clamp(2rem, 5vw, 3.4rem);
      font-weight: 800;
      line-height: 1.1;
      margin-bottom: 12px;
    }

    .hero h1 span {
      color: var(--accent);
    }

    .hero-sub {
      color: var(--text-dim);
      font-size: 1.05rem;
      max-width: 620px;
      margin-bottom: 32px;
    }

    .meta-row {
      display: flex;
      flex-wrap: wrap;
      gap: 24px;
    }

    .meta-item {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 13px;
      color: var(--text-dim);
    }

    .meta-item .dot {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: var(--accent3);
    }

    .meta-item .dot.purple {
      background: var(--accent2);
    }

    .meta-item .dot.yellow {
      background: var(--warn);
    }

    .container {
      max-width: 960px;
      margin: 0 auto;
      padding: 0 24px 80px;
    }

    .clase-header {
      display: flex;
      align-items: center;
      gap: 16px;
      margin: 52px 0 28px;
    }

    .clase-num {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.1em;
      background: var(--surface2);
      border: 1px solid var(--border);
      color: var(--text-muted);
      padding: 6px 14px;
      border-radius: 6px;
      white-space: nowrap;
      text-transform: uppercase;
    }

    .clase-title {
      font-family: 'Syne', sans-serif;
      font-size: 1.5rem;
      font-weight: 700;
    }

    .clase-title span {
      color: var(--accent2);
    }

    .clase-line {
      flex: 1;
      height: 1px;
      background: linear-gradient(to right, var(--border), transparent);
    }

    .objetivo {
      background: rgba(52, 211, 153, 0.06);
      border: 1px solid rgba(52, 211, 153, 0.2);
      border-left: 3px solid var(--accent3);
      border-radius: 8px;
      padding: 16px 20px;
      margin-bottom: 28px;
      font-size: 0.9rem;
    }

    .objetivo strong {
      color: var(--accent3);
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      display: block;
      margin-bottom: 6px;
    }

    .section {
      margin-bottom: 36px;
    }

    .section-title {
      font-family: 'Syne', sans-serif;
      font-size: 1.1rem;
      font-weight: 700;
      margin-bottom: 14px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .section-title::before {
      content: '';
      width: 4px;
      height: 18px;
      background: var(--accent);
      border-radius: 2px;
      flex-shrink: 0;
    }

    p {
      margin-bottom: 12px;
      color: var(--text-dim);
      font-size: 0.95rem;
    }

    .concepts {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 14px;
      margin: 20px 0;
    }

    .concept-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 16px;
    }

    .concept-card .icon {
      font-size: 1.4rem;
      margin-bottom: 8px;
    }

    .concept-card h4 {
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.8rem;
      color: var(--accent);
      margin-bottom: 6px;
    }

    .concept-card p {
      font-size: 0.82rem;
      margin: 0;
      color: var(--text-muted);
    }

    .code-block {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 10px;
      overflow: hidden;
      margin: 20px 0;
      font-size: 0.85rem;
    }

    .code-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 16px;
      background: var(--surface2);
      border-bottom: 1px solid var(--border);
    }

    .code-lang {
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      font-weight: 700;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 3px 10px;
      border-radius: 4px;
    }

    .lang-kotlin {
      background: rgba(127, 82, 255, 0.2);
      color: var(--kotlin);
      border: 1px solid rgba(127, 82, 255, 0.3);
    }

    .lang-xml {
      background: rgba(249, 115, 22, 0.15);
      color: var(--xml);
      border: 1px solid rgba(249, 115, 22, 0.3);
    }

    .code-filename {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      color: var(--text-muted);
    }

    .code-body {
      padding: 20px;
      overflow-x: auto;
    }

    pre {
      font-family: 'JetBrains Mono', monospace;
      line-height: 1.65;
      white-space: pre;
      color: var(--text);
    }

    .kw {
      color: #c792ea;
    }

    .fn {
      color: #82aaff;
    }

    .str {
      color: #c3e88d;
    }

    .cm {
      color: #546e7a;
      font-style: italic;
    }

    .num {
      color: #f78c6c;
    }

    .cls {
      color: #ffcb6b;
    }

    .op {
      color: #89ddff;
    }

    .tag {
      color: #f07178;
    }

    .attr {
      color: #c3e88d;
    }

    .val {
      color: #f78c6c;
    }

    .steps {
      counter-reset: step;
      display: flex;
      flex-direction: column;
      gap: 14px;
      margin: 20px 0;
    }

    .step {
      display: flex;
      gap: 16px;
      align-items: flex-start;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 16px;
    }

    .step-num {
      min-width: 30px;
      height: 30px;
      background: var(--accent);
      color: #000;
      font-family: 'JetBrains Mono', monospace;
      font-size: 13px;
      font-weight: 700;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
    }

    .step-content h4 {
      font-family: 'Syne', sans-serif;
      font-size: 0.95rem;
      margin-bottom: 4px;
    }

    .step-content p {
      font-size: 0.85rem;
      margin: 0;
    }

    .alert {
      border-radius: 8px;
      padding: 14px 18px;
      margin: 18px 0;
      font-size: 0.88rem;
      display: flex;
      gap: 12px;
      align-items: flex-start;
    }

    .alert-info {
      background: rgba(79, 158, 255, 0.07);
      border: 1px solid rgba(79, 158, 255, 0.2);
    }

    .alert-warn {
      background: rgba(251, 191, 36, 0.07);
      border: 1px solid rgba(251, 191, 36, 0.2);
    }

    .alert-icon {
      font-size: 1.1rem;
      flex-shrink: 0;
      margin-top: 1px;
    }

    .alert p {
      margin: 0;
    }

    .divider {
      border: none;
      border-top: 1px solid var(--border);
      margin: 48px 0 0;
    }

    .tarea {
      background: linear-gradient(135deg, rgba(167, 139, 250, 0.08), rgba(79, 158, 255, 0.05));
      border: 1px solid rgba(167, 139, 250, 0.25);
      border-radius: 14px;
      padding: 32px;
      margin-top: 52px;
    }

    .tarea-badge {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: rgba(167, 139, 250, 0.15);
      border: 1px solid rgba(167, 139, 250, 0.3);
      color: var(--accent2);
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      padding: 5px 14px;
      border-radius: 20px;
      margin-bottom: 18px;
    }

    .tarea h2 {
      font-family: 'Syne', sans-serif;
      font-size: 1.6rem;
      font-weight: 800;
      margin-bottom: 14px;
    }

    .tarea-desc {
      color: var(--text-dim);
      margin-bottom: 22px;
    }

    .reqs {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-bottom: 24px;
    }

    .req {
      display: flex;
      gap: 12px;
      align-items: flex-start;
      font-size: 0.9rem;
      color: var(--text-dim);
    }

    .req-check {
      width: 20px;
      height: 20px;
      border: 2px solid var(--accent2);
      border-radius: 4px;
      flex-shrink: 0;
      margin-top: 1px;
    }

    .entrega {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 14px 18px;
      font-size: 0.85rem;
    }

    .entrega strong {
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      color: var(--warn);
      text-transform: uppercase;
      letter-spacing: 0.1em;
      display: block;
      margin-bottom: 6px;
    }

    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }

    ::-webkit-scrollbar-track {
      background: var(--surface);
    }

    ::-webkit-scrollbar-thumb {
      background: var(--border);
      border-radius: 3px;
    }
  </style>
</head>

<body>

  <div class="hero">
    <div class="pill"> Semana 7 de 16 - Programación de Aplicaciones Móviles 8A</div>
    <h1>RecyclerView<br><span>en Android</span></h1>
    <p class="hero-sub">Aprende a mostrar listas dinámicas de datos con el componente más potente de Android, usando
      Kotlin y ConstraintLayout.</p>
    <div class="meta-row">
      <div class="meta-item">
        <div class="dot"></div> 2 clases · 2 horas c/u
      </div>
      <div class="meta-item">
        <div class="dot yellow"></div> ConstraintLayout
      </div>
    </div>
  </div>

  <div class="container">

    <!-- CLASE 1 -->
    <div class="clase-header">
      <span class="clase-num">Clase 01</span>
      <h2 class="clase-title">Fundamentos del <span>RecyclerView</span></h2>
      <div class="clase-line"></div>
    </div>

    <div class="objetivo">
      <strong>🎯 Objetivo de la clase</strong>
      Comprender la arquitectura de RecyclerView (Adapter + ViewHolder) y lograr mostrar una lista estática de texto en
      pantalla.
    </div>

    <div class="section">
      <div class="section-title">¿Qué es RecyclerView?</div>
      <p>RecyclerView es el componente oficial de Android para mostrar listas o grillas de datos. A diferencia del
        antiguo ListView, <strong>recicla</strong> las vistas que salen de pantalla en lugar de destruirlas, haciéndolo
        muy eficiente con listas largas.</p>
      <div class="concepts">
        <div class="concept-card">
          <div class="icon">♻️</div>
          <h4>RecyclerView</h4>
          <p>El contenedor visible en el layout. Gestiona qué ítems se muestran.</p>
        </div>
        <div class="concept-card">
          <div class="icon">🔌</div>
          <h4>Adapter</h4>
          <p>Puente entre los datos y las vistas. Crea y enlaza cada ítem.</p>
        </div>
        <div class="concept-card">
          <div class="icon">📦</div>
          <h4>ViewHolder</h4>
          <p>Guarda referencias a las vistas de un ítem para no buscarlas cada vez.</p>
        </div>
        <div class="concept-card">
          <div class="icon">📐</div>
          <h4>LayoutManager</h4>
          <p>Decide la posición de los ítems: lista vertical, horizontal o grilla.</p>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Pasos para configurar el proyecto</div>
      <div class="steps">
        <div class="step">
          <div class="step-num">1</div>
          <div class="step-content">
            <h4>Verificar dependencia en build.gradle</h4>
            <p>RecyclerView está en AndroidX. Confirmar que esté incluido.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-num">2</div>
          <div class="step-content">
            <h4>Agregar RecyclerView al layout de la Activity</h4>
            <p>Colocar el widget en el XML con ConstraintLayout.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-num">3</div>
          <div class="step-content">
            <h4>Crear el layout del ítem individual</h4>
            <p>Un XML separado que define cómo se ve cada fila de la lista.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-num">4</div>
          <div class="step-content">
            <h4>Crear el Adapter con su ViewHolder</h4>
            <p>La clase Kotlin que conecta los datos con las vistas.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-num">5</div>
          <div class="step-content">
            <h4>Configurar todo en la Activity</h4>
            <p>Asignar LayoutManager y Adapter al RecyclerView.</p>
          </div>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 1 — Dependencia</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Gradle · Kotlin DSL</span>
          <span class="code-filename">build.gradle.kts (Module)</span>
        </div>
        <div class="code-body">
          <pre><span class="cm">// En el bloque dependencies{} — normalmente ya viene incluido</span>
<span class="fn">dependencies</span> {
    <span class="fn">implementation</span>(<span class="str">"androidx.recyclerview:recyclerview:1.3.2"</span>)
}</pre>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 2 — Layout principal</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-xml">XML</span>
          <span class="code-filename">res/layout/activity_main.xml</span>
        </div>
        <div class="code-body">
          <pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;androidx.recyclerview.widget.RecyclerView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/recyclerView"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">android:clipToPadding</span>=<span class="val">"false"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre>
        </div>
      </div>
      <div class="alert alert-info">
        <span class="alert-icon">💡</span>
        <p><strong>width/height = "0dp"</strong> en ConstraintLayout significa "ocupa el espacio definido por las
          constraints". Es equivalente a <code>match_constraint</code>.</p>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 3 — Layout del ítem</div>
      <p>Este XML define cómo se ve cada fila. Se crea como nuevo archivo en <code>res/layout/</code>.</p>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-xml">XML</span>
          <span class="code-filename">res/layout/item_fruta.xml</span>
        </div>
        <div class="code-body">
          <pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
    <span class="attr">android:padding</span>=<span class="val">"12dp"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvNombreFruta"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Fruta"</span>
        <span class="attr">android:textSize</span>=<span class="val">"18sp"</span>
        <span class="attr">android:textColor</span>=<span class="val">"@android:color/black"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 4 — Adapter y ViewHolder</div>
      <p>El corazón del RecyclerView. Observar los tres métodos obligatorios que toda clase Adapter debe implementar.
      </p>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">FrutaAdapter.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="cm">/**
 * Adapter que conecta una lista de Strings con el RecyclerView.
 * @param frutas Lista de datos que se van a mostrar.
 */</span>
<span class="kw">class</span> <span class="cls">FrutaAdapter</span>(<span class="kw">private val</span> frutas: <span class="cls">List</span>&lt;<span class="cls">String</span>&gt;) :
    <span class="cls">RecyclerView</span>.<span class="cls">Adapter</span>&lt;<span class="cls">FrutaAdapter</span>.<span class="cls">FrutaViewHolder</span>&gt;() {

    <span class="cm">// ViewHolder: guarda referencias a las vistas del ítem</span>
    <span class="kw">inner class</span> <span class="cls">FrutaViewHolder</span>(itemView: <span class="cls">View</span>) : <span class="cls">RecyclerView</span>.<span class="cls">ViewHolder</span>(itemView) {
        <span class="kw">val</span> tvNombre: <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvNombreFruta)
    }

    <span class="cm">// 1. Infla el layout del ítem y crea el ViewHolder</span>
    <span class="kw">override fun</span> <span class="fn">onCreateViewHolder</span>(parent: <span class="cls">ViewGroup</span>, viewType: <span class="cls">Int</span>): <span class="cls">FrutaViewHolder</span> {
        <span class="kw">val</span> vista = <span class="cls">LayoutInflater</span>.<span class="fn">from</span>(parent.context)
            .<span class="fn">i

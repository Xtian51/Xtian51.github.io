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
            .<span class="fn">inflate</span>(<span class="cls">R</span>.layout.item_fruta, parent, <span class="kw">false</span>)
        <span class="kw">return</span> <span class="cls">FrutaViewHolder</span>(vista)
    }

    <span class="cm">// 2. Enlaza los datos del ítem en posición [position]</span>
    <span class="kw">override fun</span> <span class="fn">onBindViewHolder</span>(holder: <span class="cls">FrutaViewHolder</span>, position: <span class="cls">Int</span>) {
        holder.tvNombre.text = frutas[position]
    }

    <span class="cm">// 3. Informa cuántos ítems tiene la lista</span>
    <span class="kw">override fun</span> <span class="fn">getItemCount</span>(): <span class="cls">Int</span> = frutas.size
}</pre>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 5 — MainActivity (Clase 1)</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">MainActivity.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> androidx.recyclerview.widget.LinearLayoutManager
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">MainActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_main)

        <span class="cm">// 1. Datos de ejemplo (lista estática)</span>
        <span class="kw">val</span> listaFrutas = <span class="fn">listOf</span>(
            <span class="str">"🍎 Manzana"</span>, <span class="str">"🍌 Banano"</span>,  <span class="str">"🍊 Naranja"</span>,
            <span class="str">"🍇 Uvas"</span>,    <span class="str">"🍓 Fresa"</span>,   <span class="str">"🥭 Mango"</span>,
            <span class="str">"🍍 Piña"</span>,    <span class="str">"🍑 Durazno"</span>, <span class="str">"🍒 Cereza"</span>,
            <span class="str">"🥝 Kiwi"</span>,    <span class="str">"🍋 Limón"</span>,   <span class="str">"🫐 Arándano"</span>
        )

        <span class="cm">// 2. Obtener referencia al RecyclerView</span>
        <span class="kw">val</span> recyclerView = <span class="fn">findViewById</span>&lt;<span class="cls">RecyclerView</span>&gt;(<span class="cls">R</span>.id.recyclerView)

        <span class="cm">// 3. Asignar LayoutManager (lista vertical)</span>
        recyclerView.layoutManager = <span class="cls">LinearLayoutManager</span>(<span class="kw">this</span>)

        <span class="cm">// 4. Crear y asignar el Adapter</span>
        recyclerView.adapter = <span class="cls">FrutaAdapter</span>(listaFrutas)
    }
}</pre>
        </div>
      </div>
      <div class="alert alert-warn">
        <span class="alert-icon">⚠️</span>
        <p><strong>Punto de discusión:</strong> Probar reemplazar <code>LinearLayoutManager(this)</code> por
          <code>GridLayoutManager(this, 2)</code> y observar el cambio sin modificar el Adapter. ¿Por qué funciona así?
        </p>
      </div>
    </div>

    <!-- CLASE 2 -->
    <hr class="divider">

    <div class="clase-header">
      <span class="clase-num">Clase 02</span>
      <h2 class="clase-title">Ítems con <span>múltiples vistas</span> y clics</h2>
      <div class="clase-line"></div>
    </div>

    <div class="objetivo">
      <strong>🎯 Objetivo de la clase</strong>
      Evolucionar el ejemplo usando una data class propia, mostrar múltiples campos por ítem y manejar el evento clic en
      cada fila para navegar a otra Activity.
    </div>

    <div class="section">
      <div class="section-title">Código 6 — Data class del modelo</div>
      <p>En lugar de usar <code>String</code> directamente, definimos una clase de datos que representa el dominio del
        problema.</p>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">Producto.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="cm">/**
 * Modelo de datos para un producto.
 * 'data class' genera automáticamente equals(), hashCode() y toString().
 */</span>
<span class="kw">data class</span> <span class="cls">Producto</span>(
    <span class="kw">val</span> nombre:     <span class="cls">String</span>,
    <span class="kw">val</span> precio:     <span class="cls">Double</span>,
    <span class="kw">val</span> disponible: <span class="cls">Boolean</span>
)</pre>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 7 — Layout del ítem con múltiples vistas</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-xml">XML</span>
          <span class="code-filename">res/layout/item_producto.xml</span>
        </div>
        <div class="code-body">
          <pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
    <span class="attr">android:padding</span>=<span class="val">"12dp"</span>
    <span class="attr">android:background</span>=<span class="val">"?attr/selectableItemBackground"</span><span class="tag">&gt;</span>

    <span class="cm">&lt;!-- Nombre del producto --&gt;</span>
    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvNombre"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"17sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">android:textColor</span>=<span class="val">"@android:color/black"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toStartOf</span>=<span class="val">"@id/tvPrecio"</span> <span class="tag">/&gt;</span>

    <span class="cm">&lt;!-- Precio (derecha) --&gt;</span>
    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvPrecio"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"16sp"</span>
        <span class="attr">android:textColor</span>=<span class="val">"#1a7a4a"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="cm">&lt;!-- Estado de disponibilidad (abajo) --&gt;</span>
    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvEstado"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"13sp"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"4dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvNombre"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 8 — Adapter con clic y lógica condicional</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">ProductoAdapter.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> android.graphics.Color
<span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">ProductoAdapter</span>(
    <span class="kw">private val</span> productos: <span class="cls">List</span>&lt;<span class="cls">Producto</span>&gt;,
    <span class="kw">private val</span> onItemClick: (<span class="cls">Producto</span>) <span class="op">-&gt;</span> <span class="cls">Unit</span>   <span class="cm">// Lambda para el clic</span>
) : <span class="cls">RecyclerView</span>.<span class="cls">Adapter</span>&lt;<span class="cls">ProductoAdapter</span>.<span class="cls">ProductoViewHolder</span>&gt;() {

    <span class="kw">inner class</span> <span class="cls">ProductoViewHolder</span>(itemView: <span class="cls">View</span>) : <span class="cls">RecyclerView</span>.<span class="cls">ViewHolder</span>(itemView) {
        <span class="kw">val</span> tvNombre: <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvNombre)
        <span class="kw">val</span> tvPrecio: <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvPrecio)
        <span class="kw">val</span> tvEstado: <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvEstado)
    }

    <span class="kw">override fun</span> <span class="fn">onCreateViewHolder</span>(parent: <span class="cls">ViewGroup</span>, viewType: <span class="cls">Int</span>): <span class="cls">ProductoViewHolder</span> {
        <span class="kw">val</span> vista = <span class="cls">LayoutInflater</span>.<span class="fn">from</span>(parent.context)
            .<span class="fn">inflate</span>(<span class="cls">R</span>.layout.item_producto, parent, <span class="kw">false</span>)
        <span class="kw">return</span> <span class="cls">ProductoViewHolder</span>(vista)
    }

    <span class="kw">override fun</span> <span class="fn">onBindViewHolder</span>(holder: <span class="cls">ProductoViewHolder</span>, position: <span class="cls">Int</span>) {
        <span class="kw">val</span> producto = productos[position]

        <span class="cm">// Enlazar datos</span>
        holder.tvNombre.text = producto.nombre
        holder.tvPrecio.text = <span class="str">"$%.2f"</span>.<span class="fn">format</span>(producto.precio)

        <span class="cm">// Lógica condicional según disponibilidad</span>
        <span class="kw">if</span> (producto.disponible) {
            holder.tvEstado.text = <span class="str">"✅ Disponible"</span>
            holder.tvEstado.<span class="fn">setTextColor</span>(<span class="cls">Color</span>.<span class="fn">parseColor</span>(<span class="str">"#1a7a4a"</span>))
        } <span class="kw">else</span> {
            holder.tvEstado.text = <span class="str">"❌ Agotado"</span>
            holder.tvEstado.<span class="fn">setTextColor</span>(<span class="cls">Color</span>.<span class="fn">parseColor</span>(<span class="str">"#c0392b"</span>))
        }

        <span class="cm">// Manejar el clic sobre el ítem completo</span>
        holder.itemView.<span class="fn">setOnClickListener</span> {
            <span class="fn">onItemClick</span>(producto)
        }
    }

    <span class="kw">override fun</span> <span class="fn">getItemCount</span>(): <span class="cls">Int</span> = productos.size
}</pre>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 9 — MainActivity final (Clase 2)</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">MainActivity.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Toast
<span class="kw">import</span> androidx.recyclerview.widget.LinearLayoutManager
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">MainActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_main)

        <span class="kw">val</span> listaProductos = <span class="fn">listOf</span>(
            <span class="cls">Producto</span>(<span class="str">"Laptop Pro 15"</span>,    <span class="num">1299.99</span>, <span class="kw">true</span>),
            <span class="cls">Producto</span>(<span class="str">"Teclado Mecánico"</span>,  <span class="num">89.99</span>,  <span class="kw">true</span>),
            <span class="cls">Producto</span>(<span class="str">"Monitor 4K"</span>,        <span class="num">549.00</span>, <span class="kw">false</span>),
            <span class="cls">Producto</span>(<span class="str">"Mouse Inalámbrico"</span>,  <span class="num">45.50</span>,  <span class="kw">true</span>),
            <span class="cls">Producto</span>(<span class="str">"Webcam HD"</span>,          <span class="num">79.00</span>,  <span class="kw">false</span>),
            <span class="cls">Producto</span>(<span class="str">"Auriculares BT"</span>,     <span class="num">159.99</span>, <span class="kw">true</span>),
            <span class="cls">Producto</span>(<span class="str">"Hub USB-C"</span>,          <span class="num">35.00</span>,  <span class="kw">true</span>)
        )

        <span class="kw">val</span> recyclerView = <span class="fn">findViewById</span>&lt;<span class="cls">RecyclerView</span>&gt;(<span class="cls">R</span>.id.recyclerView)
        recyclerView.layoutManager = <span class="cls">LinearLayoutManager</span>(<span class="kw">this</span>)

        <span class="cm">// Al hacer clic: mostrar Toast Y navegar a DetalleActivity</span>
        recyclerView.adapter = <span class="cls">ProductoAdapter</span>(listaProductos) { producto <span class="op">-&gt;</span>
            <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Seleccionaste: ${producto.nombre}"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()

            <span class="cm">// Reutilizamos lo que ya saben: Intent + Extras</span>
            <span class="kw">val</span> intent = <span class="cls">Intent</span>(<span class="kw">this</span>, <span class="cls">DetalleActivity</span>::<span class="kw">class</span>.java)
            intent.<span class="fn">putExtra</span>(<span class="str">"NOMBRE"</span>,     producto.nombre)
            intent.<span class="fn">putExtra</span>(<span class="str">"PRECIO"</span>,     producto.precio)
            intent.<span class="fn">putExtra</span>(<span class="str">"DISPONIBLE"</span>, producto.disponible)
            <span class="fn">startActivity</span>(intent)
        }
    }
}</pre>
        </div>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 10 — DetalleActivity (recibe los Extras)</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">DetalleActivity.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.graphics.Color
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.TextView

<span class="kw">class</span> <span class="cls">DetalleActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_detalle)

        <span class="cm">// Recuperar los extras (ya lo saben hacer)</span>
        <span class="kw">val</span> nombre     = intent.<span class="fn">getStringExtra</span>(<span class="str">"NOMBRE"</span>) <span class="op">?:</span> <span class="str">"Sin nombre"</span>
        <span class="kw">val</span> precio     = intent.<span class="fn">getDoubleExtra</span>(<span class="str">"PRECIO"</span>, <span class="num">0.0</span>)
        <span class="kw">val</span> disponible = intent.<span class="fn">getBooleanExtra</span>(<span class="str">"DISPONIBLE"</span>, <span class="kw">false</span>)

        <span class="cm">// Mostrar en los TextViews del layout de detalle</span>
        <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvDetNombre).<span class="fn">text</span>  = nombre
        <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvDetPrecio).<span class="fn">text</span>  = <span class="str">"Precio: $%.2f"</span>.<span class="fn">format</span>(precio)

        <span class="kw">val</span> tvEstado = <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvDetEstado)
        <span class="kw">if</span> (disponible) {
            tvEstado.text = <span class="str">"✅ En stock"</span>
            tvEstado.<span class="fn">setTextColor</span>(<span class="cls">Color</span>.<span class="fn">parseColor</span>(<span class="str">"#1a7a4a"</span>))
        } <span class="kw">else</span> {
            tvEstado.text = <span class="str">"❌ Sin stock"</span>
            tvEstado.<span class="fn">setTextColor</span>(<span class="cls">Color</span>.<span class="fn">parseColor</span>(<span class="str">"#c0392b"</span>))
        }

        <span class="cm">// Botón Volver: cierra esta Activity y regresa al Back Stack</span>
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnVolver).<span class="fn">setOnClickListener</span> {
            <span class="fn">finish</span>()
        }
    }
}</pre>
        </div>
      </div>
      <div class="alert alert-info">
        <span class="alert-icon">💡</span>
        <p><strong>Conexión con lo ya visto:</strong> el Intent con Extras es exactamente lo que aprendieron antes.
          RecyclerView simplemente es el disparador del clic que inicia ese flujo.</p>
      </div>
    </div>

    <div class="section">
      <div class="section-title">Código 11 — Layout de DetalleActivity</div>
      <p>Layout de la segunda pantalla. Muestra los tres campos del producto y un botón para volver a la lista.</p>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-xml">XML</span>
          <span class="code-filename">res/layout/activity_detalle.xml</span>
        </div>
        <div class="code-body">
          <pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"24dp"</span><span class="tag">&gt;</span>

    <span class="cm">&lt;!-- Nombre del producto (título principal) --&gt;</span>
    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvDetNombre"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Nombre"</span>
        <span class="attr">android:textSize</span>=<span class="val">"26sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">android:textColor</span>=<span class="val">"@android:color/black"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="cm">&lt;!-- Precio --&gt;</span>
    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvDetPrecio"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Precio"</span>
        <span class="attr">android:textSize</span>=<span class="val">"20sp"</span>
        <span class="attr">android:textColor</span>=<span class="val">"#1a7a4a"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"16dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvDetNombre"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="cm">&lt;!-- Estado de disponibilidad --&gt;</span>
    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvDetEstado"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Estado"</span>
        <span class="attr">android:textSize</span>=<span class="val">"18sp"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"12dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvDetPrecio"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="cm">&lt;!-- Botón volver --&gt;</span>
    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnVolver"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"← Volver a la lista"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"32dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvDetEstado"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre>
        </div>
      </div>
      <div class="alert alert-warn">
        <span class="alert-icon">⚠️</span>
        <p><strong>No olvidar:</strong> conectar el botón en <code>DetalleActivity.kt</code> con
          <code>findViewById&lt;Button&gt;(R.id.btnVolver).setOnClickListener { finish() }</code>. El método
          <code>finish()</code> cierra la Activity actual y regresa a la anterior del Back Stack.
        </p>
      </div>
    </div>

    <!-- TAREA -->
    <div class="tarea">
      <div class="tarea-badge">📝 Práctica — Tarea</div>
      <h2>App: Directorio de Estudiantes</h2>
      <p class="tarea-desc">
        Desarrolla una aplicación Android que muestre un directorio de estudiantes mediante un RecyclerView. La app debe
        demostrar dominio del Adapter, ViewHolder y comunicación entre pantallas con Intents.
      </p>
      <div class="reqs">
        <div class="req">
          <div class="req-check"></div>
          <div>Crear una <strong>data class <code>Estudiante</code></strong> con los campos: nombre (String), carrera
            (String), semestre (Int) y promedio (Double).</div>
        </div>
        <div class="req">
          <div class="req-check"></div>
          <div>El RecyclerView debe mostrar al menos <strong>8 estudiantes</strong> con todos sus campos visibles en
            cada ítem.</div>
        </div>
        <div class="req">
          <div class="req-check"></div>
          <div>El color del promedio debe cambiar visualmente: <span style="color:#c0392b">rojo si &lt; 6.0</span>,
            <span style="color:#e67e22">amarillo si entre 6.0 y 7.9</span>, <span style="color:#1a7a4a">verde si ≥
              8.0</span>.
          </div>
        </div>
        <div class="req">
          <div class="req-check"></div>
          <div>Al hacer <strong>clic en un estudiante</strong>, navegar a una segunda Activity que muestre su perfil
            completo usando Extras del Intent.</div>
        </div>
        <div class="req">
          <div class="req-check"></div>
          <div>La segunda Activity debe permitir regresar a la lista (botón Volver o Back).</div>
        </div>
        <div class="req">
          <div class="req-check"></div>
          <div><strong>Punto extra:</strong> Agregar un EditText encima de la lista que filtre los estudiantes por
            nombre en tiempo real al escribir.</div>
        </div>
      </div>
      <div class="entrega">
        <strong>Entrega de la práctica:</strong>
        <ul>
          <li>Generar la aplicación</li>
          <li>Recepción de práctica funcional el día viernes 13 de marzo</li>
        </ul>
      </div>
    </div>

  </div>
</body>

</html>

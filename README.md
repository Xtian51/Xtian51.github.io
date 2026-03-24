<!DOCTYPE html>
<html lang="es">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Semana 3 — Fragments · Android Studio + Kotlin</title>
  <link
    href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Bebas+Neue&family=Outfit:wght@300;400;500;600&display=swap"
    rel="stylesheet">
  <style>
    :root {
      --bg: #0e0e0e;
      --surface: #161616;
      --surface2: #1f1f1f;
      --border: #2a2a2a;
      --border2: #333;
      --accent: #e8f542;
      --accent2: #42f5a7;
      --accent3: #f54242;
      --accent4: #4287f5;
      --text: #f0f0f0;
      --text-dim: #999;
      --text-muted: #555;
      --kotlin: #b08fff;
      --xml: #ff8f6b;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Outfit', sans-serif;
      font-weight: 300;
      line-height: 1.72;
    }

    /* ── HERO ── */
    .hero {
      min-height: 280px;
      background: var(--accent);
      padding: 52px 48px 44px;
      position: relative;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
    }

    .hero::before {
      content: 'SEMANA\A03';
      white-space: pre;
      position: absolute;
      top: -10px;
      right: -10px;
      font-family: 'Bebas Neue', sans-serif;
      font-size: 160px;
      line-height: 0.85;
      color: rgba(0, 0, 0, 0.07);
      pointer-events: none;
      user-select: none;
      text-align: right;
    }

    .week-tag {
      display: inline-block;
      background: #000;
      color: var(--accent);
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      font-weight: 700;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      padding: 5px 14px;
      border-radius: 2px;
      margin-bottom: 16px;
      width: fit-content;
    }

    .hero h1 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(3rem, 8vw, 6rem);
      line-height: 0.92;
      color: #000;
      margin-bottom: 16px;
      letter-spacing: 0.02em;
    }

    .hero-sub {
      color: #333;
      font-size: 1rem;
      max-width: 560px;
      margin-bottom: 28px;
      font-weight: 400;
    }

    .meta-strip {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
    }

    .meta-chip {
      background: rgba(0, 0, 0, 0.12);
      color: #222;
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 4px 12px;
      border-radius: 20px;
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
      display: flex;
      align-items: baseline;
      gap: 18px;
    }

    .clase-num {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 4rem;
      line-height: 1;
      color: var(--accent);
      flex-shrink: 0;
    }

    .clase-info {}

    .clase-eyebrow {
      font-family: 'JetBrains Mono', monospace;
      font-size: 9px;
      font-weight: 700;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      color: var(--text-muted);
      margin-bottom: 2px;
    }

    .clase-title {
      font-family: 'Outfit', sans-serif;
      font-size: 1.6rem;
      font-weight: 600;
      color: var(--text);
      line-height: 1.2;
    }

    .clase-title em {
      color: var(--accent);
      font-style: normal;
    }

    /* ── OBJETIVO ── */
    .objetivo {
      border-left: 3px solid var(--accent2);
      background: rgba(66, 245, 167, 0.06);
      border-radius: 0 6px 6px 0;
      padding: 14px 20px;
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

    .objetivo p {
      margin: 0;
      color: #bbb;
    }

    /* ── SECTION ── */
    .section {
      margin-bottom: 38px;
    }

    .section-title {
      font-family: 'Outfit', sans-serif;
      font-size: 1rem;
      font-weight: 600;
      color: var(--text);
      margin-bottom: 14px;
      display: flex;
      align-items: center;
      gap: 10px;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

    .section-title .tag {
      background: var(--accent);
      color: #000;
      font-family: 'JetBrains Mono', monospace;
      font-size: 9px;
      font-weight: 700;
      padding: 2px 8px;
      border-radius: 2px;
    }

    p {
      margin-bottom: 12px;
      color: var(--text-dim);
      font-size: 0.93rem;
    }

    /* ── FRAGMENT ANATOMY ── */
    .anatomy {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2px;
      background: var(--border);
      border-radius: 10px;
      overflow: hidden;
      margin: 20px 0;
    }

    @media(max-width:600px) {
      .anatomy {
        grid-template-columns: 1fr;
      }
    }

    .anatomy-cell {
      background: var(--surface);
      padding: 20px;
    }

    .anatomy-cell .label {
      font-family: 'JetBrains Mono', monospace;
      font-size: 9px;
      font-weight: 700;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      margin-bottom: 8px;
    }

    .anatomy-cell h4 {
      font-size: 1rem;
      font-weight: 600;
      margin-bottom: 6px;
    }

    .anatomy-cell p {
      font-size: 0.82rem;
      margin: 0;
    }

    .c-yellow .label {
      color: var(--accent);
    }

    .c-green .label {
      color: var(--accent2);
    }

    .c-red .label {
      color: var(--accent3);
    }

    .c-blue .label {
      color: var(--accent4);
    }

    /* ── LIFECYCLE STRIP ── */
    .lifecycle {
      display: flex;
      overflow-x: auto;
      gap: 0;
      margin: 20px 0;
      background: var(--surface2);
      border-radius: 8px;
      padding: 16px;
      align-items: center;
    }

    .lc-step {
      display: flex;
      flex-direction: column;
      align-items: center;
      flex-shrink: 0;
    }

    .lc-box {
      background: var(--surface);
      border: 1px solid var(--border2);
      border-radius: 6px;
      padding: 6px 12px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      font-weight: 700;
      color: var(--text-dim);
      white-space: nowrap;
    }

    .lc-box.important {
      border-color: var(--accent);
      color: var(--accent);
    }

    .lc-arrow {
      color: var(--text-muted);
      font-size: 18px;
      padding: 0 6px;
      flex-shrink: 0;
      line-height: 1;
      align-self: center;
    }

    /* ── CODE BLOCK ── */
    .code-block {
      background: #111;
      border: 1px solid var(--border2);
      border-radius: 8px;
      overflow: hidden;
      margin: 18px 0;
      font-size: 0.84rem;
    }

    .code-block pre,
    .code-body pre {
    background: transparent;
    }

    .code-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 9px 16px;
      background: var(--surface2);
      border-bottom: 1px solid var(--border);
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

    .lang-kotlin {
      background: rgba(176, 143, 255, 0.15);
      color: var(--kotlin);
      border: 1px solid rgba(176, 143, 255, 0.3);
    }

    .lang-xml {
      background: rgba(255, 143, 107, 0.15);
      color: var(--xml);
      border: 1px solid rgba(255, 143, 107, 0.3);
    }

    .code-filename {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      color: var(--text-muted);
    }

    .code-body {
      padding: 18px 20px;
      overflow-x: auto;
    }

    pre {
      font-family: 'JetBrains Mono', monospace;
      line-height: 1.65;
      white-space: pre;
      color: #ddd;
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
      color: #444;
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
      color: #e06c75;
    }

    .attr {
      color: #c3e88d;
    }

    .val {
      color: #f78c6c;
    }

    .an {
      color: #89ddff;
    }

    /* ── ALERT ── */
    .alert {
      border-radius: 6px;
      padding: 13px 17px;
      margin: 16px 0;
      font-size: 0.87rem;
      display: flex;
      gap: 12px;
      align-items: flex-start;
    }

    .alert-yellow {
      background: rgba(232, 245, 66, 0.06);
      border: 1px solid rgba(232, 245, 66, 0.2);
    }

    .alert-green {
      background: rgba(66, 245, 167, 0.06);
      border: 1px solid rgba(66, 245, 167, 0.2);
    }

    .alert-red {
      background: rgba(245, 66, 66, 0.06);
      border: 1px solid rgba(245, 66, 66, 0.2);
    }

    .alert-icon {
      font-size: 1.1rem;
      flex-shrink: 0;
      margin-top: 1px;
    }

    .alert p {
      margin: 0;
      color: #aaa;
    }

    /* ── DIVIDER ── */
    .divider {
      height: 2px;
      background: repeating-linear-gradient(90deg, var(--accent) 0, var(--accent) 8px, transparent 8px, transparent 16px);
      margin: 56px 0 0;
      opacity: 0.4;
    }

    /* ── TAREA ── */
    .tarea {
      background: var(--surface);
      border: 1px solid var(--border2);
      border-top: 4px solid var(--accent);
      border-radius: 10px;
      padding: 34px;
      margin-top: 56px;
    }

    .tarea-badge {
      display: inline-block;
      background: var(--accent);
      color: #000;
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
      font-family: 'Bebas Neue', sans-serif;
      font-size: 2.2rem;
      letter-spacing: 0.02em;
      color: var(--text);
      margin-bottom: 10px;
      line-height: 1;
    }

    .tarea-desc {
      color: var(--text-dim);
      margin-bottom: 22px;
      font-size: 0.93rem;
    }

    .reqs {
      display: flex;
      flex-direction: column;
      gap: 11px;
      margin-bottom: 24px;
    }

    .req {
      display: flex;
      gap: 12px;
      align-items: flex-start;
      font-size: 0.89rem;
      color: var(--text-dim);
    }

    .req-num {
      min-width: 22px;
      height: 22px;
      background: var(--accent);
      color: #000;
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      font-weight: 700;
      border-radius: 3px;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
      margin-top: 2px;
    }

    .req-num.star {
      background: var(--accent2);
    }

    .entrega {
      background: var(--surface2);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 13px 17px;
      font-size: 0.84rem;
    }

    .entrega strong {
      font-family: 'JetBrains Mono', monospace;
      font-size: 9px;
      color: var(--accent);
      text-transform: uppercase;
      letter-spacing: 0.12em;
      display: block;
      margin-bottom: 4px;
    }

    .entrega p {
      color: var(--text-muted);
      margin: 0;
    }

    ::-webkit-scrollbar {
      width: 5px;
      height: 5px;
    }

    ::-webkit-scrollbar-track {
      background: #111;
    }

    ::-webkit-scrollbar-thumb {
      background: #2a2a2a;
      border-radius: 3px;
    }
  </style>
</head>

<body>

  <!-- HERO -->
  <div class="hero">
    <div class="week-tag">📅 Semana 9 de 16</div>
    <h1>Fragments</h1>
    <p class="hero-sub">Construye interfaces modulares y reutilizables. Aprende el ciclo de vida, transacciones y la
      comunicación entre Fragment y Activity.</p>
    <div class="meta-strip">
      <span class="meta-chip">2 clases · 2 hrs c/u</span>
      <span class="meta-chip">Kotlin</span>
      <span class="meta-chip">ConstraintLayout</span>
      <span class="meta-chip">Prereq: Semanas 7 y 8</span>
    </div>
  </div>

  <div class="container">

    <!-- ══════════ CLASE 1 ══════════ -->
    <div class="clase-header">
      <div class="clase-num">01</div>
      <div class="clase-info">
        <div class="clase-eyebrow">Clase 01 · Semana 9</div>
        <div class="clase-title">¿Qué es un Fragment? Ciclo de vida y <em>transacciones</em></div>
      </div>
    </div>

    <div class="objetivo">
      <strong>🎯 Objetivo</strong>
      <p>Comprender qué problema resuelve un Fragment, conocer su ciclo de vida y ser capaz de agregar, reemplazar y
        remover Fragments dinámicamente desde una Activity.</p>
    </div>

    <!-- Concepto -->
    <div class="section">
      <div class="section-title"><span class="tag">CONCEPTO</span> ¿Por qué existen los Fragments?</div>
      <p>Un Fragment es una porción de interfaz de usuario con su propio ciclo de vida que vive <strong>dentro de una
          Activity</strong>. Permiten construir UIs modulares y reutilizables — el mismo Fragment puede usarse en
        múltiples Activities o mostrar contenido diferente según el tamaño de pantalla.</p>

      <div class="anatomy">
        <div class="anatomy-cell c-yellow">
          <div class="label">📱 Activity</div>
          <h4>Contenedor</h4>
          <p>Gestiona los Fragments a través del FragmentManager. Es el "host" del Fragment.</p>
        </div>
        <div class="anatomy-cell c-green">
          <div class="label">🧩 Fragment</div>
          <h4>Módulo de UI</h4>
          <p>Tiene su propio layout XML y lógica Kotlin. No puede existir sin una Activity host.</p>
        </div>
        <div class="anatomy-cell c-red">
          <div class="label">🔧 FragmentManager</div>
          <h4>Gestor</h4>
          <p>API para agregar, reemplazar y remover Fragments. Se obtiene con <code>supportFragmentManager</code>.</p>
        </div>
        <div class="anatomy-cell c-blue">
          <div class="label">📋 FragmentTransaction</div>
          <h4>Operación</h4>
          <p>Agrupa cambios en los Fragments (add, replace, remove) y los aplica con <code>commit()</code>.</p>
        </div>
      </div>
    </div>

    <!-- Ciclo de vida -->
    <div class="section">
      <div class="section-title"><span class="tag">CICLO DE VIDA</span> Métodos clave</div>
      <p>El Fragment tiene su propio ciclo de vida, pero está ligado al de su Activity. Los métodos más importantes para
        el trabajo cotidiano son:</p>
      <div class="lifecycle">
        <div class="lc-step">
          <div class="lc-box">onAttach()</div>
        </div>
        <div class="lc-arrow">→</div>
        <div class="lc-step">
          <div class="lc-box">onCreate()</div>
        </div>
        <div class="lc-arrow">→</div>
        <div class="lc-step">
          <div class="lc-box important">onCreateView()</div>
        </div>
        <div class="lc-arrow">→</div>
        <div class="lc-step">
          <div class="lc-box important">onViewCreated()</div>
        </div>
        <div class="lc-arrow">→</div>
        <div class="lc-step">
          <div class="lc-box">onStart()</div>
        </div>
        <div class="lc-arrow">→</div>
        <div class="lc-step">
          <div class="lc-box">onResume()</div>
        </div>
        <div class="lc-arrow">→</div>
        <div class="lc-step">
          <div class="lc-box">onPause()</div>
        </div>
        <div class="lc-arrow">→</div>
        <div class="lc-step">
          <div class="lc-box important">onDestroyView()</div>
        </div>
        <div class="lc-arrow">→</div>
        <div class="lc-step">
          <div class="lc-box">onDetach()</div>
        </div>
      </div>
      <div class="alert alert-yellow">
        <span class="alert-icon">💡</span>
        <p><strong>onCreateView()</strong> — aquí se infla el layout del Fragment y se retorna la View.<br>
          <strong>onViewCreated()</strong> — aquí se accede a los widgets con <code>view.findViewById()</code> o
          <code>binding</code>. Es el equivalente al <code>onCreate()</code> de una Activity.
        </p>
      </div>
    </div>

    <!-- Código 1: activity_main.xml con FrameLayout -->
    <div class="section">
      <div class="section-title"><span class="tag">XML</span> Código 1 — Layout de la Activity (contenedor)</div>
      <p>La Activity necesita un contenedor donde se mostrarán los Fragments. Se usa un
        <code>FragmentContainerView</code> o un <code>FrameLayout</code>.
      </p>
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

    <span class="cm">&lt;!-- Barra de botones para navegar entre Fragments --&gt;</span>
    <span class="tag">&lt;LinearLayout</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/barraNavegacion"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:orientation</span>=<span class="val">"horizontal"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span><span class="tag">&gt;</span>

        <span class="tag">&lt;Button</span>
            <span class="attr">android:id</span>=<span class="val">"@+id/btnFragmentInicio"</span>
            <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
            <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
            <span class="attr">android:layout_weight</span>=<span class="val">"1"</span>
            <span class="attr">android:text</span>=<span class="val">"Inicio"</span> <span class="tag">/&gt;</span>

        <span class="tag">&lt;Button</span>
            <span class="attr">android:id</span>=<span class="val">"@+id/btnFragmentPerfil"</span>
            <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
            <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
            <span class="attr">android:layout_weight</span>=<span class="val">"1"</span>
            <span class="attr">android:text</span>=<span class="val">"Perfil"</span> <span class="tag">/&gt;</span>

        <span class="tag">&lt;Button</span>
            <span class="attr">android:id</span>=<span class="val">"@+id/btnFragmentConfig"</span>
            <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
            <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
            <span class="attr">android:layout_weight</span>=<span class="val">"1"</span>
            <span class="attr">android:text</span>=<span class="val">"Config"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;/LinearLayout&gt;</span>

    <span class="cm">&lt;!-- Contenedor donde se mostrarán los Fragments --&gt;</span>
    <span class="tag">&lt;androidx.fragment.app.FragmentContainerView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/fragmentContainer"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/barraNavegacion"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre>
        </div>
      </div>
    </div>

    <!-- Código 2, 3, 4: los 3 layouts de Fragment -->
    <div class="section">
      <div class="section-title"><span class="tag">XML</span> Código 2 — Layout de InicioFragment</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-xml">XML</span>
          <span class="code-filename">res/layout/fragment_inicio.xml</span>
        </div>
        <div class="code-body">
          <pre><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"24dp"</span>
    <span class="attr">android:background</span>=<span class="val">"#FFF8E1"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvInicioTitulo"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"🏠 Pantalla de Inicio"</span>
        <span class="attr">android:textSize</span>=<span class="val">"24sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvInicioDesc"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Bienvenido a la app. Este es el Fragment de inicio."</span>
        <span class="attr">android:textSize</span>=<span class="val">"16sp"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"16dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvInicioTitulo"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnEnviarMensaje"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Enviar mensaje a la Activity"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"24dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvInicioDesc"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre>
        </div>
      </div>
    </div>

    <!-- Código 3 y 4: PerfilFragment y ConfigFragment (simplificados) -->
    <div class="section">
      <div class="section-title"><span class="tag">XML</span> Código 3 — Layouts de PerfilFragment y ConfigFragment
      </div>
      <p>Los otros dos Fragments tienen layouts similares — solo cambia el color de fondo y el texto para diferenciarlos
        visualmente.</p>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-xml">XML</span>
          <span class="code-filename">res/layout/fragment_perfil.xml &amp; fragment_config.xml</span>
        </div>
        <div class="code-body">
          <pre><span class="cm">&lt;!-- fragment_perfil.xml — misma estructura, fondo #E8F5E9 --&gt;</span>
<span class="cm">&lt;!-- Cambiar android:background="#E8F5E9" y los textos --&gt;</span>
<span class="tag">&lt;TextView</span> <span class="attr">android:text</span>=<span class="val">"👤 Perfil del Usuario"</span> ... <span class="tag">/&gt;</span>
<span class="tag">&lt;TextView</span> <span class="attr">android:id</span>=<span class="val">"@+id/tvPerfilNombre"</span>
           <span class="attr">android:text</span>=<span class="val">"Nombre: (actualizando...)"</span> ... <span class="tag">/&gt;</span>

<span class="cm">&lt;!-- fragment_config.xml — fondo #E3F2FD --&gt;</span>
<span class="tag">&lt;TextView</span> <span class="attr">android:text</span>=<span class="val">"⚙️ Configuración"</span> ... <span class="tag">/&gt;</span>
<span class="tag">&lt;Switch</span>
    <span class="attr">android:id</span>=<span class="val">"@+id/switchNotificaciones"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
    <span class="attr">android:text</span>=<span class="val">"Activar notificaciones"</span>
    <span class="attr">android:layout_marginTop</span>=<span class="val">"20dp"</span>
    <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvConfigTitulo"</span>
    <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span></pre>
        </div>
      </div>
    </div>

    <!-- Código 5: InicioFragment.kt -->
    <div class="section">
      <div class="section-title"><span class="tag">Kotlin</span> Código 4 — InicioFragment.kt</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">InicioFragment.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> androidx.fragment.app.Fragment

<span class="kw">class</span> <span class="cls">InicioFragment</span> : <span class="cls">Fragment</span>() {

    <span class="cm">// onCreateView: inflar el layout del Fragment y retornar la View</span>
    <span class="kw">override fun</span> <span class="fn">onCreateView</span>(
        inflater: <span class="cls">LayoutInflater</span>,
        container: <span class="cls">ViewGroup</span>?,
        savedInstanceState: <span class="cls">Bundle</span>?
    ): <span class="cls">View</span>? {
        <span class="kw">return</span> inflater.<span class="fn">inflate</span>(<span class="cls">R</span>.layout.fragment_inicio, container, <span class="kw">false</span>)
    }

    <span class="cm">// onViewCreated: aquí ya tenemos acceso a las vistas (NO en onCreateView)</span>
    <span class="kw">override fun</span> <span class="fn">onViewCreated</span>(view: <span class="cls">View</span>, savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onViewCreated</span>(view, savedInstanceState)

        view.<span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnEnviarMensaje).<span class="fn">setOnClickListener</span> {
            <span class="cm">// Comunicación Fragment → Activity (ver Clase 2)</span>
            <span class="cm">// Por ahora solo un Toast de prueba</span>
            android.widget.Toast.<span class="fn">makeText</span>(
                requireContext(),
                <span class="str">"Botón presionado en InicioFragment"</span>,
                android.widget.Toast.LENGTH_SHORT
            ).<span class="fn">show</span>()
        }
    }
}</pre>
        </div>
      </div>
      <div class="alert alert-red">
        <span class="alert-icon">⚠️</span>
        <p><strong>Error común:</strong> Llamar a <code>view.findViewById()</code> dentro de <code>onCreateView()</code>
          antes de retornar la vista resulta en <code>NullPointerException</code>. Siempre usar
          <code>onViewCreated()</code> para acceder a los widgets.
        </p>
      </div>
    </div>

    <!-- Código 6: MainActivity.kt con transacciones -->
    <div class="section">
      <div class="section-title"><span class="tag">Kotlin</span> Código 5 — MainActivity.kt con transacciones</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">MainActivity.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> androidx.fragment.app.Fragment

<span class="kw">class</span> <span class="cls">MainActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_main)

        <span class="cm">// Mostrar InicioFragment al arrancar (solo si es primera vez)</span>
        <span class="kw">if</span> (savedInstanceState == <span class="kw">null</span>) {
            <span class="fn">cargarFragment</span>(<span class="cls">InicioFragment</span>())
        }

        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnFragmentInicio).<span class="fn">setOnClickListener</span> {
            <span class="fn">cargarFragment</span>(<span class="cls">InicioFragment</span>())
        }
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnFragmentPerfil).<span class="fn">setOnClickListener</span> {
            <span class="fn">cargarFragment</span>(<span class="cls">PerfilFragment</span>())
        }
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnFragmentConfig).<span class="fn">setOnClickListener</span> {
            <span class="fn">cargarFragment</span>(<span class="cls">ConfigFragment</span>())
        }
    }

    <span class="cm">/**
     * Reemplaza el Fragment actual en el contenedor.
     * addToBackStack(null) permite volver con el botón Atrás.
     */</span>
    <span class="kw">private fun</span> <span class="fn">cargarFragment</span>(fragment: <span class="cls">Fragment</span>) {
        supportFragmentManager
            .<span class="fn">beginTransaction</span>()
            .<span class="fn">replace</span>(<span class="cls">R</span>.id.fragmentContainer, fragment)
            .<span class="fn">addToBackStack</span>(<span class="kw">null</span>)
            .<span class="fn">commit</span>()
    }
}</pre>
        </div>
      </div>
      <div class="alert alert-yellow">
        <span class="alert-icon">💡</span>
        <p><strong>savedInstanceState == null</strong> — sin esta condición, cada vez que el dispositivo rote la
          pantalla se agregaría una instancia nueva del Fragment al contenedor, apilando múltiples copias.</p>
      </div>
    </div>

    <!-- ══════════ CLASE 2 ══════════ -->
    <div class="divider"></div>

    <div class="clase-header">
      <div class="clase-num">02</div>
      <div class="clase-info">
        <div class="clase-eyebrow">Clase 02 · Semana 9</div>
        <div class="clase-title">Comunicación <em>Fragment ↔ Activity</em> con Interface</div>
      </div>
    </div>

    <div class="objetivo">
      <strong>🎯 Objetivo</strong>
      <p>Implementar el patrón oficial de comunicación bidireccional: Activity → Fragment (con argumentos) y Fragment →
        Activity (con Interface/Listener).</p>
    </div>

    <!-- Dirección de comunicación -->
    <div class="section">
      <div class="section-title"><span class="tag">CONCEPTO</span> Dos direcciones de comunicación</div>
      <p>Un Fragment nunca debe tener una referencia directa a la Activity o a otros Fragments — eso crea acoplamiento
        fuerte. El patrón correcto usa dos mecanismos distintos según la dirección:</p>

      <div class="anatomy">
        <div class="anatomy-cell c-yellow">
          <div class="label">Activity → Fragment</div>
          <h4>newInstance() + Bundle</h4>
          <p>Se pasan datos al Fragment al momento de crearlo, usando un <code>Bundle</code> de argumentos. El Fragment
            los lee con <code>arguments</code>.</p>
        </div>
        <div class="anatomy-cell c-green">
          <div class="label">Fragment → Activity</div>
          <h4>Interface (Listener)</h4>
          <p>El Fragment define una interfaz. La Activity la implementa. El Fragment llama métodos de la interfaz sin
            necesitar saber quién es la Activity.</p>
        </div>
      </div>
    </div>

    <!-- Código 7: PerfilFragment con newInstance y argumentos -->
    <div class="section">
      <div class="section-title"><span class="tag">Kotlin</span> Código 6 — PerfilFragment con newInstance()</div>
      <p>El patrón <code>companion object</code> + <code>newInstance()</code> es la forma idiomática en Kotlin para
        pasar datos a un Fragment.</p>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">PerfilFragment.kt</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.fragment.app.Fragment

<span class="kw">class</span> <span class="cls">PerfilFragment</span> : <span class="cls">Fragment</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreateView</span>(
        inflater: <span class="cls">LayoutInflater</span>, container: <span class="cls">ViewGroup</span>?, savedInstanceState: <span class="cls">Bundle</span>?
    ): <span class="cls">View</span>? = inflater.<span class="fn">inflate</span>(<span class="cls">R</span>.layout.fragment_perfil, container, <span class="kw">false</span>)

    <span class="kw">override fun</span> <span class="fn">onViewCreated</span>(view: <span class="cls">View</span>, savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onViewCreated</span>(view, savedInstanceState)

        <span class="cm">// Leer los argumentos que envió la Activity</span>
        <span class="kw">val</span> nombre = arguments<span class="op">?.</span><span class="fn">getString</span>(<span class="cls">ARG_NOMBRE</span>) <span class="op">?:</span> <span class="str">"Sin nombre"</span>
        <span class="kw">val</span> email  = arguments<span class="op">?.</span><span class="fn">getString</span>(<span class="cls">ARG_EMAIL</span>)  <span class="op">?:</span> <span class="str">"Sin email"</span>

        view.<span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvPerfilNombre).text = <span class="str">"Nombre: $nombre"</span>
        view.<span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvPerfilEmail).text  = <span class="str">"Email: $email"</span>
    }

    <span class="cm">// companion object: permite crear el Fragment con datos de forma segura</span>
    <span class="kw">companion object</span> {
        <span class="kw">private const val</span> <span class="cls">ARG_NOMBRE</span> = <span class="str">"ARG_NOMBRE"</span>
        <span class="kw">private const val</span> <span class="cls">ARG_EMAIL</span>  = <span class="str">"ARG_EMAIL"</span>

        <span class="cm">/**
         * Usar SIEMPRE este método en lugar del constructor directamente.
         * Los argumentos sobreviven a la rotación de pantalla; los parámetros
         * del constructor NO.
         */</span>
        <span class="kw">fun</span> <span class="fn">newInstance</span>(nombre: <span class="cls">String</span>, email: <span class="cls">String</span>): <span class="cls">PerfilFragment</span> {
            <span class="kw">val</span> fragment = <span class="cls">PerfilFragment</span>()
            <span class="kw">val</span> args = <span class="cls">Bundle</span>()
            args.<span class="fn">putString</span>(<span class="cls">ARG_NOMBRE</span>, nombre)
            args.<span class="fn">putString</span>(<span class="cls">ARG_EMAIL</span>,  email)
            fragment.arguments = args
            <span class="kw">return</span> fragment
        }
    }
}</pre>
        </div>
      </div>
    </div>

    <!-- Código 8: InicioFragment con Interface -->
    <div class="section">
      <div class="section-title"><span class="tag">Kotlin</span> Código 7 — InicioFragment con Interface Listener</div>
      <p>El Fragment define una interfaz. La Activity debe implementarla. El Fragment llama los métodos de la interfaz
        sin referenciar directamente a la Activity.</p>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">InicioFragment.kt (versión final)</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> android.content.Context
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> androidx.fragment.app.Fragment

<span class="kw">class</span> <span class="cls">InicioFragment</span> : <span class="cls">Fragment</span>() {

    <span class="cm">// ── 1. Definir la interfaz de comunicación ────────────────────────────</span>
    <span class="kw">interface</span> <span class="cls">InicioListener</span> {
        <span class="kw">fun</span> <span class="fn">onMensajeEnviado</span>(mensaje: <span class="cls">String</span>)
        <span class="kw">fun</span> <span class="fn">onNavegar</span>(destino: <span class="cls">String</span>)
    }

    <span class="cm">// ── 2. Referencia al listener (será la Activity) ──────────────────────</span>
    <span class="kw">private var</span> listener: <span class="cls">InicioListener</span>? = <span class="kw">null</span>

    <span class="cm">// ── 3. onAttach: verificar que la Activity implementa la interfaz ─────</span>
    <span class="kw">override fun</span> <span class="fn">onAttach</span>(context: <span class="cls">Context</span>) {
        <span class="kw">super</span>.<span class="fn">onAttach</span>(context)
        listener = <span class="kw">if</span> (context <span class="kw">is</span> <span class="cls">InicioListener</span>) {
            context
        } <span class="kw">else</span> {
            <span class="kw">throw</span> <span class="cls">RuntimeException</span>(<span class="str">"${context} debe implementar InicioListener"</span>)
        }
    }

    <span class="kw">override fun</span> <span class="fn">onCreateView</span>(
        inflater: <span class="cls">LayoutInflater</span>, container: <span class="cls">ViewGroup</span>?, savedInstanceState: <span class="cls">Bundle</span>?
    ): <span class="cls">View</span>? = inflater.<span class="fn">inflate</span>(<span class="cls">R</span>.layout.fragment_inicio, container, <span class="kw">false</span>)

    <span class="kw">override fun</span> <span class="fn">onViewCreated</span>(view: <span class="cls">View</span>, savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onViewCreated</span>(view, savedInstanceState)

        <span class="cm">// ── 4. Usar el listener para comunicarse con la Activity ───────────</span>
        view.<span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnEnviarMensaje).<span class="fn">setOnClickListener</span> {
            listener<span class="op">?.</span><span class="fn">onMensajeEnviado</span>(<span class="str">"Hola desde InicioFragment"</span>)
        }
    }

    <span class="cm">// ── 5. onDetach: limpiar la referencia para evitar memory leaks ───────</span>
    <span class="kw">override fun</span> <span class="fn">onDetach</span>() {
        <span class="kw">super</span>.<span class="fn">onDetach</span>()
        listener = <span class="kw">null</span>
    }
}</pre>
        </div>
      </div>
    </div>

    <!-- Código 9: MainActivity implementando la interfaz -->
    <div class="section">
      <div class="section-title"><span class="tag">Kotlin</span> Código 8 — MainActivity implementando la interfaz</div>
      <div class="code-block">
        <div class="code-header">
          <span class="code-lang lang-kotlin">Kotlin</span>
          <span class="code-filename">MainActivity.kt (versión final)</span>
        </div>
        <div class="code-body">
          <pre><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.Toast
<span class="kw">import</span> androidx.fragment.app.Fragment

<span class="cm">// La Activity implementa la interfaz definida en InicioFragment</span>
<span class="kw">class</span> <span class="cls">MainActivity</span> : <span class="cls">AppCompatActivity</span>(), <span class="cls">InicioFragment</span>.<span class="cls">InicioListener</span> {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_main)

        <span class="kw">if</span> (savedInstanceState == <span class="kw">null</span>) {
            <span class="fn">cargarFragment</span>(<span class="cls">InicioFragment</span>())
        }

        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnFragmentInicio).<span class="fn">setOnClickListener</span> {
            <span class="fn">cargarFragment</span>(<span class="cls">InicioFragment</span>())
        }
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnFragmentPerfil).<span class="fn">setOnClickListener</span> {
            <span class="cm">// Activity → Fragment: pasar datos con newInstance()</span>
            <span class="fn">cargarFragment</span>(<span class="cls">PerfilFragment</span>.<span class="fn">newInstance</span>(
                nombre = <span class="str">"Ana García"</span>,
                email  = <span class="str">"ana@email.com"</span>
            ))
        }
        <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnFragmentConfig).<span class="fn">setOnClickListener</span> {
            <span class="fn">cargarFragment</span>(<span class="cls">ConfigFragment</span>())
        }
    }

    <span class="kw">private fun</span> <span class="fn">cargarFragment</span>(fragment: <span class="cls">Fragment</span>) {
        supportFragmentManager
            .<span class="fn">beginTransaction</span>()
            .<span class="fn">replace</span>(<span class="cls">R</span>.id.fragmentContainer, fragment)
            .<span class="fn">addToBackStack</span>(<span class="kw">null</span>)
            .<span class="fn">commit</span>()
    }

    <span class="cm">// ── Implementación de InicioListener ─────────────────────────────────</span>
    <span class="kw">override fun</span> <span class="fn">onMensajeEnviado</span>(mensaje: <span class="cls">String</span>) {
        <span class="cm">// Fragment → Activity: la Activity recibe el mensaje y actúa</span>
        <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Recibido: $mensaje"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()
    }

    <span class="kw">override fun</span> <span class="fn">onNavegar</span>(destino: <span class="cls">String</span>) {
        <span class="kw">when</span> (destino) {
            <span class="str">"perfil"</span> <span class="op">-&gt;</span> <span class="fn">cargarFragment</span>(<span class="cls">PerfilFragment</span>.<span class="fn">newInstance</span>(<span class="str">"Ana García"</span>, <span class="str">"ana@email.com"</span>))
            <span class="str">"config"</span> <span class="op">-&gt;</span> <span class="fn">cargarFragment</span>(<span class="cls">ConfigFragment</span>())
            <span class="kw">else</span>      <span class="op">-&gt;</span> <span class="fn">cargarFragment</span>(<span class="cls">InicioFragment</span>())
        }
    }
}</pre>
        </div>
      </div>
      <div class="alert alert-green">
        <span class="alert-icon">💡</span>
        <p><strong>Ventaja del patrón Interface:</strong> el Fragment no importa ni referencia a
          <code>MainActivity</code>. Puede usarse con cualquier Activity que implemente <code>InicioListener</code>. Eso
          es exactamente lo que hace al Fragment <em>reutilizable</em>.
        </p>
      </div>
      <div class="alert alert-yellow">
        <span class="alert-icon">🔗</span>
        <p><strong>Conexión con semanas anteriores:</strong> El RecyclerView de la Semana 7 puede vivir dentro de un
          Fragment en lugar de una Activity. El clic del ítem puede usar
          <code>listener?.onItemSeleccionado(producto)</code> para comunicar el resultado a la Activity sin
          acoplamiento.
        </p>
      </div>
    </div>

    <!-- TAREA -->
    <div class="tarea">
      <div class="tarea-badge">📝 Práctica — Tarea</div>
      <h2>App: Panel de Estudiante</h2>
      <p class="tarea-desc">Construye una app con una sola Activity que gestione 3 Fragments usando el patrón de
        comunicación bidireccional. La app simula el panel de información de un estudiante.</p>
      <div class="reqs">
        <div class="req">
          <div class="req-num">1</div>
          <div><strong>MainActivity</strong>: contiene 3 botones de navegación (similar a una barra de tabs manual) y un
            <code>FragmentContainerView</code>. Al iniciar debe mostrar <code>ResumenFragment</code>.
          </div>
        </div>
        <div class="req">
          <div class="req-num">2</div>
          <div><strong>ResumenFragment</strong>: muestra nombre, carrera y semestre del estudiante. Estos datos deben
            recibirse desde la Activity usando <code>newInstance()</code> + <code>Bundle</code>.</div>
        </div>
        <div class="req">
          <div class="req-num">3</div>
          <div><strong>NotasFragment</strong>: muestra un RecyclerView (de la Semana 7) con la lista de materias y sus
            calificaciones. Al hacer clic en una materia, debe notificar a la Activity a través de una <strong>Interface
              Listener</strong>.</div>
        </div>
        <div class="req">
          <div class="req-num">4</div>
          <div><strong>PerfilFragment</strong>: muestra los datos completos del estudiante e incluye un botón "Editar"
            que, a través del Listener, indica a la Activity que debe lanzar una Activity de edición (usando el
            <code>ActivityResultLauncher</code> de la Semana 8).
          </div>
        </div>
        <div class="req">
          <div class="req-num">5</div>
          <div>La navegación entre Fragments debe funcionar correctamente con el botón Atrás del sistema gracias a
            <code>addToBackStack()</code>.
          </div>
        </div>
        <div class="req">
          <div class="req-num star">⭐</div>
          <div><strong>Punto extra:</strong> Cuando la Activity recibe el clic de una materia desde
            <code>NotasFragment</code>, actualizar el <code>ResumenFragment</code> para mostrar la materia seleccionada
            — demostrando comunicación Activity → Fragment de vuelta.
          </div>
        </div>
      </div>
      <div class="entrega">
        <strong>📦 Entrega</strong>
        <p>Viernes 23 de marzo. Se entregarán las capturas de los 3 Fragments activos y del RecyclerView de notas.</p>
      </div>
    </div>

  </div>
</body>

</html>

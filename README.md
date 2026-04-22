<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Semana 12 — Menús, BottomNavigation y Toolbar · Android Studio + Kotlin</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #f8f4ef;
    --surface: #ffffff;
    --surface2: #f2ede7;
    --border: #e0d8ce;
    --border2: #cdc3b6;
    --accent: #d4380d;
    --accent2: #1a6b3c;
    --accent3: #1d4ed8;
    --accent4: #7c3aed;
    --text: #1c1917;
    --text-dim: #57534e;
    --text-muted: #a8a29e;
    --kotlin: #7f52ff;
    --xml: #c2410c;
    --gradle: #1a6b3c;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: var(--bg); color: var(--text); font-family: 'Space Grotesk', sans-serif; font-weight: 300; line-height: 1.72; }

  /* ── HERO ── */
  .hero {
    background: var(--text);
    padding: 0;
    display: grid;
    grid-template-columns: 1fr auto;
    min-height: 260px;
    overflow: hidden;
  }
  .hero-left {
    padding: 52px 48px 44px;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
  }
  .hero-right {
    background: var(--accent);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 28px 36px;
    gap: 12px;
    min-width: 160px;
  }
  .hero-right .week-num {
    font-family: 'JetBrains Mono', monospace;
    font-size: 64px;
    font-weight: 700;
    color: #fff;
    line-height: 1;
  }
  .hero-right .week-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: rgba(255,255,255,0.6);
  }
  .hero-right .week-total {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: rgba(255,255,255,0.4);
  }

  .week-tag {
    display: inline-block;
    border: 1px solid rgba(212,56,13,0.4);
    background: rgba(212,56,13,0.1);
    color: #f87171;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px; font-weight: 700;
    letter-spacing: 0.14em; text-transform: uppercase;
    padding: 5px 14px; border-radius: 20px;
    margin-bottom: 18px; width: fit-content;
  }
  .hero h1 {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 700;
    color: #fff;
    line-height: 1.1;
    margin-bottom: 10px;
  }
  .hero h1 span { color: #fca5a5; }
  .hero-sub { color: #78716c; font-size: 0.95rem; max-width: 560px; margin-bottom: 28px; }
  .meta-strip { display: flex; flex-wrap: wrap; gap: 16px; border-top: 1px solid rgba(255,255,255,0.08); padding-top: 20px; }
  .meta-chip { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #44403c; display: flex; align-items: center; gap: 6px; }
  .meta-chip strong { color: #78716c; font-weight: 600; }

  .container { max-width: 980px; margin: 0 auto; padding: 0 28px 100px; }

  /* ── CLASE HEADER ── */
  .clase-header { margin: 60px 0 28px; display: flex; align-items: center; gap: 16px; }
  .clase-badge { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; background: var(--accent); color: #fff; padding: 5px 14px; border-radius: 3px; white-space: nowrap; flex-shrink: 0; }
  .clase-badge.b2 { background: var(--accent3); }
  .clase-title { font-family: 'Space Grotesk', sans-serif; font-size: 1.65rem; font-weight: 700; color: var(--text); line-height: 1.15; }
  .clase-title span { color: var(--accent); }
  .clase-title span.b { color: var(--accent3); }
  .clase-line { flex: 1; height: 1px; background: var(--border); }

  /* ── OBJETIVO ── */
  .objetivo { background: rgba(26,107,60,0.07); border: 1px solid rgba(26,107,60,0.2); border-left: 4px solid var(--accent2); border-radius: 6px; padding: 14px 20px; margin-bottom: 28px; font-size: 0.9rem; }
  .objetivo strong { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.14em; text-transform: uppercase; color: var(--accent2); display: block; margin-bottom: 5px; }
  .objetivo p { margin: 0; color: var(--text-dim); }

  /* ── SECTION ── */
  .section { margin-bottom: 36px; }
  .section-title { font-family: 'Space Grotesk', sans-serif; font-size: 0.88rem; font-weight: 600; color: var(--text); margin-bottom: 14px; display: flex; align-items: center; gap: 10px; text-transform: uppercase; letter-spacing: 0.06em; }
  .tag { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; padding: 2px 8px; border-radius: 3px; }
  .tag.kotlin  { background: rgba(127,82,255,0.15); color: var(--kotlin); border: 1px solid rgba(127,82,255,0.3); }
  .tag.xml     { background: rgba(194,65,12,0.15);  color: var(--xml);    border: 1px solid rgba(194,65,12,0.3); }
  .tag.gradle  { background: rgba(26,107,60,0.15);  color: var(--gradle); border: 1px solid rgba(26,107,60,0.3); }
  .tag.concept { background: rgba(212,56,13,0.12);  color: var(--accent); border: 1px solid rgba(212,56,13,0.25); }

  p { margin-bottom: 12px; color: var(--text-dim); font-size: 0.93rem; }

  /* ── CONCEPTS GRID ── */
  .concepts { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px,1fr)); gap: 12px; margin: 18px 0; }
  .concept-card { background: var(--surface); border: 1px solid var(--border); border-radius: 8px; padding: 16px; border-left: 4px solid var(--accent); }
  .concept-card.green { border-left-color: var(--accent2); }
  .concept-card.blue  { border-left-color: var(--accent3); }
  .concept-card .icon { font-size: 1.3rem; margin-bottom: 8px; }
  .concept-card h4 { font-family: 'JetBrains Mono', monospace; font-size: 0.78rem; color: var(--accent); margin-bottom: 5px; font-weight: 700; }
  .concept-card.green h4 { color: var(--accent2); }
  .concept-card.blue  h4 { color: var(--accent3); }
  .concept-card p { font-size: 0.82rem; margin: 0; }

  /* ── CODE BLOCK ── */
  .code-block { background: #1c1917; border: 1px solid #2d2925; border-radius: 8px; overflow: hidden; margin: 16px 0; font-size: 0.84rem; }
  .code-header { display: flex; align-items: center; justify-content: space-between; padding: 9px 16px; background: #252220; border-bottom: 1px solid #2d2925; }
  .code-lang { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; padding: 2px 9px; border-radius: 3px; }
  .lang-kotlin { background: rgba(127,82,255,0.2); color: #b08fff; border: 1px solid rgba(127,82,255,0.3); }
  .lang-xml    { background: rgba(194,65,12,0.2);  color: #fb923c; border: 1px solid rgba(194,65,12,0.3); }
  .lang-gradle { background: rgba(26,107,60,0.2);  color: #6ee7b7; border: 1px solid rgba(26,107,60,0.3); }
  .code-filename { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #57534e; }
  .code-body { padding: 18px 20px; overflow-x: auto; }
  pre { font-family: 'JetBrains Mono', monospace; line-height: 1.65; white-space: pre; color: #d6d3d1; background: transparent; }
  .kw  { color: #c792ea; } .fn  { color: #82aaff; } .str { color: #c3e88d; }
  .cm  { color: #44403c; font-style: italic; } .num { color: #f78c6c; }
  .cls { color: #ffcb6b; } .op  { color: #89ddff; }
  .tag-c { color: #e06c75; } .attr { color: #c3e88d; } .val { color: #f78c6c; } .an { color: #89ddff; }

  /* ── ALERT ── */
  .alert { border-radius: 6px; padding: 13px 17px; margin: 14px 0; font-size: 0.87rem; display: flex; gap: 12px; align-items: flex-start; }
  .alert-red    { background: rgba(212,56,13,0.06);  border: 1px solid rgba(212,56,13,0.2); }
  .alert-green  { background: rgba(26,107,60,0.06);  border: 1px solid rgba(26,107,60,0.2); }
  .alert-blue   { background: rgba(29,78,216,0.06);  border: 1px solid rgba(29,78,216,0.2); }
  .alert-orange { background: rgba(245,158,11,0.06); border: 1px solid rgba(245,158,11,0.2); }
  .alert-icon   { font-size: 1.1rem; flex-shrink: 0; margin-top: 1px; }
  .alert p      { margin: 0; }

  /* ── DIVIDER ── */
  .divider { margin: 56px 0 0; border: none; border-top: 2px solid var(--border2); position: relative; }
  .divider::after { content: 'CLASE 02'; position: absolute; top: -10px; left: 50%; transform: translateX(-50%); background: var(--bg); padding: 0 14px; font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; color: var(--text-muted); }

  /* ── TAREA ── */
  .tarea { background: var(--text); border-radius: 10px; padding: 34px; margin-top: 56px; position: relative; overflow: hidden; }
  .tarea::after { content: '12'; position: absolute; right: -10px; bottom: -30px; font-family: 'Space Grotesk', sans-serif; font-size: 180px; font-weight: 700; color: rgba(255,255,255,0.03); line-height: 1; pointer-events: none; }
  .tarea-badge { display: inline-block; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; padding: 4px 12px; border-radius: 3px; margin-bottom: 14px; }
  .tarea h2 { font-family: 'Space Grotesk', sans-serif; font-size: 1.8rem; font-weight: 700; color: #fff; margin-bottom: 10px; }
  .tarea-desc { color: #78716c; margin-bottom: 22px; font-size: 0.93rem; }
  .reqs { display: flex; flex-direction: column; gap: 10px; margin-bottom: 22px; }
  .req { display: flex; gap: 12px; align-items: flex-start; font-size: 0.89rem; color: #a8a29e; }
  .req-num { min-width: 22px; height: 22px; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 10px; font-weight: 700; border-radius: 3px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 2px; }
  .req-num.star { background: var(--accent2); }
  .entrega { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 6px; padding: 13px 17px; font-size: 0.84rem; }
  .entrega strong { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: #fca5a5; text-transform: uppercase; letter-spacing: 0.12em; display: block; margin-bottom: 4px; }
  .entrega p { color: #44403c; margin: 0; }

  ::-webkit-scrollbar { width: 5px; height: 5px; }
  ::-webkit-scrollbar-track { background: #252220; }
  ::-webkit-scrollbar-thumb { background: #44403c; border-radius: 3px; }
</style>
</head>
<body>

<div class="hero">
  <div class="hero-left">
    <div class="week-tag">📅 Semana 12 de 16</div>
    <h1>Menús, Toolbar<br><span>y BottomNavigation</span></h1>
    <p class="hero-sub">Construye una navegación profesional con barra inferior, opciones de menú contextuales y una Toolbar personalizada que integra todo el flujo de la app.</p>
    <div class="meta-strip">
      <div class="meta-chip">Clases <strong>2 × 2 hrs</strong></div>
      <div class="meta-chip">Lenguaje <strong>Kotlin</strong></div>
      <div class="meta-chip">Layout <strong>ConstraintLayout</strong></div>
      <div class="meta-chip">Prereq <strong>Semanas 9 y 10</strong></div>
    </div>
  </div>
  <div class="hero-right">
    <span class="week-label">semana</span>
    <span class="week-num">12</span>
    <span class="week-total">de 16</span>
  </div>
</div>

<div class="container">

  <!-- ══════════════════ CLASE 1 ══════════════════ -->
  <div class="clase-header">
    <span class="clase-badge">Clase 01</span>
    <div class="clase-title">Toolbar y <span>Options Menu</span></div>
    <div class="clase-line"></div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Personalizar la Toolbar de la app, agregar un menú de opciones con íconos y manejar los eventos de cada ítem del menú.</p>
  </div>

  <div class="section">
    <div class="section-title"><span class="tag concept">CONCEPTO</span> Tipos de menú en Android</div>
    <div class="concepts">
      <div class="concept-card">
        <div class="icon">⋮</div>
        <h4>Options Menu</h4>
        <p>Aparece en la Toolbar. Opciones globales de la pantalla: buscar, filtrar, configurar.</p>
      </div>
      <div class="concept-card green">
        <div class="icon">👆</div>
        <h4>Context Menu</h4>
        <p>Aparece al hacer long-press sobre un elemento. Acciones específicas de ese ítem.</p>
      </div>
      <div class="concept-card blue">
        <div class="icon">⬇️</div>
        <h4>BottomNavigation</h4>
        <p>Barra fija en la parte inferior. Navega entre las secciones principales de la app.</p>
      </div>
    </div>
  </div>

  <!-- Código 1: build.gradle -->
  <div class="section">
    <div class="section-title"><span class="tag gradle">GRADLE</span> Código 1 — Dependencias</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-gradle">Gradle · Kotlin DSL</span>
        <span class="code-filename">build.gradle.kts (Module)</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="fn">dependencies</span> {
    <span class="cm">// Material Design — necesario para Toolbar y BottomNavigationView</span>
    <span class="fn">implementation</span>(<span class="str">"com.google.android.material:material:1.12.0"</span>)

    <span class="cm">// Activity KTX (de Semana 10)</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.activity:activity-ktx:1.9.0"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.fragment:fragment-ktx:1.7.0"</span>)
}</pre></div>
    </div>
  </div>

  <!-- Código 2: themes.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 2 — themes.xml (NoActionBar)</div>
    <p>Para usar una Toolbar personalizada hay que deshabilitar la ActionBar por defecto del tema. De lo contrario aparecerán dos barras.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/values/themes.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;resources&gt;</span>
    <span class="cm">&lt;!-- NoActionBar: quita la barra por defecto para usar Toolbar propia --&gt;</span>
    <span class="tag-c">&lt;style</span> <span class="attr">name</span>=<span class="val">"Theme.MiApp"</span>
           <span class="attr">parent</span>=<span class="val">"Theme.MaterialComponents.Light.NoActionBar"</span><span class="tag-c">&gt;</span>
        <span class="tag-c">&lt;item</span> <span class="attr">name</span>=<span class="val">"colorPrimary"</span><span class="tag-c">&gt;</span>@color/purple_500<span class="tag-c">&lt;/item&gt;</span>
        <span class="tag-c">&lt;item</span> <span class="attr">name</span>=<span class="val">"colorPrimaryVariant"</span><span class="tag-c">&gt;</span>@color/purple_700<span class="tag-c">&lt;/item&gt;</span>
        <span class="tag-c">&lt;item</span> <span class="attr">name</span>=<span class="val">"colorOnPrimary"</span><span class="tag-c">&gt;</span>@color/white<span class="tag-c">&lt;/item&gt;</span>
    <span class="tag-c">&lt;/style&gt;</span>
<span class="tag-c">&lt;/resources&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 3: menu_principal.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 3 — menu_principal.xml (Options Menu)</div>
    <p>Los archivos de menú se crean en <code>res/menu/</code>. Clic derecho sobre <code>res</code> → New → Android Resource File → Resource type: Menu.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/menu/menu_principal.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag-c">?&gt;</span>
<span class="tag-c">&lt;menu</span> <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
      <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span><span class="tag-c">&gt;</span>

    <span class="cm">&lt;!-- showAsAction: ifRoom = muestra como ícono si hay espacio; never = en el menú desplegable --&gt;</span>
    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/menuBuscar"</span>
        <span class="attr">android:title</span>=<span class="val">"Buscar"</span>
        <span class="attr">android:icon</span>=<span class="val">"@android:drawable/ic_menu_search"</span>
        <span class="attr">app:showAsAction</span>=<span class="val">"ifRoom"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/menuOrdenar"</span>
        <span class="attr">android:title</span>=<span class="val">"Ordenar"</span>
        <span class="attr">app:showAsAction</span>=<span class="val">"never"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/menuEliminarTodos"</span>
        <span class="attr">android:title</span>=<span class="val">"Eliminar todo"</span>
        <span class="attr">app:showAsAction</span>=<span class="val">"never"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/menu&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 4: activity_main.xml con Toolbar -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 4 — activity_main.xml con Toolbar</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_main.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag-c">?&gt;</span>
<span class="tag-c">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span><span class="tag-c">&gt;</span>

    <span class="cm">&lt;!-- Toolbar personalizada reemplaza la ActionBar del sistema --&gt;</span>
    <span class="tag-c">&lt;androidx.appcompat.widget.Toolbar</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/toolbar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"?attr/actionBarSize"</span>
        <span class="attr">android:background</span>=<span class="val">"?attr/colorPrimary"</span>
        <span class="attr">android:elevation</span>=<span class="val">"4dp"</span>
        <span class="attr">app:title</span>=<span class="val">"Mi App"</span>
        <span class="attr">app:titleTextColor</span>=<span class="val">"@android:color/white"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

    <span class="cm">&lt;!-- Contenido principal --&gt;</span>
    <span class="tag-c">&lt;androidx.recyclerview.widget.RecyclerView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/recyclerView"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">android:clipToPadding</span>=<span class="val">"false"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/toolbar"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 5: MainActivity con Toolbar y Options Menu -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 5 — MainActivity.kt (Toolbar + Options Menu)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">MainActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.Menu
<span class="kw">import</span> android.view.MenuItem
<span class="kw">import</span> android.widget.Toast
<span class="kw">import</span> androidx.appcompat.widget.Toolbar

<span class="kw">class</span> <span class="cls">MainActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_main)

        <span class="cm">// Registrar la Toolbar como ActionBar de la Activity</span>
        <span class="kw">val</span> toolbar = <span class="fn">findViewById</span>&lt;<span class="cls">Toolbar</span>&gt;(<span class="cls">R</span>.id.toolbar)
        <span class="fn">setSupportActionBar</span>(toolbar)

        <span class="cm">// Opcional: mostrar botón de retroceso si es una pantalla secundaria</span>
        <span class="cm">// supportActionBar?.setDisplayHomeAsUpEnabled(true)</span>
    }

    <span class="cm">// ── 1. Inflar el menú XML en la Toolbar ─────────────────────────────</span>
    <span class="kw">override fun</span> <span class="fn">onCreateOptionsMenu</span>(menu: <span class="cls">Menu</span>): <span class="cls">Boolean</span> {
        menuInflater.<span class="fn">inflate</span>(<span class="cls">R</span>.menu.menu_principal, menu)
        <span class="kw">return true</span>  <span class="cm">// true = mostrar el menú</span>
    }

    <span class="cm">// ── 2. Manejar clics en los ítems del menú ───────────────────────────</span>
    <span class="kw">override fun</span> <span class="fn">onOptionsItemSelected</span>(item: <span class="cls">MenuItem</span>): <span class="cls">Boolean</span> {
        <span class="kw">return when</span> (item.itemId) {
            <span class="cls">R</span>.id.menuBuscar <span class="op">-&gt;</span> {
                <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Buscar presionado"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()
                <span class="kw">true</span>
            }
            <span class="cls">R</span>.id.menuOrdenar <span class="op">-&gt;</span> {
                <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Ordenar presionado"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()
                <span class="kw">true</span>
            }
            <span class="cls">R</span>.id.menuEliminarTodos <span class="op">-&gt;</span> {
                <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Eliminar todo presionado"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()
                <span class="kw">true</span>
            }
            <span class="kw">else</span> <span class="op">-&gt;</span> <span class="kw">super</span>.<span class="fn">onOptionsItemSelected</span>(item)
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-red">
      <span class="alert-icon">⚠️</span>
      <p><strong>return true vs super:</strong> Retornar <code>true</code> indica que el evento fue manejado. El <code>else -> super.onOptionsItemSelected(item)</code> es obligatorio para que los ítems del sistema (como el botón de retroceso) sigan funcionando.</p>
    </div>
  </div>

  <!-- Código 6: Context Menu en RecyclerView -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 6 — menu_contexto.xml (Context Menu)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/menu/menu_contexto.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag-c">?&gt;</span>
<span class="tag-c">&lt;menu</span> <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span><span class="tag-c">&gt;</span>

    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/ctxEditar"</span>
        <span class="attr">android:title</span>=<span class="val">"✏️ Editar"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/ctxEliminar"</span>
        <span class="attr">android:title</span>=<span class="val">"🗑️ Eliminar"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/ctxCompartir"</span>
        <span class="attr">android:title</span>=<span class="val">"↗️ Compartir"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/menu&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 7: Context Menu en MainActivity -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 7 — Context Menu en Activity</div>
    <p>El Context Menu requiere registrar la vista y sobrescribir dos métodos: <code>onCreateContextMenu</code> para inflar el menú y <code>onContextItemSelected</code> para manejar los clics.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">MainActivity.kt — agregar al onCreate y añadir estos métodos</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> android.view.ContextMenu
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.widget.TextView

<span class="cm">// ── Dentro de onCreate ───────────────────────────────────────────────────</span>

<span class="kw">val</span> tvItem = <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvItemEjemplo)

<span class="cm">// Registrar la vista para recibir el Context Menu (long press)</span>
<span class="fn">registerForContextMenu</span>(tvItem)

<span class="cm">// ── Métodos fuera del onCreate ───────────────────────────────────────────</span>

<span class="kw">override fun</span> <span class="fn">onCreateContextMenu</span>(
    menu: <span class="cls">ContextMenu</span>,
    v: <span class="cls">View</span>,
    menuInfo: <span class="cls">ContextMenu</span>.<span class="cls">ContextMenuInfo</span>?
) {
    <span class="kw">super</span>.<span class="fn">onCreateContextMenu</span>(menu, v, menuInfo)
    menu.setHeaderTitle(<span class="str">"Opciones del ítem"</span>)
    menuInflater.<span class="fn">inflate</span>(<span class="cls">R</span>.menu.menu_contexto, menu)
}

<span class="kw">override fun</span> <span class="fn">onContextItemSelected</span>(item: <span class="cls">MenuItem</span>): <span class="cls">Boolean</span> {
    <span class="kw">return when</span> (item.itemId) {
        <span class="cls">R</span>.id.ctxEditar    <span class="op">-&gt;</span> {
            <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Editar ítem"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()
            <span class="kw">true</span>
        }
        <span class="cls">R</span>.id.ctxEliminar  <span class="op">-&gt;</span> {
            <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Eliminar ítem"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()
            <span class="kw">true</span>
        }
        <span class="cls">R</span>.id.ctxCompartir <span class="op">-&gt;</span> {
            <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Compartir ítem"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>()
            <span class="kw">true</span>
        }
        <span class="kw">else</span> <span class="op">-&gt;</span> <span class="kw">super</span>.<span class="fn">onContextItemSelected</span>(item)
    }
}</pre></div>
    </div>
    <div class="alert alert-blue">
      <span class="alert-icon">💡</span>
      <p><strong>Context Menu en RecyclerView:</strong> Para usarlo con ítems del RecyclerView, llamar <code>registerForContextMenu(recyclerView)</code> y en el <code>onContextItemSelected</code> usar <code>AdapterView.AdapterContextMenuInfo</code> para obtener la posición del ítem seleccionado.</p>
    </div>
  </div>

  <!-- ══════════════════ CLASE 2 ══════════════════ -->
  <hr class="divider">

  <div class="clase-header" style="margin-top:56px">
    <span class="clase-badge b2">Clase 02</span>
    <div class="clase-title"><span class="b">BottomNavigationView</span> con Fragments</div>
    <div class="clase-line"></div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Integrar <code>BottomNavigationView</code> con Fragments para construir una navegación de tipo "app real" con secciones independientes, recordando la pestaña activa al rotar.</p>
  </div>

  <!-- Código 8: menu_bottom_nav.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 8 — menu_bottom_nav.xml</div>
    <p>La BottomNavigationView también usa un archivo de menú para definir sus ítems, pero cada ítem debe tener un ícono obligatoriamente.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/menu/menu_bottom_nav.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag-c">?&gt;</span>
<span class="tag-c">&lt;menu</span> <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span><span class="tag-c">&gt;</span>

    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/navInicio"</span>
        <span class="attr">android:title</span>=<span class="val">"Inicio"</span>
        <span class="attr">android:icon</span>=<span class="val">"@android:drawable/ic_menu_myplaces"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/navBuscar"</span>
        <span class="attr">android:title</span>=<span class="val">"Buscar"</span>
        <span class="attr">android:icon</span>=<span class="val">"@android:drawable/ic_menu_search"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;item</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/navPerfil"</span>
        <span class="attr">android:title</span>=<span class="val">"Perfil"</span>
        <span class="attr">android:icon</span>=<span class="val">"@android:drawable/ic_menu_myplaces"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/menu&gt;</span></pre></div>
    </div>
    <div class="alert alert-orange">
      <span class="alert-icon">💡</span>
      <p>Los íconos de sistema (<code>@android:drawable/</code>) funcionan para el ejemplo pero son limitados y pueden verse desactualizados. En un proyecto real se usan íconos de Material Design: clic derecho sobre <code>res</code> → New → Vector Asset → Material Icons.</p>
    </div>
  </div>

  <!-- Código 9: activity_main.xml con BottomNavigation -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 9 — activity_main.xml con BottomNavigationView</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_main.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag-c">?&gt;</span>
<span class="tag-c">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span><span class="tag-c">&gt;</span>

    <span class="tag-c">&lt;androidx.appcompat.widget.Toolbar</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/toolbar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"?attr/actionBarSize"</span>
        <span class="attr">android:background</span>=<span class="val">"?attr/colorPrimary"</span>
        <span class="attr">android:elevation</span>=<span class="val">"4dp"</span>
        <span class="attr">app:titleTextColor</span>=<span class="val">"@android:color/white"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

    <span class="cm">&lt;!-- Contenedor de Fragments entre Toolbar y BottomNav --&gt;</span>
    <span class="tag-c">&lt;androidx.fragment.app.FragmentContainerView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/fragmentContainer"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/toolbar"</span>
        <span class="attr">app:layout_constraintBottom_toTopOf</span>=<span class="val">"@id/bottomNav"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

    <span class="cm">&lt;!-- BottomNavigationView anclada al fondo --&gt;</span>
    <span class="tag-c">&lt;com.google.android.material.bottomnavigation.BottomNavigationView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/bottomNav"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">app:menu</span>=<span class="val">"@menu/menu_bottom_nav"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 10: Los 3 Fragments (layouts) -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 10 — Layouts de los 3 Fragments</div>
    <p>Cada sección de la BottomNav tiene su propio Fragment. Los layouts son simples — lo importante es que tengan IDs únicos.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">fragment_inicio.xml / fragment_buscar.xml / fragment_perfil.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="cm">&lt;!-- fragment_inicio.xml --&gt;</span>
<span class="tag-c">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"24dp"</span><span class="tag-c">&gt;</span>

    <span class="tag-c">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvInicioTitulo"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"🏠 Inicio"</span>
        <span class="attr">android:textSize</span>=<span class="val">"28sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span>

<span class="cm">&lt;!-- fragment_buscar.xml: misma estructura, texto "🔍 Buscar" --&gt;
&lt;!-- fragment_perfil.xml: misma estructura, texto "👤 Perfil" --&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 11: Los 3 Fragments .kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 11 — InicioFragment, BuscarFragment, PerfilFragment</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">InicioFragment.kt / BuscarFragment.kt / PerfilFragment.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="cm">// InicioFragment.kt</span>
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> androidx.fragment.app.Fragment

<span class="kw">class</span> <span class="cls">InicioFragment</span> : <span class="cls">Fragment</span>() {
    <span class="kw">override fun</span> <span class="fn">onCreateView</span>(
        inflater: <span class="cls">LayoutInflater</span>, container: <span class="cls">ViewGroup</span>?, savedInstanceState: <span class="cls">Bundle</span>?
    ): <span class="cls">View</span>? = inflater.<span class="fn">inflate</span>(<span class="cls">R</span>.layout.fragment_inicio, container, <span class="kw">false</span>)
}

<span class="cm">// BuscarFragment.kt — misma estructura con R.layout.fragment_buscar</span>
<span class="kw">class</span> <span class="cls">BuscarFragment</span> : <span class="cls">Fragment</span>() {
    <span class="kw">override fun</span> <span class="fn">onCreateView</span>(
        inflater: <span class="cls">LayoutInflater</span>, container: <span class="cls">ViewGroup</span>?, savedInstanceState: <span class="cls">Bundle</span>?
    ): <span class="cls">View</span>? = inflater.<span class="fn">inflate</span>(<span class="cls">R</span>.layout.fragment_buscar, container, <span class="kw">false</span>)
}

<span class="cm">// PerfilFragment.kt — misma estructura con R.layout.fragment_perfil</span>
<span class="kw">class</span> <span class="cls">PerfilFragment</span> : <span class="cls">Fragment</span>() {
    <span class="kw">override fun</span> <span class="fn">onCreateView</span>(
        inflater: <span class="cls">LayoutInflater</span>, container: <span class="cls">ViewGroup</span>?, savedInstanceState: <span class="cls">Bundle</span>?
    ): <span class="cls">View</span>? = inflater.<span class="fn">inflate</span>(<span class="cls">R</span>.layout.fragment_perfil, container, <span class="kw">false</span>)
}</pre></div>
    </div>
  </div>

  <!-- Código 12: MainActivity final con todo integrado -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 12 — MainActivity.kt (versión final completa)</div>
    <p>La Activity final integra Toolbar, Options Menu y BottomNavigationView. El título de la Toolbar cambia dinámicamente según la sección activa.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">MainActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.Menu
<span class="kw">import</span> android.view.MenuItem
<span class="kw">import</span> android.widget.Toast
<span class="kw">import</span> androidx.appcompat.widget.Toolbar
<span class="kw">import</span> androidx.fragment.app.Fragment
<span class="kw">import</span> com.google.android.material.bottomnavigation.BottomNavigationView

<span class="kw">class</span> <span class="cls">MainActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">private lateinit var</span> toolbar: <span class="cls">Toolbar</span>

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_main)

        <span class="cm">// ── Toolbar ──────────────────────────────────────────────────────</span>
        toolbar = <span class="fn">findViewById</span>(<span class="cls">R</span>.id.toolbar)
        <span class="fn">setSupportActionBar</span>(toolbar)

        <span class="cm">// ── Fragment inicial (solo si no hay estado guardado) ─────────────</span>
        <span class="kw">if</span> (savedInstanceState == <span class="kw">null</span>) {
            <span class="fn">cargarFragment</span>(<span class="cls">InicioFragment</span>(), <span class="str">"Inicio"</span>)
        }

        <span class="cm">// ── BottomNavigationView ─────────────────────────────────────────</span>
        <span class="fn">findViewById</span>&lt;<span class="cls">BottomNavigationView</span>&gt;(<span class="cls">R</span>.id.bottomNav)
            .<span class="fn">setOnItemSelectedListener</span> { item <span class="op">-&gt;</span>
                <span class="kw">when</span> (item.itemId) {
                    <span class="cls">R</span>.id.navInicio <span class="op">-&gt;</span> { <span class="fn">cargarFragment</span>(<span class="cls">InicioFragment</span>(), <span class="str">"Inicio"</span>);  <span class="kw">true</span> }
                    <span class="cls">R</span>.id.navBuscar <span class="op">-&gt;</span> { <span class="fn">cargarFragment</span>(<span class="cls">BuscarFragment</span>(), <span class="str">"Buscar"</span>);  <span class="kw">true</span> }
                    <span class="cls">R</span>.id.navPerfil <span class="op">-&gt;</span> { <span class="fn">cargarFragment</span>(<span class="cls">PerfilFragment</span>(), <span class="str">"Perfil"</span>);  <span class="kw">true</span> }
                    <span class="kw">else</span>           <span class="op">-&gt;</span> <span class="kw">false</span>
                }
            }
    }

    <span class="kw">private fun</span> <span class="fn">cargarFragment</span>(fragment: <span class="cls">Fragment</span>, titulo: <span class="cls">String</span>) {
        <span class="cm">// Actualizar el título de la Toolbar al cambiar de sección</span>
        supportActionBar<span class="op">?.</span>title = titulo

        supportFragmentManager
            .<span class="fn">beginTransaction</span>()
            .<span class="fn">replace</span>(<span class="cls">R</span>.id.fragmentContainer, fragment)
            .<span class="cm">// NO se llama addToBackStack — la BottomNav no debe tener historial de Atrás</span>
            <span class="fn">commit</span>()
    }

    <span class="cm">// ── Options Menu ─────────────────────────────────────────────────────</span>
    <span class="kw">override fun</span> <span class="fn">onCreateOptionsMenu</span>(menu: <span class="cls">Menu</span>): <span class="cls">Boolean</span> {
        menuInflater.<span class="fn">inflate</span>(<span class="cls">R</span>.menu.menu_principal, menu)
        <span class="kw">return true</span>
    }

    <span class="kw">override fun</span> <span class="fn">onOptionsItemSelected</span>(item: <span class="cls">MenuItem</span>): <span class="cls">Boolean</span> {
        <span class="kw">return when</span> (item.itemId) {
            <span class="cls">R</span>.id.menuBuscar       <span class="op">-&gt;</span> { <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Buscar"</span>,         <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>(); <span class="kw">true</span> }
            <span class="cls">R</span>.id.menuOrdenar      <span class="op">-&gt;</span> { <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Ordenar"</span>,        <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>(); <span class="kw">true</span> }
            <span class="cls">R</span>.id.menuEliminarTodos <span class="op">-&gt;</span> { <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Eliminar todo"</span>, <span class="cls">Toast</span>.LENGTH_SHORT).<span class="fn">show</span>(); <span class="kw">true</span> }
            <span class="kw">else</span>                  <span class="op">-&gt;</span> <span class="kw">super</span>.<span class="fn">onOptionsItemSelected</span>(item)
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-green">
      <span class="alert-icon">💡</span>
      <p><strong>Sin addToBackStack en BottomNav:</strong> A diferencia de los Fragments de la Semana 9, aquí NO se llama <code>addToBackStack()</code>. Las secciones de una BottomNav son destinos paralelos — el usuario no "navega de vuelta" entre ellas con el botón Atrás; el botón Atrás debe cerrar la app o subir un nivel, no alternar pestañas.</p>
    </div>
  </div>

  <!-- Código 13: AndroidManifest -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 13 — AndroidManifest.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">AndroidManifest.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;manifest</span> <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span><span class="tag-c">&gt;</span>
    <span class="tag-c">&lt;application</span>
        <span class="attr">android:allowBackup</span>=<span class="val">"true"</span>
        <span class="cm">&lt;!-- Aplicar el tema NoActionBar --&gt;</span>
        <span class="attr">android:theme</span>=<span class="val">"@style/Theme.MiApp"</span><span class="tag-c">&gt;</span>

        <span class="tag-c">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".MainActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"true"</span><span class="tag-c">&gt;</span>
            <span class="tag-c">&lt;intent-filter&gt;</span>
                <span class="tag-c">&lt;action</span> <span class="attr">android:name</span>=<span class="val">"android.intent.action.MAIN"</span> <span class="tag-c">/&gt;</span>
                <span class="tag-c">&lt;category</span> <span class="attr">android:name</span>=<span class="val">"android.intent.category.LAUNCHER"</span> <span class="tag-c">/&gt;</span>
            <span class="tag-c">&lt;/intent-filter&gt;</span>
        <span class="tag-c">&lt;/activity&gt;</span>

    <span class="tag-c">&lt;/application&gt;</span>
<span class="tag-c">&lt;/manifest&gt;</span></pre></div>
    </div>
    <div class="alert alert-red">
      <span class="alert-icon">⚠️</span>
      <p><strong>Error frecuente:</strong> Si el tema en el Manifest no es <code>NoActionBar</code> y se llama <code>setSupportActionBar(toolbar)</code>, la app lanza una excepción al iniciar: <em>"This Activity already has an action bar supplied by the window decor."</em> Siempre verificar el tema antes de correr.</p>
    </div>
  </div>

  <!-- TAREA -->
  <div class="tarea">
    <div class="tarea-badge">📝 Práctica — Tarea</div>
    <h2>App: Gestor de Recetas</h2>
    <p class="tarea-desc">Rediseña la app de la Semana 11 (o crea una nueva app de recetas) aplicando navegación profesional con Toolbar, Options Menu y BottomNavigationView.</p>
    <div class="reqs">
      <div class="req"><div class="req-num">1</div><div>La app debe tener una <strong>Toolbar personalizada</strong> cuyo título cambie dinámicamente según la sección activa. El tema debe ser <code>NoActionBar</code>.</div></div>
      <div class="req"><div class="req-num">2</div><div>Implementar un <strong>Options Menu</strong> con al menos 3 ítems: uno visible como ícono en la Toolbar (<code>showAsAction="ifRoom"</code>) y dos en el menú desplegable (<code>showAsAction="never"</code>).</div></div>
      <div class="req"><div class="req-num">3</div><div>La <strong>BottomNavigationView</strong> debe tener 3 secciones: "Recetas" (lista con RecyclerView), "Favoritos" (lista filtrada) y "Perfil" (info del usuario). Cada sección es un Fragment independiente.</div></div>
      <div class="req"><div class="req-num">4</div><div>Implementar un <strong>Context Menu</strong> sobre los ítems del RecyclerView de recetas, con las opciones: "Ver detalle", "Agregar a favoritos" y "Eliminar".</div></div>
      <div class="req"><div class="req-num">5</div><div>Al rotar el dispositivo, la <strong>sección activa de la BottomNav debe recordarse</strong> — usar <code>savedInstanceState</code> en la Activity para guardar y restaurar el ítem seleccionado.</div></div>
      <div class="req"><div class="req-num star">⭐</div><div><strong>Punto extra:</strong> En el Fragment de "Recetas", conectar el ítem de búsqueda del Options Menu para filtrar la lista del RecyclerView en tiempo real usando la Interface Listener de la Semana 9.</div></div>
    </div>
    <div class="entrega">
      <strong>--- Entrega ---</strong>
      <p>Capturas mostrando las 3 secciones, el Options Menu desplegado y el Context Menu activo sobre un ítem.</p>
    </div>
  </div>

</div>
</body>
</html>

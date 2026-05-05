<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Semana 14 — Retrofit + Coroutines · Android Studio + Kotlin</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Unbounded:wght@400;700;900&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #fefce8;
    --surface: #ffffff;
    --surface2: #fef9c3;
    --border: #fde047;
    --border2: #eab308;
    --accent: #ca8a04;
    --accent2: #15803d;
    --accent3: #1d4ed8;
    --accent4: #dc2626;
    --text: #1c1917;
    --text-dim: #57534e;
    --text-muted: #a8a29e;
    --kotlin: #7f52ff;
    --xml: #c2410c;
    --gradle: #15803d;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: var(--bg); color: var(--text); font-family: 'Inter', sans-serif; font-weight: 300; line-height: 1.72; }

  /* ── HERO ── */
  .hero {
    background: var(--text);
    padding: 56px 48px 48px;
    position: relative;
    overflow: hidden;
  }
  .hero::after {
    content: 'API';
    position: absolute;
    right: -20px; bottom: -30px;
    font-family: 'Unbounded', sans-serif;
    font-size: 220px;
    font-weight: 900;
    color: rgba(255,255,255,0.03);
    line-height: 1;
    pointer-events: none;
    user-select: none;
  }
  .week-tag {
    display: inline-flex; align-items: center; gap: 8px;
    border: 1px solid rgba(234,179,8,0.4);
    background: rgba(234,179,8,0.1);
    color: #fde047;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px; font-weight: 700;
    letter-spacing: 0.14em; text-transform: uppercase;
    padding: 5px 14px; border-radius: 20px;
    margin-bottom: 20px; width: fit-content;
  }
  .hero h1 {
    font-family: 'Unbounded', sans-serif;
    font-size: clamp(1.8rem, 5vw, 3.2rem);
    font-weight: 900;
    color: #fff;
    line-height: 1.1;
    margin-bottom: 8px;
    letter-spacing: -0.02em;
  }
  .hero h1 span { color: #fde047; }
  .hero-sub { color: #57534e; font-size: 0.96rem; max-width: 580px; margin-bottom: 32px; }
  .meta-strip { display: flex; flex-wrap: wrap; gap: 20px; border-top: 1px solid rgba(255,255,255,0.08); padding-top: 22px; }
  .meta-chip { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #44403c; display: flex; align-items: center; gap: 6px; }
  .meta-chip strong { color: #78716c; font-weight: 600; }

  .container { max-width: 980px; margin: 0 auto; padding: 0 28px 100px; }

  /* ── CLASE HEADER ── */
  .clase-header { margin: 60px 0 28px; display: flex; align-items: center; gap: 16px; }
  .clase-badge { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; background: var(--accent); color: #fff; padding: 5px 14px; border-radius: 3px; white-space: nowrap; flex-shrink: 0; }
  .clase-badge.b2 { background: var(--accent3); }
  .clase-title { font-family: 'Unbounded', sans-serif; font-size: 1.3rem; font-weight: 700; color: var(--text); line-height: 1.2; letter-spacing: -0.02em; }
  .clase-title span { color: var(--accent); }
  .clase-title span.b { color: var(--accent3); }
  .clase-line { flex: 1; height: 1px; background: var(--border); }

  /* ── OBJETIVO ── */
  .objetivo { background: rgba(21,128,61,0.06); border: 1px solid rgba(21,128,61,0.2); border-left: 4px solid var(--accent2); border-radius: 6px; padding: 14px 20px; margin-bottom: 28px; font-size: 0.9rem; }
  .objetivo strong { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.14em; text-transform: uppercase; color: var(--accent2); display: block; margin-bottom: 5px; }
  .objetivo p { margin: 0; color: var(--text-dim); }

  /* ── SECTION ── */
  .section { margin-bottom: 36px; }
  .section-title { font-family: 'Inter', sans-serif; font-size: 0.85rem; font-weight: 600; color: var(--text); margin-bottom: 14px; display: flex; align-items: center; gap: 10px; text-transform: uppercase; letter-spacing: 0.07em; }
  .tag { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; padding: 2px 8px; border-radius: 3px; }
  .tag.kotlin  { background: rgba(127,82,255,0.12); color: var(--kotlin); border: 1px solid rgba(127,82,255,0.3); }
  .tag.xml     { background: rgba(194,65,12,0.12);  color: var(--xml);    border: 1px solid rgba(194,65,12,0.3); }
  .tag.gradle  { background: rgba(21,128,61,0.12);  color: var(--gradle); border: 1px solid rgba(21,128,61,0.3); }
  .tag.concept { background: rgba(202,138,4,0.12);  color: var(--accent); border: 1px solid rgba(202,138,4,0.3); }
  .tag.json    { background: rgba(29,78,216,0.12);  color: var(--accent3); border: 1px solid rgba(29,78,216,0.3); }

  p { margin-bottom: 12px; color: var(--text-dim); font-size: 0.93rem; }

  /* ── HTTP FLOW ── */
  .http-flow {
    display: flex;
    align-items: center;
    gap: 0;
    background: var(--text);
    border-radius: 10px;
    padding: 24px;
    margin: 18px 0;
    overflow-x: auto;
  }
  .http-box {
    flex-shrink: 0;
    border-radius: 8px;
    padding: 14px 18px;
    text-align: center;
    min-width: 130px;
  }
  .http-box .layer { font-family: 'JetBrains Mono', monospace; font-size: 8px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; margin-bottom: 6px; display: block; }
  .http-box h4 { font-family: 'Unbounded', sans-serif; font-size: 0.72rem; font-weight: 700; margin-bottom: 4px; }
  .http-box p { font-size: 0.7rem; margin: 0; font-family: 'JetBrains Mono', monospace; line-height: 1.4; }
  .box-ui    { background: rgba(202,138,4,0.15); border: 1px solid rgba(202,138,4,0.3); }
  .box-ui    .layer, .box-ui h4, .box-ui p { color: #fde047; }
  .box-vm    { background: rgba(21,128,61,0.15); border: 1px solid rgba(21,128,61,0.3); }
  .box-vm    .layer, .box-vm h4, .box-vm p { color: #86efac; }
  .box-repo  { background: rgba(29,78,216,0.15); border: 1px solid rgba(29,78,216,0.3); }
  .box-repo  .layer, .box-repo h4, .box-repo p { color: #93c5fd; }
  .box-retro { background: rgba(127,82,255,0.15); border: 1px solid rgba(127,82,255,0.3); }
  .box-retro .layer, .box-retro h4, .box-retro p { color: #d8b4fe; }
  .box-api   { background: rgba(220,38,38,0.15); border: 1px solid rgba(220,38,38,0.3); }
  .box-api   .layer, .box-api h4, .box-api p { color: #fca5a5; }
  .http-arrow { color: #3f3f46; font-size: 20px; padding: 0 8px; flex-shrink: 0; }

  /* ── CONCEPTS ── */
  .concepts { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px,1fr)); gap: 12px; margin: 18px 0; }
  .concept-card { background: var(--surface); border: 1px solid var(--border); border-radius: 8px; padding: 16px; border-top: 3px solid var(--accent); }
  .concept-card.green { border-top-color: var(--accent2); }
  .concept-card.blue  { border-top-color: var(--accent3); }
  .concept-card.red   { border-top-color: var(--accent4); }
  .concept-card .icon { font-size: 1.3rem; margin-bottom: 8px; }
  .concept-card h4 { font-family: 'JetBrains Mono', monospace; font-size: 0.78rem; color: var(--accent); margin-bottom: 5px; font-weight: 700; }
  .concept-card.green h4 { color: var(--accent2); }
  .concept-card.blue  h4 { color: var(--accent3); }
  .concept-card.red   h4 { color: var(--accent4); }
  .concept-card p { font-size: 0.82rem; margin: 0; }

  /* ── CODE BLOCK ── */
  .code-block { background: #1c1917; border: 1px solid #2d2925; border-radius: 8px; overflow: hidden; margin: 16px 0; font-size: 0.84rem; }
  .code-header { display: flex; align-items: center; justify-content: space-between; padding: 9px 16px; background: #252220; border-bottom: 1px solid #2d2925; }
  .code-lang { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; padding: 2px 9px; border-radius: 3px; }
  .lang-kotlin { background: rgba(127,82,255,0.2); color: #b08fff; border: 1px solid rgba(127,82,255,0.3); }
  .lang-xml    { background: rgba(194,65,12,0.2);  color: #fb923c; border: 1px solid rgba(194,65,12,0.3); }
  .lang-gradle { background: rgba(21,128,61,0.2);  color: #6ee7b7; border: 1px solid rgba(21,128,61,0.3); }
  .lang-json   { background: rgba(29,78,216,0.2);  color: #93c5fd; border: 1px solid rgba(29,78,216,0.3); }
  .code-filename { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #57534e; }
  .code-body { padding: 18px 20px; overflow-x: auto; }
  pre { font-family: 'JetBrains Mono', monospace; line-height: 1.65; white-space: pre; color: #d6d3d1; background: transparent; }
  .kw  { color: #c792ea; } .fn  { color: #82aaff; } .str { color: #c3e88d; }
  .cm  { color: #44403c; font-style: italic; } .num { color: #f78c6c; }
  .cls { color: #ffcb6b; } .op  { color: #89ddff; }
  .tag-c { color: #e06c75; } .attr { color: #c3e88d; } .val { color: #f78c6c; }
  .an { color: #89ddff; } .jk { color: #fde047; } .jv { color: #c3e88d; } .jn { color: #f78c6c; }

  /* ── ALERT ── */
  .alert { border-radius: 6px; padding: 13px 17px; margin: 14px 0; font-size: 0.87rem; display: flex; gap: 12px; align-items: flex-start; }
  .alert-yellow { background: rgba(202,138,4,0.07);  border: 1px solid rgba(202,138,4,0.2); }
  .alert-green  { background: rgba(21,128,61,0.07);  border: 1px solid rgba(21,128,61,0.2); }
  .alert-red    { background: rgba(220,38,38,0.07);  border: 1px solid rgba(220,38,38,0.2); }
  .alert-blue   { background: rgba(29,78,216,0.07);  border: 1px solid rgba(29,78,216,0.2); }
  .alert-icon   { font-size: 1.1rem; flex-shrink: 0; margin-top: 1px; }
  .alert p      { margin: 0; }

  /* ── DIVIDER ── */
  .divider { margin: 56px 0 0; border: none; border-top: 2px solid var(--border); position: relative; }
  .divider::after { content: 'CLASE 02'; position: absolute; top: -11px; left: 50%; transform: translateX(-50%); background: var(--bg); padding: 0 14px; font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; color: var(--text-muted); }

  /* ── TAREA ── */
  .tarea { background: var(--text); border-radius: 10px; padding: 34px; margin-top: 56px; position: relative; overflow: hidden; }
  .tarea::after { content: 'REST'; position: absolute; right: -10px; bottom: -20px; font-family: 'Unbounded', sans-serif; font-size: 140px; font-weight: 900; color: rgba(255,255,255,0.03); line-height: 1; pointer-events: none; }
  .tarea-badge { display: inline-block; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; padding: 4px 12px; border-radius: 3px; margin-bottom: 14px; }
  .tarea h2 { font-family: 'Unbounded', sans-serif; font-size: 1.6rem; font-weight: 900; color: #fff; margin-bottom: 10px; letter-spacing: -0.02em; }
  .tarea-desc { color: #57534e; margin-bottom: 22px; font-size: 0.93rem; }
  .reqs { display: flex; flex-direction: column; gap: 10px; margin-bottom: 22px; }
  .req { display: flex; gap: 12px; align-items: flex-start; font-size: 0.89rem; color: #a8a29e; }
  .req-num { min-width: 22px; height: 22px; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 10px; font-weight: 700; border-radius: 3px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 2px; }
  .req-num.star { background: var(--accent2); }
  .entrega { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 6px; padding: 13px 17px; font-size: 0.84rem; }
  .entrega strong { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: #fde047; text-transform: uppercase; letter-spacing: 0.12em; display: block; margin-bottom: 4px; }
  .entrega p { color: #44403c; margin: 0; }

  ::-webkit-scrollbar { width: 5px; height: 5px; }
  ::-webkit-scrollbar-track { background: #252220; }
  ::-webkit-scrollbar-thumb { background: #44403c; border-radius: 3px; }
</style>
</head>
<body>

<div class="hero">
  <div class="week-tag">📅 Semana 14 de 16</div>
  <h1>Retrofit<br><span>+ Coroutines</span></h1>
  <p class="hero-sub">Conecta tu app a servicios web reales. Consume APIs REST de forma moderna usando Retrofit para las peticiones HTTP y Coroutines para no bloquear el hilo principal.</p>
  <div class="meta-strip">
    <div class="meta-chip">Clases <strong>2 × 2 hrs</strong></div>
    <div class="meta-chip">Lenguaje <strong>Kotlin</strong></div>
    <div class="meta-chip">Layout <strong>ConstraintLayout</strong></div>
    <div class="meta-chip">Prereq <strong>Semana 10 — ViewModel + LiveData</strong></div>
  </div>
</div>

<div class="container">

  <!-- ══════════════════ CLASE 1 ══════════════════ -->
  <div class="clase-header">
    <span class="clase-badge">Clase 01</span>
    <div class="clase-title">Retrofit, Gson y <span>primera petición</span></div>
    <div class="clase-line"></div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Configurar Retrofit, modelar la respuesta JSON con data classes y hacer la primera llamada GET a una API pública, mostrando el resultado en pantalla.</p>
  </div>

  <!-- Concepto: arquitectura -->
  <div class="section">
    <div class="section-title"><span class="tag concept">CONCEPTO</span> Flujo completo de una petición HTTP</div>
    <div class="http-flow">
      <div class="http-box box-ui">
        <span class="layer">vista</span>
        <h4>Activity</h4>
        <p>Observa<br>LiveData</p>
      </div>
      <div class="http-arrow">→</div>
      <div class="http-box box-vm">
        <span class="layer">viewmodel</span>
        <h4>ViewModel</h4>
        <p>viewModelScope<br>.launch{}</p>
      </div>
      <div class="http-arrow">→</div>
      <div class="http-box box-repo">
        <span class="layer">repository</span>
        <h4>Repository</h4>
        <p>suspend fun<br>getPokemons()</p>
      </div>
      <div class="http-arrow">→</div>
      <div class="http-box box-retro">
        <span class="layer">retrofit</span>
        <h4>ApiService</h4>
        <p>@GET("pokemon")<br>suspend fun</p>
      </div>
      <div class="http-arrow">→</div>
      <div class="http-box box-api">
        <span class="layer">internet</span>
        <h4>API REST</h4>
        <p>pokeapi.co<br>JSON response</p>
      </div>
    </div>
  </div>

  <!-- Conceptos clave -->
  <div class="section">
    <div class="section-title"><span class="tag concept">CONCEPTO</span> Componentes clave</div>
    <div class="concepts">
      <div class="concept-card blue">
        <div class="icon">🌐</div>
        <h4>Retrofit</h4>
        <p>Librería que convierte una API HTTP en una interface Kotlin. Define las peticiones con anotaciones como <code>@GET</code>, <code>@POST</code>.</p>
      </div>
      <div class="concept-card green">
        <div class="icon">🔄</div>
        <h4>Coroutines</h4>
        <p>Permite ejecutar código asíncrono de forma secuencial y legible. Reemplaza callbacks y AsyncTask.</p>
      </div>
      <div class="concept-card">
        <div class="icon">📦</div>
        <h4>Gson</h4>
        <p>Convierte automáticamente el JSON de la respuesta en data classes Kotlin. No es necesario parsear manualmente.</p>
      </div>
      <div class="concept-card red">
        <div class="icon">🛡️</div>
        <h4>Result / sealed class</h4>
        <p>Envuelve la respuesta en estados: Loading, Success, Error. Permite manejar los tres casos en la UI.</p>
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
    <span class="cm">// Retrofit — cliente HTTP</span>
    <span class="fn">implementation</span>(<span class="str">"com.squareup.retrofit2:retrofit:2.11.0"</span>)

    <span class="cm">// Convertidor Gson — JSON → data class automáticamente</span>
    <span class="fn">implementation</span>(<span class="str">"com.squareup.retrofit2:converter-gson:2.11.0"</span>)

    <span class="cm">// OkHttp Logging Interceptor — ver peticiones en Logcat (solo en debug)</span>
    <span class="fn">implementation</span>(<span class="str">"com.squareup.okhttp3:logging-interceptor:4.12.0"</span>)

    <span class="cm">// Coroutines para Android</span>
    <span class="fn">implementation</span>(<span class="str">"org.jetbrains.kotlinx:kotlinx-coroutines-android:1.8.0"</span>)

    <span class="cm">// ViewModel + LiveData (Semana 10)</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.lifecycle:lifecycle-livedata-ktx:2.7.0"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.activity:activity-ktx:1.9.0"</span>)
}</pre></div>
    </div>
  </div>

  <!-- Código 2: AndroidManifest -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 2 — AndroidManifest.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">AndroidManifest.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;manifest</span> <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span><span class="tag-c">&gt;</span>

    <span class="cm">&lt;!-- Internet: permiso normal, no requiere solicitud en runtime --&gt;</span>
    <span class="tag-c">&lt;uses-permission</span> <span class="attr">android:name</span>=<span class="val">"android.permission.INTERNET"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;application</span>
        <span class="attr">android:allowBackup</span>=<span class="val">"true"</span>
        <span class="attr">android:theme</span>=<span class="val">"@style/Theme.AppCompat.Light.DarkActionBar"</span>
        <span class="cm">&lt;!-- usesCleartextTraffic solo si la API usa HTTP en lugar de HTTPS --&gt;</span>
        <span class="attr">android:usesCleartextTraffic</span>=<span class="val">"false"</span><span class="tag-c">&gt;</span>

        <span class="tag-c">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".MainActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"true"</span><span class="tag-c">&gt;</span>
            <span class="tag-c">&lt;intent-filter&gt;</span>
                <span class="tag-c">&lt;action</span> <span class="attr">android:name</span>=<span class="val">"android.intent.action.MAIN"</span> <span class="tag-c">/&gt;</span>
                <span class="tag-c">&lt;category</span> <span class="attr">android:name</span>=<span class="val">"android.intent.category.LAUNCHER"</span> <span class="tag-c">/&gt;</span>
            <span class="tag-c">&lt;/intent-filter&gt;</span>
        <span class="tag-c">&lt;/activity&gt;</span>

        <span class="tag-c">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".DetalleActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"false"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;/application&gt;</span>
<span class="tag-c">&lt;/manifest&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 3: Respuesta JSON de referencia -->
  <div class="section">
    <div class="section-title"><span class="tag json">JSON</span> Código 3 — Respuesta de la API (PokeAPI)</div>
    <p>La API que usaremos es <code>https://pokeapi.co/api/v2/pokemon?limit=20</code>. Es gratuita, sin clave y perfecta para aprender. Así se ve una parte de su respuesta:</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-json">JSON</span>
        <span class="code-filename">GET https://pokeapi.co/api/v2/pokemon?limit=20</span>
      </div>
      <div class="code-body"><pre style="background:transparent">{
  <span class="jk">"count"</span>: <span class="jn">1302</span>,
  <span class="jk">"next"</span>: <span class="jv">"https://pokeapi.co/api/v2/pokemon?offset=20&limit=20"</span>,
  <span class="jk">"results"</span>: [
    {
      <span class="jk">"name"</span>: <span class="jv">"bulbasaur"</span>,
      <span class="jk">"url"</span>: <span class="jv">"https://pokeapi.co/api/v2/pokemon/1/"</span>
    },
    {
      <span class="jk">"name"</span>: <span class="jv">"ivysaur"</span>,
      <span class="jk">"url"</span>: <span class="jv">"https://pokeapi.co/api/v2/pokemon/2/"</span>
    }
  ]
}</pre></div>
    </div>
    <div class="alert alert-blue">
      <span class="alert-icon">💡</span>
      <p><strong>Regla de modelado:</strong> Cada objeto JSON se convierte en una <code>data class</code>. Cada campo JSON es una propiedad. El nombre de la propiedad Kotlin debe coincidir con la clave JSON, o usar la anotación <code>@SerializedName("nombre_en_json")</code> si son distintos.</p>
    </div>
  </div>

  <!-- Código 4: Data classes -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 4 — Data classes del modelo</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">PokemonModels.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> com.google.gson.annotations.SerializedName

<span class="cm">// Representa la respuesta completa del endpoint /pokemon</span>
<span class="kw">data class</span> <span class="cls">PokemonResponse</span>(
    <span class="kw">val</span> count:   <span class="cls">Int</span>,
    <span class="kw">val</span> next:    <span class="cls">String</span>?,
    <span class="kw">val</span> results: <span class="cls">List</span>&lt;<span class="cls">PokemonItem</span>&gt;
)

<span class="cm">// Representa cada Pokémon en la lista</span>
<span class="kw">data class</span> <span class="cls">PokemonItem</span>(
    <span class="kw">val</span> name: <span class="cls">String</span>,
    <span class="kw">val</span> url:  <span class="cls">String</span>
) {
    <span class="cm">// El id se extrae de la URL: "https://pokeapi.co/api/v2/pokemon/25/"</span>
    <span class="kw">fun</span> <span class="fn">getId</span>(): <span class="cls">Int</span> {
        <span class="kw">return</span> url.<span class="fn">trimEnd</span>(<span class="str">'/'</span>).<span class="fn">substringAfterLast</span>(<span class="str">'/'</span>).<span class="fn">toIntOrNull</span>() <span class="op">?:</span> <span class="num">0</span>
    }

    <span class="cm">// URL del sprite (imagen) del Pokémon usando su id</span>
    <span class="kw">fun</span> <span class="fn">getImageUrl</span>(): <span class="cls">String</span> {
        <span class="kw">return</span> <span class="str">"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getId()}.png"</span>
    }
}

<span class="cm">// Detalle de un Pokémon individual (endpoint /pokemon/{id})</span>
<span class="kw">data class</span> <span class="cls">PokemonDetalle</span>(
    <span class="kw">val</span> id:     <span class="cls">Int</span>,
    <span class="kw">val</span> name:   <span class="cls">String</span>,
    <span class="kw">val</span> height: <span class="cls">Int</span>,
    <span class="kw">val</span> weight: <span class="cls">Int</span>,
    <span class="kw">val</span> types:  <span class="cls">List</span>&lt;<span class="cls">TypeSlot</span>&gt;
)

<span class="kw">data class</span> <span class="cls">TypeSlot</span>(
    <span class="kw">val</span> slot: <span class="cls">Int</span>,
    <span class="kw">val</span> type: <span class="cls">TypeInfo</span>
)

<span class="kw">data class</span> <span class="cls">TypeInfo</span>(
    <span class="kw">val</span> name: <span class="cls">String</span>,
    <span class="kw">val</span> url:  <span class="cls">String</span>
)</pre></div>
    </div>
  </div>

  <!-- Código 5: PokemonApiService -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 5 — PokemonApiService.kt (interface Retrofit)</div>
    <p>La interface define los endpoints disponibles. Retrofit genera la implementación automáticamente en tiempo de ejecución.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">PokemonApiService.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> retrofit2.http.GET
<span class="kw">import</span> retrofit2.http.Path
<span class="kw">import</span> retrofit2.http.Query

<span class="kw">interface</span> <span class="cls">PokemonApiService</span> {

    <span class="cm">// GET https://pokeapi.co/api/v2/pokemon?limit=20&offset=0</span>
    <span class="an">@GET</span>(<span class="str">"pokemon"</span>)
    <span class="kw">suspend fun</span> <span class="fn">getPokemonList</span>(
        <span class="an">@Query</span>(<span class="str">"limit"</span>)  limit:  <span class="cls">Int</span> = <span class="num">20</span>,
        <span class="an">@Query</span>(<span class="str">"offset"</span>) offset: <span class="cls">Int</span> = <span class="num">0</span>
    ): <span class="cls">PokemonResponse</span>

    <span class="cm">// GET https://pokeapi.co/api/v2/pokemon/25 (pikachu)</span>
    <span class="an">@GET</span>(<span class="str">"pokemon/{id}"</span>)
    <span class="kw">suspend fun</span> <span class="fn">getPokemonDetalle</span>(
        <span class="an">@Path</span>(<span class="str">"id"</span>) id: <span class="cls">Int</span>
    ): <span class="cls">PokemonDetalle</span>
}</pre></div>
    </div>
    <div class="alert alert-yellow">
      <span class="alert-icon">💡</span>
      <p><strong>suspend fun:</strong> Las funciones de Retrofit deben ser <code>suspend</code> para usarse con coroutines. Retrofit maneja el cambio de hilo automáticamente — no es necesario especificar <code>Dispatchers.IO</code> explícitamente cuando se usa con coroutines.</p>
    </div>
  </div>

  <!-- Código 6: RetrofitClient -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 6 — RetrofitClient.kt (Singleton)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">RetrofitClient.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> okhttp3.OkHttpClient
<span class="kw">import</span> okhttp3.logging.HttpLoggingInterceptor
<span class="kw">import</span> retrofit2.Retrofit
<span class="kw">import</span> retrofit2.converter.gson.GsonConverterFactory

<span class="kw">object</span> <span class="cls">RetrofitClient</span> {

    <span class="kw">private const val</span> BASE_URL = <span class="str">"https://pokeapi.co/api/v2/"</span>

    <span class="cm">// Interceptor de logs — solo para desarrollo</span>
    <span class="kw">private val</span> loggingInterceptor = <span class="cls">HttpLoggingInterceptor</span>().<span class="fn">apply</span> {
        level = <span class="cls">HttpLoggingInterceptor</span>.<span class="cls">Level</span>.BODY
    }

    <span class="kw">private val</span> okHttpClient = <span class="cls">OkHttpClient</span>.<span class="cls">Builder</span>()
        .<span class="fn">addInterceptor</span>(loggingInterceptor)
        .<span class="fn">build</span>()

    <span class="kw">private val</span> retrofit = <span class="cls">Retrofit</span>.<span class="cls">Builder</span>()
        .<span class="fn">baseUrl</span>(BASE_URL)
        .<span class="fn">client</span>(okHttpClient)
        .<span class="fn">addConverterFactory</span>(<span class="cls">GsonConverterFactory</span>.<span class="fn">create</span>())
        .<span class="fn">build</span>()

    <span class="cm">// Instancia del servicio — Retrofit implementa la interface automáticamente</span>
    <span class="kw">val</span> apiService: <span class="cls">PokemonApiService</span> = retrofit.<span class="fn">create</span>(<span class="cls">PokemonApiService</span>::<span class="kw">class</span>.java)
}</pre></div>
    </div>
  </div>

  <!-- Código 7: Estado de UI con sealed class -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 7 — ApiResult.kt (sealed class de estados)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">ApiResult.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="cm">/**
 * Envuelve el resultado de una operación de red en 3 estados posibles.
 * La sealed class garantiza que en el when() se manejen todos los casos.
 */</span>
<span class="kw">sealed class</span> <span class="cls">ApiResult</span>&lt;<span class="kw">out</span> T&gt; {
    <span class="kw">data class</span> <span class="cls">Success</span>&lt;T&gt;(<span class="kw">val</span> data: T) : <span class="cls">ApiResult</span>&lt;T&gt;()
    <span class="kw">data class</span> <span class="cls">Error</span>(<span class="kw">val</span> mensaje: <span class="cls">String</span>) : <span class="cls">ApiResult</span>&lt;<span class="cls">Nothing</span>&gt;()
    <span class="kw">object</span> <span class="cls">Loading</span> : <span class="cls">ApiResult</span>&lt;<span class="cls">Nothing</span>&gt;()
}</pre></div>
    </div>
  </div>

  <!-- Código 8: PokemonRepository -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 8 — PokemonRepository.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">PokemonRepository.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">class</span> <span class="cls">PokemonRepository</span> {

    <span class="kw">private val</span> api = <span class="cls">RetrofitClient</span>.apiService

    <span class="cm">// try-catch envuelve la petición: cualquier fallo de red queda en Error</span>
    <span class="kw">suspend fun</span> <span class="fn">getPokemonList</span>(limit: <span class="cls">Int</span> = <span class="num">20</span>): <span class="cls">ApiResult</span>&lt;<span class="cls">List</span>&lt;<span class="cls">PokemonItem</span>&gt;&gt; {
        <span class="kw">return try</span> {
            <span class="kw">val</span> respuesta = api.<span class="fn">getPokemonList</span>(limit = limit)
            <span class="cls">ApiResult</span>.<span class="cls">Success</span>(respuesta.results)
        } <span class="kw">catch</span> (e: <span class="cls">Exception</span>) {
            <span class="cls">ApiResult</span>.<span class="cls">Error</span>(e.message <span class="op">?:</span> <span class="str">"Error desconocido"</span>)
        }
    }

    <span class="kw">suspend fun</span> <span class="fn">getPokemonDetalle</span>(id: <span class="cls">Int</span>): <span class="cls">ApiResult</span>&lt;<span class="cls">PokemonDetalle</span>&gt; {
        <span class="kw">return try</span> {
            <span class="cls">ApiResult</span>.<span class="cls">Success</span>(api.<span class="fn">getPokemonDetalle</span>(id))
        } <span class="kw">catch</span> (e: <span class="cls">Exception</span>) {
            <span class="cls">ApiResult</span>.<span class="cls">Error</span>(e.message <span class="op">?:</span> <span class="str">"Error al cargar el detalle"</span>)
        }
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 9: PokemonViewModel -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 9 — PokemonViewModel.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">PokemonViewModel.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.lifecycle.LiveData
<span class="kw">import</span> androidx.lifecycle.MutableLiveData
<span class="kw">import</span> androidx.lifecycle.ViewModel
<span class="kw">import</span> androidx.lifecycle.viewModelScope
<span class="kw">import</span> kotlinx.coroutines.launch

<span class="kw">class</span> <span class="cls">PokemonViewModel</span> : <span class="cls">ViewModel</span>() {

    <span class="kw">private val</span> repository = <span class="cls">PokemonRepository</span>()

    <span class="kw">private val</span> _pokemonList = <span class="cls">MutableLiveData</span>&lt;<span class="cls">ApiResult</span>&lt;<span class="cls">List</span>&lt;<span class="cls">PokemonItem</span>&gt;&gt;&gt;()
    <span class="kw">val</span> pokemonList: <span class="cls">LiveData</span>&lt;<span class="cls">ApiResult</span>&lt;<span class="cls">List</span>&lt;<span class="cls">PokemonItem</span>&gt;&gt;&gt; = _pokemonList

    <span class="kw">private val</span> _pokemonDetalle = <span class="cls">MutableLiveData</span>&lt;<span class="cls">ApiResult</span>&lt;<span class="cls">PokemonDetalle</span>&gt;&gt;()
    <span class="kw">val</span> pokemonDetalle: <span class="cls">LiveData</span>&lt;<span class="cls">ApiResult</span>&lt;<span class="cls">PokemonDetalle</span>&gt;&gt; = _pokemonDetalle

    <span class="kw">init</span> {
        <span class="cm">// Cargar la lista al crear el ViewModel</span>
        <span class="fn">cargarPokemonList</span>()
    }

    <span class="kw">fun</span> <span class="fn">cargarPokemonList</span>() {
        viewModelScope.<span class="fn">launch</span> {
            _pokemonList.value = <span class="cls">ApiResult</span>.<span class="cls">Loading</span>
            _pokemonList.value = repository.<span class="fn">getPokemonList</span>()
        }
    }

    <span class="kw">fun</span> <span class="fn">cargarDetalle</span>(id: <span class="cls">Int</span>) {
        viewModelScope.<span class="fn">launch</span> {
            _pokemonDetalle.value = <span class="cls">ApiResult</span>.<span class="cls">Loading</span>
            _pokemonDetalle.value = repository.<span class="fn">getPokemonDetalle</span>(id)
        }
    }
}</pre></div>
    </div>
  </div>

  <!-- ══════════════════ CLASE 2 ══════════════════ -->
  <hr class="divider">

  <div class="clase-header" style="margin-top:56px">
    <span class="clase-badge b2">Clase 02</span>
    <div class="clase-title">UI completa con <span class="b">RecyclerView</span> y manejo de estados</div>
    <div class="clase-line"></div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Construir la UI completa: lista de Pokémon con RecyclerView, pantalla de detalle y manejo visual de los tres estados (cargando, éxito, error) para cada petición.</p>
  </div>

  <!-- Código 10: activity_main.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 10 — activity_main.xml</div>
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

    <span class="cm">&lt;!-- ProgressBar visible durante la carga --&gt;</span>
    <span class="tag-c">&lt;ProgressBar</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/progressBar"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:visibility</span>=<span class="val">"gone"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

    <span class="cm">&lt;!-- Mensaje de error --&gt;</span>
    <span class="tag-c">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvError"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:visibility</span>=<span class="val">"gone"</span>
        <span class="attr">android:textColor</span>=<span class="val">"#dc2626"</span>
        <span class="attr">android:textSize</span>=<span class="val">"14sp"</span>
        <span class="attr">android:padding</span>=<span class="val">"16dp"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

    <span class="cm">&lt;!-- Lista de resultados --&gt;</span>
    <span class="tag-c">&lt;androidx.recyclerview.widget.RecyclerView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/recyclerPokemon"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">android:clipToPadding</span>=<span class="val">"false"</span>
        <span class="attr">android:visibility</span>=<span class="val">"gone"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 11: item_pokemon.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 11 — item_pokemon.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/item_pokemon.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag-c">?&gt;</span>
<span class="tag-c">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
    <span class="attr">android:padding</span>=<span class="val">"12dp"</span>
    <span class="attr">android:background</span>=<span class="val">"?attr/selectableItemBackground"</span><span class="tag-c">&gt;</span>

    <span class="tag-c">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvPokemonId"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"40dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"12sp"</span>
        <span class="attr">android:textColor</span>=<span class="val">"#888"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvPokemonNombre"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"17sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">android:layout_marginStart</span>=<span class="val">"8dp"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toEndOf</span>=<span class="val">"@id/tvPokemonId"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 12: PokemonAdapter -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 12 — PokemonAdapter.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">PokemonAdapter.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">PokemonAdapter</span>(
    <span class="kw">private var</span> lista: <span class="cls">List</span>&lt;<span class="cls">PokemonItem</span>&gt; = <span class="fn">emptyList</span>(),
    <span class="kw">private val</span> onClick: (<span class="cls">PokemonItem</span>) <span class="op">-&gt;</span> <span class="cls">Unit</span>
) : <span class="cls">RecyclerView</span>.<span class="cls">Adapter</span>&lt;<span class="cls">PokemonAdapter</span>.<span class="cls">PokemonViewHolder</span>&gt;() {

    <span class="kw">inner class</span> <span class="cls">PokemonViewHolder</span>(itemView: <span class="cls">View</span>) : <span class="cls">RecyclerView</span>.<span class="cls">ViewHolder</span>(itemView) {
        <span class="kw">val</span> tvId:     <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvPokemonId)
        <span class="kw">val</span> tvNombre: <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvPokemonNombre)
    }

    <span class="kw">override fun</span> <span class="fn">onCreateViewHolder</span>(parent: <span class="cls">ViewGroup</span>, viewType: <span class="cls">Int</span>) =
        <span class="cls">PokemonViewHolder</span>(<span class="cls">LayoutInflater</span>.<span class="fn">from</span>(parent.context)
            .<span class="fn">inflate</span>(<span class="cls">R</span>.layout.item_pokemon, parent, <span class="kw">false</span>))

    <span class="kw">override fun</span> <span class="fn">onBindViewHolder</span>(holder: <span class="cls">PokemonViewHolder</span>, position: <span class="cls">Int</span>) {
        <span class="kw">val</span> pokemon = lista[position]
        holder.tvId.text     = <span class="str">"#${pokemon.getId()}"</span>
        holder.tvNombre.text = pokemon.name.<span class="fn">replaceFirstChar</span> { it.<span class="fn">uppercase</span>() }
        holder.itemView.<span class="fn">setOnClickListener</span> { <span class="fn">onClick</span>(pokemon) }
    }

    <span class="kw">override fun</span> <span class="fn">getItemCount</span>() = lista.size

    <span class="kw">fun</span> <span class="fn">actualizarLista</span>(nuevaLista: <span class="cls">List</span>&lt;<span class="cls">PokemonItem</span>&gt;) {
        lista = nuevaLista
        <span class="fn">notifyDataSetChanged</span>()
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 13: MainActivity.kt completo -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 13 — MainActivity.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">MainActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.widget.ProgressBar
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.activity.viewModels
<span class="kw">import</span> androidx.recyclerview.widget.LinearLayoutManager
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">MainActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">private val</span> viewModel: <span class="cls">PokemonViewModel</span> <span class="kw">by</span> <span class="fn">viewModels</span>()

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_main)

        <span class="kw">val</span> progressBar    = <span class="fn">findViewById</span>&lt;<span class="cls">ProgressBar</span>&gt;(<span class="cls">R</span>.id.progressBar)
        <span class="kw">val</span> tvError        = <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvError)
        <span class="kw">val</span> recyclerView   = <span class="fn">findViewById</span>&lt;<span class="cls">RecyclerView</span>&gt;(<span class="cls">R</span>.id.recyclerPokemon)

        <span class="kw">val</span> adapter = <span class="cls">PokemonAdapter</span> { pokemon <span class="op">-&gt;</span>
            <span class="kw">val</span> intent = <span class="cls">Intent</span>(<span class="kw">this</span>, <span class="cls">DetalleActivity</span>::<span class="kw">class</span>.java)
            intent.<span class="fn">putExtra</span>(<span class="str">"POKEMON_ID"</span>, pokemon.<span class="fn">getId</span>())
            intent.<span class="fn">putExtra</span>(<span class="str">"POKEMON_NOMBRE"</span>, pokemon.name)
            <span class="fn">startActivity</span>(intent)
        }

        recyclerView.layoutManager = <span class="cls">LinearLayoutManager</span>(<span class="kw">this</span>)
        recyclerView.adapter = adapter

        <span class="cm">// Observar el LiveData con los 3 estados de la sealed class</span>
        viewModel.pokemonList.<span class="fn">observe</span>(<span class="kw">this</span>) { resultado <span class="op">-&gt;</span>
            <span class="kw">when</span> (resultado) {
                <span class="kw">is</span> <span class="cls">ApiResult</span>.<span class="cls">Loading</span> <span class="op">-&gt;</span> {
                    progressBar.visibility  = <span class="cls">View</span>.VISIBLE
                    recyclerView.visibility = <span class="cls">View</span>.GONE
                    tvError.visibility      = <span class="cls">View</span>.GONE
                }
                <span class="kw">is</span> <span class="cls">ApiResult</span>.<span class="cls">Success</span> <span class="op">-&gt;</span> {
                    progressBar.visibility  = <span class="cls">View</span>.GONE
                    recyclerView.visibility = <span class="cls">View</span>.VISIBLE
                    tvError.visibility      = <span class="cls">View</span>.GONE
                    adapter.<span class="fn">actualizarLista</span>(resultado.data)
                }
                <span class="kw">is</span> <span class="cls">ApiResult</span>.<span class="cls">Error</span> <span class="op">-&gt;</span> {
                    progressBar.visibility  = <span class="cls">View</span>.GONE
                    recyclerView.visibility = <span class="cls">View</span>.GONE
                    tvError.visibility      = <span class="cls">View</span>.VISIBLE
                    tvError.text = <span class="str">"❌ ${resultado.mensaje}"</span>
                }
            }
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-red">
      <span class="alert-icon">⚠️</span>
      <p><strong>NetworkOnMainThreadException:</strong> Si se llama a Retrofit directamente en la Activity sin coroutines ni ViewModel, Android lanza esta excepción. <code>viewModelScope.launch</code> garantiza que la petición corre en un hilo de fondo automáticamente.</p>
    </div>
  </div>

  <!-- Código 14: DetalleActivity -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 14 — activity_detalle.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_detalle.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag-c">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag-c">?&gt;</span>
<span class="tag-c">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"20dp"</span><span class="tag-c">&gt;</span>

    <span class="tag-c">&lt;ProgressBar</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/progressDetalle"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:visibility</span>=<span class="val">"visible"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvDetNombre"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"28sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">android:visibility</span>=<span class="val">"gone"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

    <span class="tag-c">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvDetInfo"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"16sp"</span>
        <span class="attr">android:visibility</span>=<span class="val">"gone"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"12dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvDetNombre"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag-c">/&gt;</span>

<span class="tag-c">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 15: DetalleActivity.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 15 — DetalleActivity.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">DetalleActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.widget.ProgressBar
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.activity.viewModels

<span class="kw">class</span> <span class="cls">DetalleActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">private val</span> viewModel: <span class="cls">PokemonViewModel</span> <span class="kw">by</span> <span class="fn">viewModels</span>()

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_detalle)

        <span class="kw">val</span> pokemonId     = intent.<span class="fn">getIntExtra</span>(<span class="str">"POKEMON_ID"</span>, <span class="num">1</span>)
        <span class="kw">val</span> pokemonNombre = intent.<span class="fn">getStringExtra</span>(<span class="str">"POKEMON_NOMBRE"</span>) <span class="op">?:</span> <span class="str">""</span>

        title = pokemonNombre.<span class="fn">replaceFirstChar</span> { it.<span class="fn">uppercase</span>() }

        <span class="kw">val</span> progressBar = <span class="fn">findViewById</span>&lt;<span class="cls">ProgressBar</span>&gt;(<span class="cls">R</span>.id.progressDetalle)
        <span class="kw">val</span> tvNombre    = <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvDetNombre)
        <span class="kw">val</span> tvInfo      = <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvDetInfo)

        viewModel.pokemonDetalle.<span class="fn">observe</span>(<span class="kw">this</span>) { resultado <span class="op">-&gt;</span>
            <span class="kw">when</span> (resultado) {
                <span class="kw">is</span> <span class="cls">ApiResult</span>.<span class="cls">Loading</span> <span class="op">-&gt;</span> {
                    progressBar.visibility = <span class="cls">View</span>.VISIBLE
                    tvNombre.visibility    = <span class="cls">View</span>.GONE
                    tvInfo.visibility      = <span class="cls">View</span>.GONE
                }
                <span class="kw">is</span> <span class="cls">ApiResult</span>.<span class="cls">Success</span> <span class="op">-&gt;</span> {
                    <span class="kw">val</span> p = resultado.data
                    progressBar.visibility = <span class="cls">View</span>.GONE
                    tvNombre.visibility    = <span class="cls">View</span>.VISIBLE
                    tvInfo.visibility      = <span class="cls">View</span>.VISIBLE
                    tvNombre.text = p.name.<span class="fn">replaceFirstChar</span> { it.<span class="fn">uppercase</span>() }
                    <span class="kw">val</span> tipos = p.types.<span class="fn">joinToString</span>(<span class="str">", "</span>) { it.type.name }
                    tvInfo.text = <span class="str">"Altura: ${p.height * 10} cm\nPeso: ${p.weight / 10.0} kg\nTipos: $tipos"</span>
                }
                <span class="kw">is</span> <span class="cls">ApiResult</span>.<span class="cls">Error</span> <span class="op">-&gt;</span> {
                    progressBar.visibility = <span class="cls">View</span>.GONE
                    tvNombre.visibility    = <span class="cls">View</span>.VISIBLE
                    tvNombre.text = <span class="str">"❌ ${resultado.mensaje}"</span>
                }
            }
        }

        <span class="cm">// Cargar el detalle al abrir la Activity</span>
        viewModel.<span class="fn">cargarDetalle</span>(pokemonId)
    }
}</pre></div>
    </div>
    <div class="alert alert-green">
      <span class="alert-icon">🔗</span>
      <p><strong>Integración completa:</strong> Esta app usa RecyclerView (Sem. 7), Intents y Extras (Sem. 8), ViewModel + LiveData (Sem. 10) y Retrofit + Coroutines (Sem. 14) trabajando juntos en una arquitectura limpia. Es el proyecto más cercano a una app Android profesional del curso.</p>
    </div>
    <div class="alert alert-yellow">
      <span class="alert-icon">💡</span>
      <p><strong>Para mostrar imágenes desde URL</strong> se necesita una librería adicional como Glide o Picasso. No están incluidas aquí para no sobrecargar la semana, pero el punto extra de la tarea las menciona. Agregar Glide: <code>implementation("com.github.bumptech.glide:glide:4.16.0")</code> y usar <code>Glide.with(context).load(url).into(imageView)</code>.</p>
    </div>
  </div>

  <!-- TAREA -->
  <div class="tarea">
    <div class="tarea-badge">📝 Práctica — Tarea</div>
    <h2>App: Explorador del Clima</h2>
    <p class="tarea-desc">Construye una app que consuma la API pública de Open-Meteo (<code>api.open-meteo.com</code>) para mostrar el clima actual y el pronóstico de los próximos días. Es gratuita, sin registro y retorna JSON bien documentado.</p>
    <div class="reqs">
      <div class="req"><div class="req-num">1</div><div>Configurar <strong>Retrofit + Gson</strong> con la URL base <code>https://api.open-meteo.com/v1/</code>. La endpoint a usar es: <code>/forecast?latitude=16.92&longitude=-92.26&current_weather=true&daily=temperature_2m_max,temperature_2m_min&timezone=America/Mexico_City</code></div></div>
      <div class="req"><div class="req-num">2</div><div>Modelar la respuesta con <strong>data classes</strong> para: el clima actual (<code>current_weather</code>) y el pronóstico diario (<code>daily</code> con listas de fechas y temperaturas máx/mín).</div></div>
      <div class="req"><div class="req-num">3</div><div>Implementar el patrón completo: <strong>ApiService → Repository → ViewModel → Activity</strong>. El ViewModel expone un <code>LiveData&lt;ApiResult&lt;...&gt;&gt;</code> con los tres estados.</div></div>
      <div class="req"><div class="req-num">4</div><div>La UI muestra el <strong>clima actual</strong> (temperatura y código de tiempo) en la parte superior, y un <strong>RecyclerView</strong> con el pronóstico de los próximos 7 días.</div></div>
      <div class="req"><div class="req-num">5</div><div>Manejar correctamente los <strong>tres estados visuales</strong>: ProgressBar durante la carga, datos visibles en éxito, y mensaje de error con botón "Reintentar" que llame al método del ViewModel.</div></div>
      <div class="req"><div class="req-num star">⭐</div><div><strong>Punto extra:</strong> Agregar <strong>Glide</strong> (<code>com.github.bumptech.glide:glide:4.16.0</code>) para mostrar un ícono del clima usando las imágenes de <code>https://openweathermap.org/img/wn/</code> según el código meteorológico WMO.</div></div>
    </div>
    <div class="entrega">
      <strong> Entrega</strong>
      <p>Capturas mostrando: la pantalla de carga (ProgressBar), la lista con el pronóstico y un estado de error simulado (desconectando el WiFi del emulador).</p>
    </div>
  </div>

</div>
</body>
</html>

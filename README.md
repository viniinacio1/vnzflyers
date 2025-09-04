# Create a deploy-ready static site (HTML/CSS/JS) and zip it for VNZ
import os, zipfile, textwrap, json, pathlib

root = "/mnt/data/vnz-flyers-site"
os.makedirs(root, exist_ok=True)
assets = os.path.join(root, "assets")
os.makedirs(assets, exist_ok=True)

index_html = """<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>VNZ Flyers — Flyers & Motion</title>
  <meta name="description" content="Flyers e Motion Flyers que vendem por você. Simples, direto e com estética de respeito.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="./styles.css">
</head>
<body>
  <header class="nav">
    <div class="container nav__inner">
      <a href="#home" class="logo">VNZ <span>Flyers</span></a>
      <nav class="nav__links">
        <a href="#portfolio">Portfólio</a>
        <a href="#servicos">Serviços</a>
        <a href="#pacotes">Pacotes</a>
        <a href="#contato" class="btn">Pedir agora</a>
      </nav>
      <button class="nav__menu" aria-label="menu" onclick="toggleMenu()">☰</button>
    </div>
  </header>

  <main id="home" class="hero">
    <div class="container hero__grid">
      <div class="hero__text">
        <h1>Flyers e <mark>Motion Flyers</mark> que vendem por você.</h1>
        <p>Design afiado + animações chamativas, do jeitinho que converte no feed, story e reels. Simples, direto e com estética de respeito.</p>
        <div class="hero__cta">
          <a href="#pacotes" class="btn">Ver pacotes →</a>
          <a href="#portfolio" class="btn btn--ghost">Ver portfólio</a>
        </div>
        <ul class="hero__badges">
          <li>★ +120 clientes</li>
          <li>⚡ Entrega ágil</li>
          <li>R$ Preço justo</li>
        </ul>
      </div>
      <div class="hero__mosaic">
        <div class="tile"></div><div class="tile"></div><div class="tile"></div><div class="tile"></div>
      </div>
    </div>
  </main>

  <section id="servicos" class="section">
    <div class="container">
      <h2>Serviços</h2>
      <p class="muted">Do estático ao animado, pacotes sob medida para sua página vender mais.</p>
      <div class="grid3">
        <article class="card">
          <h3>Flyer Estático</h3>
          <p>Artes para feed e stories com tipografia forte e composição limpa.</p>
          <ul>
            <li>Formato quadrado/vertical</li>
            <li>Entrega em PNG/JPG</li>
            <li>1 rodada de ajustes</li>
          </ul>
        </article>
        <article class="card">
          <h3>Motion Flyer</h3>
          <p>Animações curtas e diretas para dar vida ao seu post.</p>
          <ul>
            <li>Até 15s</li>
            <li>Som opcional</li>
            <li>Export em MP4</li>
          </ul>
        </article>
        <article class="card">
          <h3>Kits de Lançamento</h3>
          <p>Combo com 5 artes (estático + motion) alinhadas à sua campanha.</p>
          <ul>
            <li>Guia de uso de cores</li>
            <li>Padronização visual</li>
            <li>Prioridade na fila</li>
          </ul>
        </article>
      </div>
    </div>
  </section>

  <section id="pacotes" class="section alt">
    <div class="container">
      <h2>Pacotes e valores</h2>
      <p class="muted">Transparência total. Você escolhe o que precisa e pronto.</p>
      <div class="grid3">
        <article class="price">
          <header><h3>Start</h3><div class="price__tag">R$ 79</div></header>
          <p>1 Flyer Estático</p>
          <ul><li>1 arte estática</li><li>Entrega em 24–48h</li><li>1 ajuste</li></ul>
          <a href="#contato" class="btn btn--block">Pedir Start</a>
        </article>
        <article class="price highlight">
          <header><h3>Turbo</h3><div class="price__tag">R$ 149</div></header>
          <p>1 Motion Flyer</p>
          <ul><li>Até 15s</li><li>Legendado opcional</li><li>1 ajuste</li></ul>
          <a href="#contato" class="btn btn--block">Pedir Turbo</a>
        </article>
        <article class="price">
          <header><h3>Lançamento</h3><div class="price__tag">R$ 349</div></header>
          <p>Kit 5 artes (misto)</p>
          <ul><li>3 estáticos + 2 motion</li><li>Guia de cores</li><li>Prioridade</li></ul>
          <a href="#contato" class="btn btn--block">Pedir Kit</a>
        </article>
      </div>
    </div>
  </section>

  <section id="portfolio" class="section">
    <div class="container">
      <h2>Portfólio</h2>
      <p class="muted">Exemplos (troque pelas suas artes reais).</p>
      <div class="grid3 portfolio">
        <div class="ph"></div><div class="ph"></div><div class="ph"></div>
        <div class="ph"></div><div class="ph"></div><div class="ph"></div>
        <div class="ph"></div><div class="ph"></div><div class="ph"></div>
      </div>
    </div>
  </section>

  <section id="contato" class="section alt">
    <div class="container grid2">
      <div>
        <h2>Fazer pedido</h2>
        <p class="muted">Fala comigo e já manda o briefing. Respondo rapidinho!</p>
        <form id="form" onsubmit="return openWhatsApp(event)">
          <input required name="nome" placeholder="Seu nome">
          <select name="tipo">
            <option>Flyer Estático</option>
            <option>Motion Flyer</option>
            <option>Kit Lançamento</option>
          </select>
          <input type="number" name="qtde" min="1" value="1">
          <textarea name="detalhes" rows="4" placeholder="Cores, texto, referências, prazo…"></textarea>
          <button class="btn btn--block" type="submit">Abrir no WhatsApp</button>
        </form>
      </div>
      <aside class="card contact">
        <h3>Contato direto</h3>
        <ul>
          <li>📞 +55 (11) 93020-0313</li>
          <li>✉️ vinicius.inacioc@hotmail.com</li>
          <li>📷 @vnz.design (exemplo)</li>
        </ul>
        <p class="muted small">1) Você envia o briefing. 2) Eu retorno com prazo e valor final. 3) Entrega e 1 rodada de ajustes inclusa.</p>
      </aside>
    </div>
  </section>

  <footer class="footer">
    <div class="container">
      <p>© <span id="year"></span> VNZ Flyers. Todos os direitos reservados.</p>
      <nav><a href="#servicos">Serviços</a><a href="#pacotes">Pacotes</a><a href="#contato">Contato</a></nav>
    </div>
  </footer>

  <script src="./script.js"></script>
</body>
</html>
"""

styles_css = """
:root { --bg:#fff; --fg:#111; --muted:#6b7280; --brand:#111; --alt:#f6f6f6; }
*{box-sizing:border-box} body{margin:0;font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Arial;background:var(--bg);color:var(--fg);}
.container{max-width:1100px;margin:0 auto;padding:0 20px}
.nav{position:sticky;top:0;backdrop-filter:saturate(1.2) blur(8px);background:rgba(255,255,255,.7);border-bottom:1px solid #e5e7eb;z-index:40}
.nav__inner{height:64px;display:flex;align-items:center;justify-content:space-between}
.logo{font-weight:700;text-decoration:none;color:var(--fg)} .logo span{color:var(--muted);font-weight:600}
.nav__links{display:flex;gap:18px;align-items:center}
.nav__links a{color:var(--fg);text-decoration:none;opacity:.9} .nav__links a:hover{opacity:1}
.nav__menu{display:none;background:transparent;border:0;font-size:20px}
.btn{display:inline-flex;align-items:center;gap:8px;background:var(--brand);color:#fff;border-radius:16px;padding:10px 14px;text-decoration:none;border:1px solid #111}
.btn--ghost{background:transparent;color:var(--fg);border-color:#e5e7eb}
.btn--block{width:100%;justify-content:center}
.hero{padding:72px 0;background:linear-gradient(180deg,#fff, #fafafa 50%, #fff)}
.hero__grid{display:grid;grid-template-columns:1.1fr .9fr;gap:28px;align-items:center}
.hero__text h1{font-size:44px;line-height:1.05;margin:0 0 10px} mark{background:#111;color:#fff;padding:0 6px;border-radius:6px}
.hero__text p{color:var(--muted);max-width:520px}
.hero__cta{margin-top:16px;display:flex;gap:10px;flex-wrap:wrap}
.hero__badges{margin:14px 0 0;padding:0;list-style:none;display:flex;gap:16px;color:var(--muted);font-size:14px}
.hero__mosaic{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.tile{aspect-ratio:4/5;border-radius:16px;background:#e5e7eb;box-shadow:0 1px 0 #e5e7eb}
.section{padding:72px 0} .section.alt{background:var(--alt)}
.section h2{font-size:32px;margin:0 0 6px} .muted{color:var(--muted)}
.grid3{display:grid;grid-template-columns:repeat(3,1fr);gap:18px}
.grid2{display:grid;grid-template-columns:1.1fr .9fr;gap:18px}
.card{border:1px solid #e5e7eb;border-radius:16px;padding:18px;background:#fff}
.price{border:1px solid #e5e7eb;border-radius:18px;padding:18px;background:#fff;display:flex;flex-direction:column;gap:10px}
.price header{display:flex;align-items:center;justify-content:space-between}
.price__tag{font-weight:700;font-size:22px}
.price.highlight{border-width:2px}
.portfolio .ph{aspect-ratio:4/5;background:#e5e7eb;border-radius:14px}
.contact ul{margin:0 0 10px;padding-left:18px}
.small{font-size:12px}
footer.footer{border-top:1px solid #e5e7eb;padding:24px 0}
.footer .container{display:flex;align-items:center;justify-content:space-between;gap:16px}
@media (max-width:900px){.hero__grid,.grid3,.grid2{grid-template-columns:1fr}.nav__links{display:none}.nav__menu{display:block}}
"""

script_js = """
function toggleMenu(){ const links=document.querySelector('.nav__links'); if(links.style.display==='flex'){links.style.display='none'} else {links.style.display='flex'; links.style.flexDirection='column'} }
function openWhatsApp(e){ e.preventDefault(); const f=e.target; const nome=f.nome.value||''; const tipo=f.tipo.value||'Flyer Estático'; const qtde=f.qtde.value||'1'; const detalhes=f.detalhes.value||''; const msg=encodeURIComponent(`Olá, sou ${nome}. Quero ${qtde}x ${tipo}. Detalhes: ${detalhes}`); const zap='5511930200313'; window.location.href=`https://wa.me/${zap}?text=${msg}`; return false;}
document.getElementById('year').textContent = new Date().getFullYear();
"""

with open(os.path.join(root,"index.html"),"w", encoding="utf-8") as f: f.write(index_html)
with open(os.path.join(root,"styles.css"),"w", encoding="utf-8") as f: f.write(styles_css)
with open(os.path.join(root,"script.js"),"w", encoding="utf-8") as f: f.write(script_js)

zip_path = "/mnt/data/vnz-flyers-site.zip"
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for dirpath, _, filenames in os.walk(root):
        for name in filenames:
            path = os.path.join(dirpath, name)
            z.write(path, arcname=os.path.relpath(path, root))

zip_path

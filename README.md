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

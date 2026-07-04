# Site PRO Corretora Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Construir e publicar o site institucional single-page da PRO Corretora (HTML/CSS/JS puro, sem build, sem formulários), hospedado no GitHub Pages.

**Architecture:** Página única (`index.html`) com seções âncora (Header, Hero, Serviços, Sobre, Contato, Rodapé) mais um botão flutuante de WhatsApp. Estilo em `styles.css` usando variáveis CSS para a paleta da marca. Interatividade mínima em `script.js` (menu mobile + fechamento ao navegar).

**Tech Stack:** HTML5, CSS3 (custom properties, Flexbox/Grid, media queries), JavaScript vanilla (sem frameworks, sem dependências externas, sem CDNs).

## Global Constraints

- Sem formulários e sem coleta de dados de visitantes (decisão do spec para evitar exposição a LGPD).
- Zero dependências externas / sem build step — arquivos devem rodar abrindo `index.html` direto no navegador.
- Paleta de cores exata: `#0B3568` (azul-marinho), `#1E56A0` (azul royal), `#7DA2D4` (azul claro), `#F5F7FA` (branco gelo). Botão flutuante do WhatsApp usa o verde convencional da marca WhatsApp `#25D366` (convenção de mercado para reconhecimento imediato do botão).
- Mobile-first, responsivo.
- Contatos: WhatsApp `https://wa.me/5585992764459`, e-mail `contato@procorretora.com` (`mailto:`), Instagram `https://www.instagram.com/procorretora/`. Sem endereço físico.
- Nome exibido: "PRO CORRETORA". Logo em `assets/logo.png` (já commitado).

**Nota sobre testes:** este projeto é markup/estilo estático sem lógica de negócio — não há suíte de testes automatizados (adicionar Jest/Playwright violaria a restrição de zero dependências do spec). Cada tarefa é verificada abrindo o arquivo no navegador e checando o comportamento visual/funcional descrito no passo de verificação.

---

### Task 1: Esqueleto do projeto e CSS base

**Files:**
- Create: `index.html`
- Create: `styles.css`
- Create: `README.md`

**Interfaces:**
- Produces: variáveis CSS `--color-navy`, `--color-royal`, `--color-light`, `--color-offwhite`, `--color-whatsapp`, `--container-width`; classe utilitária `.container`; classes `.btn`, `.btn-cta`, `.btn-large`.

- [ ] **Step 1: Criar `index.html` com o esqueleto**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PRO Corretora — Seguros e Investimentos</title>
  <meta name="description" content="PRO Corretora: seguros auto, vida, saúde, residencial, previdência privada e consórcio. Fale conosco no WhatsApp.">
  <link rel="icon" href="assets/logo.png">
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <!-- Header, Hero, Serviços, Sobre, Contato, Rodapé e botão flutuante serão adicionados nas próximas tasks -->
  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Criar `styles.css` com reset, variáveis e utilitários base**

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --color-navy: #0B3568;
  --color-royal: #1E56A0;
  --color-light: #7DA2D4;
  --color-offwhite: #F5F7FA;
  --color-whatsapp: #25D366;
  --container-width: 1100px;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Segoe UI', Arial, sans-serif;
  color: var(--color-navy);
  line-height: 1.5;
  background: #fff;
}

.container {
  max-width: var(--container-width);
  margin: 0 auto;
  padding: 0 1.25rem;
}

.btn {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  border-radius: 999px;
  text-decoration: none;
  font-weight: 600;
  transition: background 0.2s ease;
}

.btn-cta {
  background: var(--color-royal);
  color: #fff;
}

.btn-cta:hover {
  background: var(--color-navy);
}

.btn-large {
  padding: 1rem 2rem;
  font-size: 1.125rem;
}
```

- [ ] **Step 3: Criar `README.md` com instruções básicas**

```markdown
# Site PRO Corretora

Site institucional single-page (HTML/CSS/JS puro, sem build, sem formulários).

## Editar conteúdo

- Textos e links: `index.html`
- Cores e estilo: `styles.css` (variáveis no topo do arquivo, seção `:root`)
- Comportamento do menu mobile: `script.js`

## Ver localmente

Abra `index.html` direto no navegador (duplo clique) — não precisa de servidor nem instalação.

## Publicar (GitHub Pages)

Ver instruções na Task 9 do plano em `docs/superpowers/plans/2026-07-04-corretora-site.md`.
```

- [ ] **Step 4: Verificar no navegador**

Abra `index.html` no navegador. Esperado: página em branco, sem erros no console (F12 → Console).

- [ ] **Step 5: Commit**

```bash
git add index.html styles.css README.md
git commit -m "Add project skeleton and base CSS variables"
```

---

### Task 2: Header, navegação e botão CTA

**Files:**
- Modify: `index.html` (adicionar `<header>` logo após `<body>`)
- Modify: `styles.css` (adicionar ao final)
- Create: `script.js`

**Interfaces:**
- Consumes: `--color-navy`, `--color-light`, `--color-offwhite`, `.btn`, `.btn-cta` (Task 1)
- Produces: classes `.site-header`, `.header-inner`, `.brand`, `.logo`, `.brand-name`, `.site-nav`, `.nav-open`, `.menu-toggle`; elementos com seletores `.menu-toggle` e `.site-nav` consumidos por `script.js`.

- [ ] **Step 1: Adicionar o header em `index.html`** (logo após `<body>`, antes do comentário das próximas seções)

```html
<header class="site-header">
  <div class="container header-inner">
    <div class="brand">
      <img src="assets/logo.png" alt="PRO Corretora" class="logo">
      <span class="brand-name">PRO CORRETORA</span>
    </div>
    <nav class="site-nav">
      <a href="#servicos">Serviços</a>
      <a href="#sobre">Sobre</a>
      <a href="#contato">Contato</a>
    </nav>
    <a class="btn btn-cta" href="https://wa.me/5585992764459" target="_blank" rel="noopener">Fale conosco</a>
    <button class="menu-toggle" aria-label="Abrir menu" aria-expanded="false">☰</button>
  </div>
</header>
```

- [ ] **Step 2: Adicionar estilos do header em `styles.css`**

```css
.site-header {
  position: sticky;
  top: 0;
  background: var(--color-navy);
  z-index: 100;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding: 0.75rem 1.25rem;
  position: relative;
}

.brand {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.logo {
  width: 40px;
  height: 40px;
  border-radius: 50%;
}

.brand-name {
  color: #fff;
  font-weight: 700;
  font-size: 1.1rem;
  letter-spacing: 0.5px;
}

.site-nav {
  display: none;
  gap: 1.5rem;
}

.site-nav a {
  color: var(--color-offwhite);
  text-decoration: none;
  font-weight: 500;
}

.site-nav a:hover {
  color: var(--color-light);
}

.menu-toggle {
  display: inline-flex;
  background: none;
  border: none;
  color: #fff;
  font-size: 1.5rem;
  cursor: pointer;
}

.site-nav.nav-open {
  display: flex;
  flex-direction: column;
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: var(--color-navy);
  padding: 1rem 1.25rem;
  gap: 1rem;
}

@media (min-width: 768px) {
  .site-nav {
    display: flex;
  }

  .menu-toggle {
    display: none;
  }
}
```

- [ ] **Step 3: Criar `script.js` com o toggle do menu mobile**

```javascript
const menuToggle = document.querySelector('.menu-toggle');
const siteNav = document.querySelector('.site-nav');

menuToggle.addEventListener('click', () => {
  const isOpen = siteNav.classList.toggle('nav-open');
  menuToggle.setAttribute('aria-expanded', String(isOpen));
});

siteNav.querySelectorAll('a').forEach((link) => {
  link.addEventListener('click', () => {
    siteNav.classList.remove('nav-open');
    menuToggle.setAttribute('aria-expanded', 'false');
  });
});
```

- [ ] **Step 4: Verificar no navegador**

Abra `index.html`. Redimensione a janela para < 768px de largura: o menu deve virar um botão "☰"; clicar nele deve abrir/fechar a navegação. Em largura >= 768px, os links "Serviços / Sobre / Contato" devem aparecer diretamente, sem o botão hamburger. Sem erros no console.

- [ ] **Step 5: Commit**

```bash
git add index.html styles.css script.js
git commit -m "Add sticky header with nav and mobile menu toggle"
```

---

### Task 3: Seção Hero

**Files:**
- Modify: `index.html` (adicionar `<section class="hero">` logo após `</header>`)
- Modify: `styles.css` (adicionar ao final)

**Interfaces:**
- Consumes: `--color-royal`, `--color-navy`, `.btn`, `.btn-cta`, `.btn-large` (Tasks 1-2)

- [ ] **Step 1: Adicionar a seção hero em `index.html`**

```html
<section class="hero">
  <div class="container hero-inner">
    <h1>Proteção e planejamento financeiro para você e sua família</h1>
    <p>Seguros e investimentos com atendimento direto, sem burocracia.</p>
    <a class="btn btn-cta btn-large" href="https://wa.me/5585992764459" target="_blank" rel="noopener">Falar no WhatsApp</a>
  </div>
</section>
```

- [ ] **Step 2: Adicionar estilos do hero em `styles.css`**

```css
.hero {
  background: linear-gradient(135deg, var(--color-royal), var(--color-navy));
  color: #fff;
  padding: 4rem 0;
  text-align: center;
}

.hero-inner {
  max-width: 700px;
}

.hero h1 {
  font-size: 1.75rem;
  margin-bottom: 1rem;
}

.hero p {
  font-size: 1.1rem;
  margin-bottom: 1.5rem;
  opacity: 0.9;
}

@media (min-width: 768px) {
  .hero h1 {
    font-size: 2.5rem;
  }
}
```

- [ ] **Step 3: Verificar no navegador**

Abra `index.html`. Esperado: seção com fundo em degradê azul, título, subtítulo e botão "Falar no WhatsApp" centralizados; título menor em telas estreitas e maior a partir de 768px.

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "Add hero section"
```

---

### Task 4: Seção Serviços

**Files:**
- Modify: `index.html` (adicionar `<section id="servicos">` logo após a seção hero)
- Modify: `styles.css` (adicionar ao final)

**Interfaces:**
- Consumes: `--color-navy`, `--color-royal`, `--color-light` (Task 1)
- Produces: classes `.services`, `.services-grid`, `.service-card` (consumidas apenas visualmente, sem dependência de outras tasks)

- [ ] **Step 1: Adicionar a seção de serviços em `index.html`**

```html
<section id="servicos" class="services">
  <div class="container">
    <h2>Nossos Serviços</h2>
    <div class="services-grid">
      <article class="service-card">
        <h3>Seguro Auto</h3>
        <p>Cobertura completa para o seu veículo, com assistência 24h.</p>
      </article>
      <article class="service-card">
        <h3>Seguro Vida</h3>
        <p>Proteção financeira para você e para quem depende de você.</p>
      </article>
      <article class="service-card">
        <h3>Seguro Saúde</h3>
        <p>Planos de saúde sob medida para você e sua família.</p>
      </article>
      <article class="service-card">
        <h3>Seguro Residencial</h3>
        <p>Sua casa protegida contra incêndio, roubo e outros imprevistos.</p>
      </article>
      <article class="service-card">
        <h3>Previdência Privada</h3>
        <p>Planejamento para construir seu futuro financeiro com segurança.</p>
      </article>
      <article class="service-card">
        <h3>Consórcios</h3>
        <p>Realize conquistas como veículo ou imóvel de forma planejada.</p>
      </article>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Adicionar estilos da seção em `styles.css`**

```css
.services {
  padding: 4rem 0;
  background: #fff;
}

.services h2 {
  text-align: center;
  color: var(--color-navy);
  margin-bottom: 2rem;
  font-size: 1.75rem;
}

.services-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

@media (min-width: 600px) {
  .services-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 900px) {
  .services-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

.service-card {
  background: var(--color-offwhite);
  border: 1px solid var(--color-light);
  border-radius: 12px;
  padding: 1.5rem;
  text-align: center;
}

.service-card h3 {
  color: var(--color-royal);
  margin-bottom: 0.5rem;
}
```

- [ ] **Step 3: Verificar no navegador**

Abra `index.html` e clique em "Serviços" no menu: deve rolar suavemente até a seção. Esperado: 1 coluna no mobile, 2 colunas a partir de 600px, 3 colunas a partir de 900px, com os 6 cards de serviço.

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "Add services section with responsive grid"
```

---

### Task 5: Seção Sobre nós

**Files:**
- Modify: `index.html` (adicionar `<section id="sobre">` logo após a seção de serviços)
- Modify: `styles.css` (adicionar ao final)

**Interfaces:**
- Consumes: `--color-navy`, `--color-offwhite` (Task 1)

- [ ] **Step 1: Adicionar a seção "Sobre nós" em `index.html`**

```html
<section id="sobre" class="about">
  <div class="container">
    <h2>Sobre nós</h2>
    <p class="about-text">A PRO Corretora nasceu para simplificar a forma como você protege o que importa e planeja o seu futuro. Trabalhamos com seguros auto, vida, saúde e residencial, além de soluções de previdência privada e consórcio, sempre com atendimento direto e sem burocracia. Fale com a gente e encontre a solução certa pra sua necessidade.</p>
  </div>
</section>
```

- [ ] **Step 2: Adicionar estilos em `styles.css`**

```css
.about {
  padding: 4rem 0;
  background: var(--color-offwhite);
}

.about h2 {
  text-align: center;
  color: var(--color-navy);
  margin-bottom: 1.5rem;
  font-size: 1.75rem;
}

.about-text {
  max-width: 700px;
  margin: 0 auto;
  text-align: center;
  font-size: 1.05rem;
}
```

- [ ] **Step 3: Verificar no navegador**

Abra `index.html` e clique em "Sobre" no menu: deve rolar até a seção com fundo levemente diferente (branco-gelo) e o texto centralizado, largura máxima legível.

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "Add about us section"
```

---

### Task 6: Seção Contatos

**Files:**
- Modify: `index.html` (adicionar `<section id="contato">` logo após a seção "Sobre nós")
- Modify: `styles.css` (adicionar ao final)

**Interfaces:**
- Consumes: `--color-navy`, `--color-royal`, `--color-light` (Task 1)

- [ ] **Step 1: Adicionar a seção de contatos em `index.html`**

```html
<section id="contato" class="contact">
  <div class="container">
    <h2>Fale com a gente</h2>
    <div class="contact-grid">
      <a class="contact-card" href="https://wa.me/5585992764459" target="_blank" rel="noopener">
        <svg class="contact-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
        </svg>
        <span>WhatsApp / Telefone<br>+55 85 9 9276 4459</span>
      </a>
      <a class="contact-card" href="mailto:contato@procorretora.com">
        <svg class="contact-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M4 4h16v16H4z"/>
          <path d="M4 6l8 7 8-7"/>
        </svg>
        <span>E-mail<br>contato@procorretora.com</span>
      </a>
      <a class="contact-card" href="https://www.instagram.com/procorretora/" target="_blank" rel="noopener">
        <svg class="contact-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <rect x="3" y="3" width="18" height="18" rx="5"/>
          <circle cx="12" cy="12" r="4"/>
          <circle cx="17.5" cy="6.5" r="1"/>
        </svg>
        <span>Instagram<br>@procorretora</span>
      </a>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Adicionar estilos em `styles.css`**

```css
.contact {
  padding: 4rem 0;
  background: #fff;
}

.contact h2 {
  text-align: center;
  color: var(--color-navy);
  margin-bottom: 2rem;
  font-size: 1.75rem;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

@media (min-width: 700px) {
  .contact-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

.contact-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  background: var(--color-offwhite);
  border: 1px solid var(--color-light);
  border-radius: 12px;
  padding: 1.5rem;
  text-decoration: none;
  color: var(--color-navy);
  text-align: center;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.contact-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 20px rgba(11, 53, 104, 0.15);
}

.contact-icon {
  width: 32px;
  height: 32px;
  color: var(--color-royal);
}
```

- [ ] **Step 3: Verificar no navegador**

Abra `index.html` e clique em "Contato" no menu: deve rolar até 3 cartões (mobile: empilhados; desktop >= 700px: lado a lado). Passar o mouse sobre um cartão deve elevá-lo levemente. Clicar no cartão de e-mail deve abrir o cliente de e-mail padrão (`mailto:`); WhatsApp e Instagram abrem em nova aba.

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "Add contact section with WhatsApp, email and Instagram links"
```

---

### Task 7: Rodapé e botão flutuante do WhatsApp

**Files:**
- Modify: `index.html` (adicionar `<footer>` após a seção de contatos, e o botão flutuante logo antes de `<script src="script.js">`)
- Modify: `styles.css` (adicionar ao final)

**Interfaces:**
- Consumes: `--color-navy`, `--color-offwhite`, `--color-light`, `--color-whatsapp` (Task 1)

- [ ] **Step 1: Adicionar rodapé e botão flutuante em `index.html`**

```html
<footer class="site-footer">
  <div class="container">
    <p>&copy; 2026 PRO Corretora. Todos os direitos reservados.</p>
    <div class="footer-social">
      <a href="https://www.instagram.com/procorretora/" target="_blank" rel="noopener">Instagram</a>
    </div>
  </div>
</footer>

<a class="whatsapp-float" href="https://wa.me/5585992764459" target="_blank" rel="noopener" aria-label="Fale conosco no WhatsApp">
  <svg viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2">
    <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
  </svg>
</a>
```

- [ ] **Step 2: Adicionar estilos em `styles.css`**

```css
.site-footer {
  background: var(--color-navy);
  color: var(--color-offwhite);
  text-align: center;
  padding: 2rem 0;
}

.footer-social a {
  color: var(--color-light);
  text-decoration: none;
  margin-top: 0.5rem;
  display: inline-block;
}

.whatsapp-float {
  position: fixed;
  bottom: 1.5rem;
  right: 1.5rem;
  width: 56px;
  height: 56px;
  background: var(--color-whatsapp);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.25);
  z-index: 200;
}

.whatsapp-float svg {
  width: 28px;
  height: 28px;
}
```

- [ ] **Step 3: Verificar no navegador**

Abra `index.html`, role a página inteira: o botão circular verde de WhatsApp deve permanecer fixo no canto inferior direito o tempo todo. O rodapé deve mostrar o texto de copyright e o link do Instagram.

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "Add footer and floating WhatsApp button"
```

---

### Task 8: Revisão final de responsividade e acessibilidade

**Files:**
- Modify: `styles.css` (ajustes pontuais, se necessário)

- [ ] **Step 1: Checklist manual de verificação**

Abra `index.html` e verifique, em pelo menos 3 larguras (ex: 375px celular, 768px tablet, 1280px desktop):

1. Nenhum texto ou elemento vaza horizontalmente (sem scroll lateral indesejado).
2. Header permanece fixo no topo e não sobrepõe o conteúdo abaixo dele.
3. Menu mobile abre/fecha corretamente abaixo de 768px.
4. Todos os links (`Serviços`, `Sobre`, `Contato`, botões CTA, cartões de contato, botão flutuante) funcionam e apontam para os destinos corretos.
5. Contraste de texto legível em todas as seções (texto escuro sobre fundo claro, texto claro sobre fundo escuro).
6. Botão flutuante do WhatsApp não sobrepõe conteúdo importante no rodapé em telas pequenas — se sobrepuser, ajuste `bottom`/`right` em `.whatsapp-float` para uma seção estreita.

- [ ] **Step 2: Corrigir quaisquer problemas encontrados diretamente em `styles.css`**

(Sem placeholder — se o Step 1 não encontrar problemas, pule para o commit.)

- [ ] **Step 3: Commit** (somente se houver alterações)

```bash
git add styles.css
git commit -m "Polish responsive layout after manual QA"
```

---

### Task 9: Publicar no GitHub Pages

**Files:**
- Nenhum arquivo de código — apenas configuração de repositório remoto.

- [ ] **Step 1: Criar repositório no GitHub**

Acesse https://github.com/new, crie um repositório público chamado `corretora-site` (ou nome de sua preferência), sem inicializar com README (o projeto já tem um).

- [ ] **Step 2: Conectar o repositório local ao remoto**

```bash
cd /c/Users/devic/projects/corretora-site
git remote add origin https://github.com/<seu-usuario>/corretora-site.git
git branch -M main
git push -u origin main
```

- [ ] **Step 3: Ativar o GitHub Pages**

No GitHub: `Settings` → `Pages` → em "Build and deployment", selecione `Source: Deploy from a branch`, `Branch: main`, pasta `/ (root)` → `Save`.

- [ ] **Step 4: Verificar publicação**

Aguarde 1-2 minutos e acesse a URL exibida em `Settings` → `Pages` (formato `https://<seu-usuario>.github.io/corretora-site/`). Esperado: o site carrega igual ao teste local, com logo, seções e botão de WhatsApp funcionando.

# Site institucional — PRO Corretora

## Contexto e objetivo

PRO Corretora (seguros e investimentos) precisa de um site institucional simples. Objetivo: apresentar os serviços, um breve "sobre nós" e os contatos da empresa, direcionando o visitante para o WhatsApp para qualificação de lead (feita por um bot separado, fora do escopo deste projeto). Sem formulários e sem coleta de dados — decisão deliberada para evitar exposição a obrigações de LGPD, dado o baixo nível de familiaridade da equipe com tratamento de dados pessoais.

## Escopo

Site estático de uma única página (single-page, com scroll), hospedado no GitHub Pages.

Fora de escopo: formulários de contato, backend, banco de dados, bot de WhatsApp (etapa seguinte, tratada separadamente).

## Abordagem técnica

HTML/CSS/JS puro, sem build step e sem dependências. Justificativa: o site não tem interatividade além de links e scroll suave; um framework ou gerador de site estático adicionaria complexidade de manutenção sem benefício, e o dono do site tem pouca experiência técnica — arquivos simples são mais fáceis de editar no futuro.

## Identidade visual

Logo em `assets/logo.png` (fornecido pelo cliente). Paleta extraída por amostragem de pixels do logo:

| Cor | Hex | Uso |
|---|---|---|
| Azul-marinho profundo | `#0B3568` | Fundo principal / texto sobre claro |
| Azul royal | `#1E56A0` | Botões, CTA, destaques |
| Azul claro / prata | `#7DA2D4` | Bordas, ícones, detalhes |
| Branco gelo | `#F5F7FA` | Fundo de seções claras, texto sobre azul |

## Estrutura da página

1. **Header fixo** — logo + "PRO CORRETORA" + navegação âncora (Serviços / Sobre / Contato) + botão "Fale conosco" em destaque
2. **Hero** — frase de impacto + CTA principal para WhatsApp
3. **Serviços** — grid de cards: Seguro Auto, Seguro Vida, Seguro Saúde, Seguro Residencial, Previdência Privada, Consórcios
4. **Sobre nós** — texto curto (ver Conteúdo abaixo)
5. **Contatos** — telefone/WhatsApp, e-mail, Instagram, com ícones e links diretos
6. **Rodapé** — nome, ano, redes sociais
7. **Botão flutuante de WhatsApp** — fixo no canto inferior direito, visível durante o scroll

## Conteúdo

**Nome exibido:** PRO CORRETORA

**Serviços:**
- Seguro Auto
- Seguro Vida
- Seguro Saúde
- Seguro Residencial
- Previdência Privada
- Consórcios

**Sobre nós (rascunho aprovado, ajustável):**
> A PRO Corretora nasceu para simplificar a forma como você protege o que importa e planeja o seu futuro. Trabalhamos com seguros auto, vida, saúde e residencial, além de soluções de previdência privada e consórcio, sempre com atendimento direto e sem burocracia. Fale com a gente e encontre a solução certa pra sua necessidade.

**Contatos:**
- WhatsApp/Telefone: +55 85 9 9276 4459 (link `https://wa.me/5585992764459`)
- E-mail: contato@procorretora.com (link `mailto:`)
- Instagram: https://www.instagram.com/procorretora/
- Sem endereço físico (atendimento remoto)

## Comportamento e dados

- Nenhum formulário, nenhuma coleta de dados de visitantes, nenhum cookie de rastreamento — sem superfície de exposição a LGPD.
- Todo contato direciona para canais externos (WhatsApp, e-mail, Instagram) já operados pela empresa.
- Site responsivo (mobile-first), já que a maior parte do tráfego deve vir de celular e converter em clique no WhatsApp.

## Testes / verificação

- Verificação manual visual em desktop e mobile (viewport simulado).
- Checar todos os links externos (WhatsApp, e-mail, Instagram) abrem corretamente.
- Validar responsividade nas seções (header, grid de serviços, contatos).

## Deploy

Repositório Git local nesta pasta, publicado via GitHub Pages quando o repositório remoto for criado.

# Leque de Eventos

Catálogo estático de eventos desenvolvido como parte do curso de Frontend Avançado.

O projeto utiliza HTML semântico e CSS moderno, com foco em responsividade, acessibilidade e organização da cascata.

---

## 📁 Estrutura do projeto

```text
leque-de-eventos-estatico/
├── index.html
├── eventos.html
├── evento.html
├── css/
│   ├── tokens.css
│   ├── base.css
│   └── componentes.css
└── README.md

🎯 Páginas

Home

Apresenta o catálogo e alguns eventos em destaque.

Listagem

Apresenta os 8 eventos disponíveis no catálogo.

Detalhe

Apresenta as informações completas de um evento.

🎫 Catálogo de eventos

O catálogo possui 8 eventos plausíveis, contemplando diferentes categorias, formatos, preços e níveis.

Evento	Categoria	Formato	Local
React Recife · Meetup #42	Tecnologia	Presencial	Recife - PE
CSS Beyond the Box	Design	Online	Online
Java & Spring Boot Conference	Tecnologia	Híbrido	João Pessoa - PB
Product Builders Nordeste	Negócios	Presencial	Fortaleza - CE
Web Performance Day	Tecnologia	Online	Online
Design Systems na Prática	Design	Híbrido	Recife - PE
Tech Careers Summit	Carreira	Presencial	João Pessoa - PB
Cloud Native Brasil	Tecnologia	Online	Online
🎨 Tokens CSS

Os valores reutilizáveis do projeto foram centralizados em css/tokens.css.

A utilização de custom properties evita valores espalhados pelo CSS e facilita futuras alterações de identidade visual.

Token	Função
--cor-fundo	Cor principal do fundo
--cor-superficie	Fundo de cards e superfícies
--cor-texto	Texto principal
--cor-texto-suave	Texto secundário
--cor-marca	Cor principal da identidade
--cor-marca-hover	Cor da marca em interação
--cor-borda	Bordas
--cor-ok	Estados positivos e eventos gratuitos
--esp-1	Espaçamento pequeno
--esp-2	Espaçamento médio
--esp-3	Espaçamento grande
--esp-4	Espaçamento extra
--esp-5	Espaçamento de seção
--raio	Raio padrão dos componentes
--largura-conteudo	Largura máxima do conteúdo

Os tokens são nomeados de acordo com seu papel, e não pela aparência.

Por exemplo:

--cor-marca

é preferível a:

--roxo

porque a marca pode mudar de cor sem que o nome do token deixe de fazer sentido.

🌓 Temas

O projeto possui tema claro e escuro utilizando:

color-scheme: light dark;

O tema escuro é aplicado de acordo com a preferência do sistema operacional ou navegador:

@media (prefers-color-scheme: dark) {
  :root {
    /* tokens do tema escuro */
  }
}

Não foi utilizado JavaScript para controlar o tema.

📦 Organização do CSS

O CSS foi dividido em três arquivos:

tokens.css

Responsável pelas custom properties, paleta, espaçamentos, tipografia e temas.

base.css

Responsável pelo reset, elementos gerais, tipografia, links, foco e estrutura global da página.

componentes.css

Responsável pelo cabeçalho, rodapé, lista de eventos, cards, Container Queries e demais componentes específicos.

A cascata foi organizada utilizando:

@layer reset, base, componentes, utilitarios;

A ordem das camadas é:

reset
  ↓
base
  ↓
componentes
  ↓
utilitarios

A camada utilitarios foi declarada para estabelecer a arquitetura da cascata, mas não possui regras específicas neste projeto.

📐 @container

Foi utilizado @container nos cards de eventos.

Cada item da lista funciona como um container:

.lista-eventos > li {
  container-type: inline-size;
}

O card muda seu layout quando o espaço disponível dentro desse container chega a pelo menos 420px:

@container (min-width: 420px) {
  .card-evento {
    display: grid;
    grid-template-columns: 120px 1fr;
    gap: var(--esp-2);
  }
}
Por que usar @container?

O comportamento do card depende do espaço que o próprio componente recebe, e não do tamanho total da tela.

Isso permite que o mesmo componente seja utilizado em diferentes contextos e larguras sem precisar criar uma regra específica para cada tamanho de dispositivo.

Na home, a lista também pode estar dentro de um container mais estreito:

.lista-eventos-container {
  width: min(100%, 32rem);
}

Assim, o mesmo card consegue se adaptar ao espaço disponível.

🔎 :has()

O pseudo-classe :has() foi utilizado para identificar visualmente os cards de eventos gratuitos:

.card-evento:has(.selo-gratuito) {
  border-color: var(--cor-ok);
}

O card recebe uma borda com a cor de sucesso quando contém o selo:

<p class="selo-gratuito">
  Gratuito
</p>
O que isso evita?

Não foi necessário adicionar uma classe extra ao card apenas para indicar que ele é gratuito.

Em vez de:

<article class="card-evento evento-gratuito">

o CSS consegue reagir diretamente à presença do conteúdo:

.card-evento:has(.selo-gratuito)

Dessa forma, o estilo é baseado na estrutura real do componente.

🧱 @layer e cascata

A utilização de @layer permite organizar a prioridade das regras CSS de maneira explícita.

A ordem utilizada no projeto é:

@layer reset, base, componentes, utilitarios;

Isso permite separar as responsabilidades de cada grupo de regras e reduz a necessidade de aumentar a especificidade dos seletores para resolver conflitos.

Durante o desenvolvimento, a organização das camadas foi utilizada para evitar a necessidade de recorrer a !important.

O projeto final possui:

0 ocorrências de !important
⌨️ Acessibilidade e navegação por teclado

O projeto possui um link para pular diretamente para o conteúdo principal:

<a class="skip-link" href="#conteudo">
  Pular para o conteúdo
</a>

Ele é o primeiro elemento focável das páginas.

Também foi implementado um indicador visual de foco:

:focus-visible {
  outline: 2px solid var(--cor-marca);
  outline-offset: 2px;
}

As três páginas foram testadas utilizando somente:

Tab
Shift + Tab
Enter

Durante o teste foi verificado que:

o Skip Link aparece no primeiro Tab;
o Skip Link leva ao conteúdo principal;
os links podem receber foco;
o foco permanece visualmente perceptível;
a ordem de navegação é lógica;
os links podem ser ativados com Enter.
📱 Responsividade

A listagem utiliza CSS Grid:

grid-template-columns:
  repeat(
    auto-fit,
    minmax(min(280px, 100%), 1fr)
  );

O uso de auto-fit permite que os cards se reorganizem automaticamente conforme o espaço disponível.

O trecho:

minmax(min(280px, 100%), 1fr)

evita que o tamanho mínimo do card provoque rolagem horizontal em telas estreitas.

A estrutura geral da página utiliza:

min-height: 100dvh;

junto com Grid para manter o rodapé na parte inferior da página quando houver pouco conteúdo.

🧩 HTML semântico

As páginas utilizam elementos HTML semânticos, incluindo:

<header>
<nav>
<main>
<section>
<article>
<footer>
<ul>
<li>
<time>

Cada página possui:

exatamente um <main>;
um <h1>;
hierarquia de títulos sem saltos;
navegação identificada com aria-label.

A listagem utiliza <ul> e cada evento é representado por um <article> dentro de um <li>.

As datas utilizam o atributo datetime:

<time datetime="2026-09-12T19:00">
  12 de setembro, 19h
</time>
🚫 Tecnologias não utilizadas

O projeto foi desenvolvido sem:

JavaScript;
Bootstrap;
Tailwind;
bibliotecas de componentes;
frameworks frontend.

Todo o comportamento apresentado é obtido utilizando HTML e CSS.

♿ Acessibilidade

Foram adotadas práticas de acessibilidade durante a construção das páginas.

Entre elas:

Skip Link;
foco visível com :focus-visible;
navegação por teclado;
HTML semântico;
hierarquia adequada de títulos;
links reais com destinos válidos;
identificação do <main>;
datas utilizando <time datetime>.

O projeto também evita:

outline: none;

sem substituição visual e não utiliza:

!important;
👥 Equipe
Pessoa	Responsabilidades
João Gabriel	Desenvolvimento do projeto
📊 Checklist da entrega
 Três telas
 8 eventos
 Link "pular para o conteúdo"
 Um <main> por página
 Um <h1> por página
 Hierarquia de títulos
 Lista usando <ul>
 Cards usando <article>
 Datas usando <time datetime>
 Custom properties
 Tema claro e escuro
 CSS Grid
 CSS Flexbox
 auto-fit
 @container
 @layer
 :has()
 Zero !important
 Navegação por teclado
 :focus-visible
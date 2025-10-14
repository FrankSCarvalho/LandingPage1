# LandingPage1

Este é um tutorial passo a passo para construir a Landing Page responsiva e animada, utilizando HTML, CSS, JavaScript e jQuery, conforme demonstrado no vídeo.
Siga os passos e as estruturas de código fornecidas para construir a página junto.

--------------------------------------------------------------------------------
## Configuração Inicial e Estrutura de Arquivos
O primeiro passo é organizar o ambiente de trabalho e criar a estrutura básica de arquivos.
1. Criação da Pasta: Crie uma pasta chamada Landing page.
2. Abertura no VS Code: Abra esta pasta no VS Code e utilize a extensão Live Server para rodar o projeto.
3. Estrutura de Arquivos: Crie os seguintes arquivos e pastas:
    - index.html
    - Pasta Styles/
    - Pasta JavaScript/
    - JavaScript/script.js
4. HTML Básico: No `index.html`, insira a estrutura básica de HTML (use ! e dê Enter).
    - Troque a linguagem para PT-BR.
    - Troque o título para Landing page.
5. Inclusão de Bibliotecas e Scripts \
Adicione os seguintes links de bibliotecas e scripts ao seu `index.html`:
    1. Font Awesome (Ícones): No `<head>`, adicione o CDN do Font Awesome para usar os ícones.
    2. jQuery: No `<head>`, adicione o CDN do jQuery, que será usado para a interatividade.
    3. JavaScript: Importe seu arquivo de script no final do `<body>`: \
`<!-- index.html (dentro de <head>) -->` \
`<link rel="stylesheet" href="[LINK DO FONT AWESOME CDN]">` \
`<script src="[LINK DO JQUERY CDN]"></script>` \
`<!-- index.html (no final de <body>) -->` \
`<script src="src/JavaScript/script.js"></script>` \
## Estrutura CSS e Estilos Gerais ()
O `styles.css` será o arquivo geral para resets, fontes e estilos de componentes reutilizáveis, como botões.
    1. Criação do Arquivo: Crie `styles.css` dentro da pasta Styles.
    2. Importação de Fontes: Use `@import` para importar a fonte Poppins do Google Fonts.
    3. Reset e Base: Aplique o reset básico:
/* Styles/styles.css */
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box; /* Ajuda na responsividade [8] */
    font-family: 'Poppins', sans-serif; /* Fonte Poppins [8] */
}

body {
    background-color: #F9F9EA; /* Cor de fundo padrão [8] */
}

/* Estilo para todas as seções [9] */
section {
    padding: 28px 8%; /* Mesmo padding usado no header [9] */
}
4. Botão Padrão (.btn-defu): Estilize o botão padrão (componente reutilizável) em styles.css:
/* Styles/styles.css */
.btn-defu {
    border: none;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #FCB45; /* Amarelo primário [10] */
    border-radius: 12px;
    padding: 10px 14px;
    font-weight: 600;
    cursor: pointer;
    box-shadow: 0 0 0 2px rgba(0, 0, 0, 0.1);
    transition: background-color 0.3s ease; /* Transição suave [11] */
}

.btn-defu:hover {
    background-color: #F8D477; /* Cor do hover [11] */
}
3. Construção do Header e Navegação
Vamos construir a navegação (header) em HTML e estilizar em header.css.
HTML do Header
No index.html, crie a estrutura do header:
<!-- index.html (dentro de <body>) -->
<header>
    <nav id="nav_bar">
        <!-- Logo [14] -->
        <i class="fa-solid fa-burger" id="nav_logo">Food</i>
        
        <!-- Menu para Desktop [14, 15] -->
        <ul id="nav_list">
            <li class="nav-item active">
                <a href="#home">Início</a>
            </li>
            <li class="nav-item">
                <a href="#menu">Cardápio</a>
            </li>
            <li class="nav-item">
                <a href="#testimonials">Avaliações</a>
            </li>
        </ul>

        <!-- Botão Peça Aqui [15] -->
        <button class="btn-defu">Peça aqui</button>
        
        <!-- Botão Mobile [16] -->
        <button id="mobile_btn">
            <i class="fa-solid fa-bars"></i>
        </button>
    </nav>
    
    <!-- Menu Mobile (Inicialmente oculto) [16] -->
    <div id="mobile_menu">
        <ul id="mobile_nav_list">
            <!-- Copiar os <li> do nav_list aqui [16] -->
            <li class="nav-item active"><a href="#home">Início</a></li>
            <li class="nav-item"><a href="#menu">Cardápio</a></li>
            <li class="nav-item"><a href="#testimonials">Avaliações</a></li>
        </ul>
        <button class="btn-defu">Peça aqui</button>
    </div>
</header>
CSS do Header ()
1. Crie header.css dentro de Styles.
2. Importação: Por enquanto, importe ele no index.html (futuramente faremos a unificação).
3. Estilização:
/* Styles/header.css */
header {
    width: 100%;
    padding: 28px 8%;
    position: sticky; /* Fixar no topo [17] */
    top: 0; /* Fixar no topo [17] */
    background-color: #F9F9EA; /* Cor de fundo para não ficar transparente [18] */
    z-index: 3; /* Garantir que fique acima de outros elementos [18] */
}

#nav_bar {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between; /* Elementos nas pontas [19] */
}

/* Estilo da Logo [20] */
#nav_logo {
    font-size: 24px;
    color: #E9A209;
}

/* Lista de Navegação (Desktop) [20] */
#nav_list {
    display: flex;
    list-style: none; /* Remove a bolinha [20] */
    gap: 48px;
}

#nav_item a {
    text-decoration: none;
    color: #1D1D1D;
    font-weight: 600;
}

/* Classe Ativa [21] */
.nav-item.active a {
    color: #1D1D1D;
    border-bottom: 3px solid #F8D477; /* Risquinho embaixo [21] */
}

/* Esconder elementos Mobile (inicialmente) [22] */
#mobile_btn, #mobile_menu {
    display: none;
}
Responsividade do Header (Media Query)
Adicione a media query para telas menores que 1170px:
/* Styles/header.css (no final) */
@media screen and (max-width: 1170px) {
    /* Oculta lista e botão Peça aqui no desktop [23] */
    #nav_list, .btn-defu {
        display: none;
    }
    
    /* Mostra o botão mobile [23] */
    #mobile_btn {
        display: block;
        border: none;
        background-color: transparent;
        font-size: 1.5rem;
        cursor: pointer;
    }

    /* Estiliza o menu mobile quando ativo [5, 24] */
    #mobile_menu.active {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    
    #mobile_nav_list {
        display: flex;
        flex-direction: column;
        gap: 12px;
        margin: 12px 0;
    }

    #mobile_nav_list .nav-item {
        list-style: none; /* Remove bolinhas no mobile [24] */
        text-align: center;
    }
}
Interatividade da Nav Bar (jQuery)
No JavaScript/script.js, inicialize o jQuery e adicione a lógica para o menu mobile:
// JavaScript/script.js

$(document).ready(function() {
    // 1. Lógica do Botão Mobile [5, 25, 26]
    $('#mobile_btn').on('click', function() {
        $('#mobile_menu').toggleClass('active'); // Adiciona/remove 'active' no menu [5]
        $('#mobile_btn').find('i').toggleClass('fa-x'); // Troca o ícone (barras <-> X) [26]
    });
});
4. Construção da Seção Home
A seção home contém o CTA (Título, Descrição, Botões) e o Banner (Imagem e Forma Geométrica).
HTML da Home
Crie a seção main e a primeira section abaixo do header:
<!-- index.html (abaixo de </header>) -->
<main id="content">
    <section id="home">
        <!-- Forma geométrica (Shape) [29] -->
        <div class="shape"></div>

        <!-- CTA - Call to Action [30] -->
        <div id="cta">
            <h1 id="cta_title">
                O Sabor vai até <br>
                <span style="color: #E9A209;">você</span>
            </h1>
            <p class="description">
                [Texto de descrição aleatório]
            </p>

            <!-- Botões [31] -->
            <div id="cta_buttons">
                <a href="#menu" class="btn-defu">Ver Cardápio</a>
                <a href="tel:+555555555" id="phone_button">
                    <button class="btn-defu">
                        <i class="fa-solid fa-phone"></i>
                    </button>
                    [Número de Telefone]
                </a>
            </div>

            <!-- Botões de Mídia Social [32] -->
            <div class="social-media-buttons">
                <a href="[Link WhatsApp]"><i class="fa-brands fa-whatsapp"></i></a>
                <a href="[Link Instagram]"><i class="fa-brands fa-instagram"></i></a>
                <a href="[Link Facebook]"><i class="fa-brands fa-facebook"></i></a>
            </div>
        </div>

        <!-- Banner (Imagem) [33] -->
        <div id="banner">
            <!-- Arraste sua imagem hero.png para a pasta src/images/ [33] -->
            <img src="src/images/hero.png" alt="Prato principal">
        </div>
    </section>
    <!-- Outras seções virão aqui -->
</main>
CSS da Home ()
1. Crie home.css dentro de Styles e importe-o no index.html.
2. Estilização Base:
/* Styles/home.css */

/* Defina position relative para o shape funcionar [35] */
#home {
    display: flex;
    min-height: calc(100vh - 91px); /* Desconta a nav bar [34] */
    position: relative; 
}

/* Estilo do CTA [36] */
#cta {
    width: 35%; /* Ocupa menos espaço que o banner [36] */
    display: flex;
    flex-direction: column;
    gap: 28px;
    margin-top: 5%;
}

#cta_title {
    font-size: 4rem;
    color: #1D1D1D;
}

.description {
    font-size: 1.2rem;
}

#cta_buttons {
    display: flex;
    gap: 24px;
}

/* Estilizando o botão de telefone [37] */
#phone_button {
    text-decoration: none;
    color: #1D1D1D;
    display: flex;
    gap: 8px;
    align-items: center;
    background-color: #fff;
    padding: 8px 14px;
    border-radius: 12px;
    font-weight: 500;
    box-shadow: 0 0 12px 4px rgba(0, 0, 0, 0.1);
}
#phone_button .btn-defu {
    box-shadow: none; /* Remove sombra do botão interno [38] */
}
3. Estilização dos Botões de Mídia Social (em styles.css)
/* Styles/styles.css (Adicione aqui) */
.social-media-buttons {
    display: flex;
    gap: 18px;
}

.social-media-buttons a {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 45px;
    height: 40px;
    background-color: #fff;
    border-radius: 10px;
    font-size: 1.25rem;
    color: #1D1D1D;
    box-shadow: 0 0 12px 4px rgba(0, 0, 0, 0.1);
    transition: box-shadow 0.3s ease;
}

.social-media-buttons a:hover {
    box-shadow: 0 0 12px 8px rgba(0, 0, 0, 0.1); /* Sombra maior no hover [39] */
}
4. Estilização do Banner e Shape (em home.css)
/* Styles/home.css (Continuação) */

#banner {
    display: flex;
    align-items: start;
    justify-content: end;
    width: 70%;
    z-index: 2; /* Fica por cima da forma [35] */
}

#banner img {
    height: 100%;
    width: fit-content;
}

/* Forma Geométrica [35, 40] */
.shape {
    background-color: #FFE8B4; 
    width: 50%;
    height: 100%;
    position: absolute; /* Posição absoluta dentro do #home [40] */
    top: 0;
    right: 0;
    /* Border radius complexo para formar a onda [35] */
    border-radius: 40% 30% 0% 20%; 
    z-index: 1; /* Fica por baixo do banner [35] */
}
Responsividade da Home
/* Styles/home.css (no final) */

@media screen and (max-width: 1170px) {
    #home {
        flex-direction: column;
        min-height: 100%;
        padding-top: 0;
    }
    
    /* Oculta o banner, imagem e shape em telas menores [41] */
    #banner, #banner img, .shape {
        display: none;
    }

    #cta {
        width: 100%; /* Ocupa 100% da largura [41] */
        align-items: center; /* Centraliza itens [41] */
        text-align: center; /* Centraliza texto [41] */
    }
}

@media screen and (max-width: 450px) {
    /* Oculta o botão de telefone em telas muito pequenas [42] */
    #phone_button {
        display: none;
    }
}
5. Construção da Seção Cardápio ()
Estilos de Título Comuns (em )
Adicione os estilos dos títulos de seção ao seu arquivo geral, pois serão reutilizados:
/* Styles/styles.css (Adicione aqui) */
.section-title {
    color: #E9A209;
    font-size: 1.563rem; 
}

.section-subtitle {
    font-size: 2.1875rem;
}
HTML do Cardápio
Crie a seção menu abaixo da home:
<!-- index.html (abaixo de </section id="home">) -->
<section id="menu">
    <h2 class="section-title">Cardápio</h2>
    <h3 class="section-subtitle">Nossos pratos especiais</h3>

    <div id="dishes">
        <!-- Prato 1 (.dish) [45] -->
        <div class="dish">
            <div class="dish-heart">
                <i class="fa-solid fa-heart"></i>
            </div>
            
            <!-- Arraste suas imagens (dish1.png, dish2.png...) para src/images/ [46] -->
            <img src="src/images/dish1.png" alt="Prato 1" class="dish-image">
            
            <h3 class="dish-title">[Nome do Prato]</h3>
            
            <p class="dish-description">
                [Descrição do Prato]
            </p>
            
            <!-- Avaliação [47] -->
            <div class="dish-rate">
                <i class="fa-solid fa-star"></i>
                <!-- Duplique a estrela 4 vezes [48] -->
                <span>500+</span>
            </div>
            
            <!-- Preço e Botão [48] -->
            <div class="dish-price">
                <h4>R$ 20,00</h4>
                <button class="btn-defu">
                    <i class="fa-solid fa-basket-shopping"></i>
                </button>
            </div>
        </div>
        
        <!-- Duplique o .dish mais três vezes, ajustando o src da imagem [49] -->
        
    </div>
</section>
CSS do Cardápio ()
1. Crie menu.css dentro de Styles e importe-o.
2. Estilização:
/* Styles/menu.css */
#menu {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
}

#dishes {
    width: 100%;
    display: flex;
    justify-content: center;
    gap: 24px;
    margin-top: 32px;
}

.dish {
    display: flex;
    flex-direction: column;
    align-items: center;
    border-radius: 20px;
    gap: 18px;
    width: 25%; /* 4 pratos por linha [51] */
    padding: 20px;
    background-color: #fff;
    position: relative;
    overflow: hidden; /* Esconde o coração que fica fora da borda [52] */
    box-shadow: 0 0 12px 4px rgba(0, 0, 0, 0.1);
}

/* Coração / Like [52, 53] */
.dish-heart {
    position: absolute;
    right: -10px;
    top: -10px;
    background-color: #E9A209;
    width: 70px;
    height: 70px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #F9F9EA;
    font-size: 1.563rem;
    
    /* Arredondamento para formar o corte [52] */
    border-radius: 0 37.5px 0 42.5px;
}

.dish-description {
    color: #434343;
    text-align: center;
}

.dish-rate i {
    color: #E9A209; /* Cor amarela para as estrelas [54] */
}

.dish-price {
    display: flex;
    align-items: center;
    gap: 20px;
}
Responsividade do Cardápio
/* Styles/menu.css (no final) */

@media screen and (max-width: 1170px) {
    #dishes {
        flex-wrap: wrap; /* Quebra para duas colunas [55] */
    }

    .dish {
        /* Cálculo para garantir duas colunas com 12px de gap [56] */
        width: calc(50% - 12px); 
    }
}

@media screen and (max-width: 600px) {
    #menu .section-subtitle {
        text-align: center;
    }
    
    .dish {
        width: 100%; /* Uma coluna [57] */
    }
}
6. Construção da Seção Avaliações ()
HTML das Avaliações
Crie a seção testimonials abaixo da menu:
<!-- index.html (abaixo de </section id="menu">) -->
<section id="testimonials">
    <!-- Imagem do Chefe [58, 59] -->
    <!-- Arraste sua imagem chef.png para src/images/ [59] -->
    <img src="src/images/chef.png" alt="Chefe de cozinha" id="testimonial_chef">

    <div id="testimonials_content">
        <h2 class="section-title">Depoimentos</h2>
        <h3 class="section-subtitle">O que os clientes falam sobre nós</h3>

        <div id="feedbacks">
            <!-- Feedback 1 [60] -->
            <div class="feedback">
                <!-- Arraste sua imagem avatar.png para src/images/ [60] -->
                <img src="src/images/avatar.png" alt="Avatar" class="feedback-avatar">
                
                <div class="feedback-content">
                    <!-- Nome e Estrelas [61] -->
                    <p>Fulana de Tal 
                        <span>
                            <i class="fa-solid fa-star"></i>
                            <!-- Duplique a estrela 4 vezes -->
                        </span>
                    </p>
                    
                    <!-- Depoimento [61] -->
                    <p>"[Depoimento do Cliente]"</p>
                </div>
            </div>
            
            <!-- Duplique o .feedback para mais avaliações [61] -->

        </div>
        
        <!-- Botão de Ver Mais [62] -->
        <button class="btn-defu">Ver mais avaliações</button>
    </div>
</section>
CSS das Avaliações ()
1. Crie testimonials.css e importe-o.
2. Estilização:
/* Styles/testimonials.css */
#testimonials {
    min-height: calc(100vh - 91px);
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 48px;
}

#testimonial_chef {
    width: 500px;
    height: auto;
}

#testimonials_content {
    width: 50%;
}

/* Aumenta um pouco o subtítulo nesta seção [63] */
#testimonials .section-subtitle {
    font-size: 3rem;
}

#feedbacks {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-bottom: 40px;
}

.feedback {
    display: flex;
    align-items: center;
    gap: 20px;
    background-color: #fff;
    padding: 12px;
    border-radius: 12px;
    box-shadow: 0 0 12px 4px rgba(0, 0, 0, 0.1);
}

.feedback-avatar {
    width: 100px;
    height: 100px;
    border-radius: 100%; /* Transforma em círculo [64] */
    object-fit: cover;
}

/* Layout para nome e estrelas [64] */
.feedback-content p:first-child {
    display: flex;
    justify-content: space-between;
}

.feedback-content span i {
    color: #E9A209; /* Cor amarela para estrelas [65] */
}
Responsividade das Avaliações
/* Styles/testimonials.css (no final) */
@media screen and (max-width: 1170px) {
    #testimonials {
        flex-direction: column; /* Coloca um abaixo do outro [65] */
    }
    
    /* Oculta o chefe [66] */
    #testimonial_chef {
        display: none;
    }
    
    #testimonials_content {
        width: 70%;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    
    /* Ajusta tamanho da fonte dos títulos [67] */
    #testimonials .section-subtitle {
        font-size: 2.5rem; 
    }
}

@media screen and (max-width: 600px) {
    #testimonials_content {
        width: 100%; /* Ocupa a tela toda [68] */
    }
    
    .feedback {
        flex-direction: column; /* Avatar e conteúdo um abaixo do outro [69] */
        text-align: center;
    }
    
    #testimonials .section-subtitle {
        font-size: 2rem; 
    }
}
7. Construção do Footer
O footer contém o SVG da onda, o copyright e os botões de mídia social.
HTML do Footer
Crie a tag footer abaixo da tag </main>:
<!-- index.html (abaixo de </main>) -->
<footer>
    <!-- Imagem da Onda (Wave SVG) [70] -->
    <!-- Gere seu próprio wave.svg e coloque em src/images/ [71] -->
    <img src="src/images/wave.svg" alt="Wave" class="wave"> 

    <div id="footer_items">
        <span id="copyright">
            <!-- Símbolo de Copyright (&copy;) [72] -->
            &copy; 2024 [Seu Nome]
        </span>

        <!-- Botões de Mídia Social (reutilizado da Home) [72] -->
        <div class="social-media-buttons">
            <a href="[Link WhatsApp]"><i class="fa-brands fa-whatsapp"></i></a>
            <a href="[Link Instagram]"><i class="fa-brands fa-instagram"></i></a>
            <a href="[Link Facebook]"><i class="fa-brands fa-facebook"></i></a>
        </div>
    </div>
</footer>
CSS do Footer ()
1. Crie footer.css e importe-o.
2. Estilização:
/* Styles/footer.css */
footer {
    background-color: #FFE8B4; 
    padding-top: 100px; /* Espaço para a onda */
    margin-top: 50px;
}

footer .wave {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: auto;
}

#footer_items {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 8% 24px 8%; /* Padding (topo 0, lados 8%, baixo 24px) [74] */
}

#copyright {
    color: #1D1D1D;
    font-weight: 500;
}
Responsividade do Footer
/* Styles/footer.css (no final) */
@media screen and (max-width: 600px) {
    #footer_items {
        flex-direction: column; /* Um abaixo do outro [75] */
        gap: 20px;
    }
}
8. Refinamento e Otimização
Unificação de Imports CSS
Para deixar o HTML mais limpo, importe todos os arquivos CSS dentro do styles.css e remova as tags <link> dos arquivos específicos no index.html.
/* Styles/styles.css (No topo do arquivo) */
@import url('header.css');
@import url('home.css');
@import url('menu.css');
@import url('testimonials.css');
@import url('footer.css');

/* Remova todas as tags <link> (exceto a do styles.css e o CDN do Font Awesome) do seu index.html [73] */
Variáveis CSS
Crie variáveis globais em :root no styles.css para cores primárias e neutras, substituindo os códigos hexadecimais em todos os arquivos CSS.
/* Styles/styles.css (Adicione abaixo de @import) */
:root {
    /* Cores Neutras [77] */
    --color-neutral-0: #FFFFFF; /* Branco */
    --color-neutral-1: #1D1D1D; /* Escuro */

    /* Cores Primárias (Amarelos/Laranja) [77-81] */
    --color-primary-1: #F9F9EA; 
    --color-primary-2: #FFE8B4; 
    --color-primary-3: #FCB45; 
    --color-primary-4: #F8D477; 
    --color-primary-5: #E9A209; 
    --color-primary-6: #FFA500; /* Exemplo de cor mais forte */
}

/* Agora, substitua, por exemplo: background-color: #F9F9EA; por background-color: var(--color-primary-1); */
9. Animações e Interatividade
Rolagem Suave (Smooth Scroll)
Adicione a propriedade scroll-behavior: smooth à tag html no styles.css para que a rolagem entre as seções seja suave.
/* Styles/styles.css (Adicione aqui) */
html {
    scroll-behavior: smooth;
}
Ativação da Nav Bar no Scroll (jQuery)
Adicione a lógica de ativação de link de navegação enquanto o usuário rola a página:
// JavaScript/script.js (Dentro de $(document).ready())

const sections = $('section'); // Pega todas as seções [84]
const navItems = $('.nav-item'); // Pega todos os itens de navegação [84]
const header = $('header');
let activeSectionIndex = 0; // Index da seção ativa [85]

$(window).on('scroll', function() {
    // Lógica para adicionar sombra no header [85-89]
    const scrollPosition = $(window).scrollTop() - header.outerHeight();
    
    if (scrollPosition <= 0) {
        header.css('box-shadow', 'none');
    } else {
        header.css('box-shadow', '0 1px 5px rgba(0, 0, 0, 0.1)');
    }

    // Lógica para trocar a tab ativa [90]
    navItems.removeClass('active'); // Remove a classe de todos primeiro [91]

    sections.each(function(i) {
        const sectionTop = $(this).offset().top - 96; /* Descontando o header [92] */
        const sectionBottom = sectionTop + $(this).outerHeight(); [92]

        if (scrollPosition >= sectionTop && scrollPosition < sectionBottom) {
            activeSectionIndex = i;
            return false; // Sai do loop [93]
        }
    });

    // Adiciona a classe ativa no item correspondente [93]
    $(navItems[activeSectionIndex]).addClass('active');
});
Animações de Entrada (ScrollReveal)
Use a biblioteca ScrollReveal para adicionar animações suaves de entrada aos elementos.
1. Adicione o script: No index.html, adicione o script do ScrollReveal (logo abaixo do jQuery CDN).
2. No script.js: Use ScrollReveal().reveal() para animar os componentes:
// JavaScript/script.js (Fora de $(document).ready())

ScrollReveal().reveal('#cta', {
    origin: 'left',
    duration: 2000,
    distance: '20%'
});

ScrollReveal().reveal('.dish', {
    origin: 'left',
    duration: 1500,
    distance: '20%'
});

ScrollReveal().reveal('#testimonial_chef', {
    origin: 'left',
    duration: 1000,
    distance: '20%'
});

ScrollReveal().reveal('.feedback', {
    origin: 'right',
    duration: 1000,
    distance: '20%'
});

Tutorial Passo a Passo: Construindo a Landing Page Responsiva e Animada
Este tutorial visa replicar a construção da Landing Page responsiva e animada utilizando HTML, CSS, JavaScript e jQuery, conforme apresentado no vídeo. A página foi desenvolvida em componentes, focando em manutenibilidade e responsividade.
1. Configuração Inicial e Estrutura de Arquivos
Inicie o projeto organizando a estrutura de pastas e arquivos no VS Code:
1. Crie uma pasta principal (ex: Landing page).
2. Crie o arquivo principal: index.html.
3. Crie a pasta src/.
4. Dentro de src/, crie as pastas Styles/, JavaScript/ e images/.
5. Dentro de JavaScript/, crie o arquivo script.js.
6. Abra o index.html e configure a estrutura básica (usando ! + Enter). Troque a linguagem para PT-BR e o título para Landing page.
Inclusão de Bibliotecas (CDNs)
Adicione as seguintes referências no <head> do index.html:
• Font Awesome CDN: Para ícones (ex: hambúrguer, estrelas, redes sociais).
• jQuery CDN: Para manipulação facilitada do DOM.
• ScrollReveal CDN: Para as animações de entrada dos elementos.
<!-- index.html (dentro de <head>) -->
<script src="[LINK DO JQUERY CDN]"></script>
<script src="[LINK DO SCROLL REVEAL CDN]"></script>
Importe o script principal no final do <body>.
<!-- index.html (no final de <body>) -->
<script src="src/JavaScript/script.js"></script>
2. Estrutura CSS e Estilos Gerais ()
Crie o arquivo styles.css dentro de src/Styles/. Este arquivo será o estilo geral e o hub de importação para todos os outros CSS.
A. Estilos Base e Reset
Adicione a importação da fonte Poppins e o reset básico:
/* src/Styles/styles.css */
@import url('[LINK DA FONTE POPPINS]');

* {
    padding: 0;
    margin: 0;
    box-sizing: border-box; /* Essencial para responsividade [13] */
    font-family: 'Poppins', sans-serif;
}

body {
    background-color: var(--color-primary-1); /* #F9F9EA [13, 14] */
}

section {
    padding: 28px 8%; /* Padding usado em todas as seções [15, 16] */
}
B. Componentes Reutilizáveis
Defina as classes de título de seção e o botão padrão (.btn-defu) no styles.css:
/* src/Styles/styles.css */
.section-title {
    color: var(--color-primary-5); /* #E9A209 [18] */
    font-size: 1.563rem;
}

.section-subtitle {
    font-size: 2.1875rem;
}

/* Botão Padrão */
.btn-defu {
    /* Estilos do botão (display: flex, background: amarelo, box-shadow, cursor: pointer) [19, 20] */
    background-color: var(--color-primary-3); /* #FCB45 */
    border-radius: 12px;
    padding: 10px 14px;
    transition: background-color 0.3s ease;
}

.btn-defu:hover {
    background-color: var(--color-primary-4); /* #F8D477 [20] */
}

/* Botões de Mídia Social (usado na Home e Footer) */
.social-media-buttons {
    display: flex;
    gap: 18px;
    /* Estilos de cor, sombra e hover [21, 22] */
}
3. Header e Navegação
Crie o arquivo header.css dentro de src/Styles/.
A. Estrutura HTML do Header
A navegação deve incluir a logo, a lista de links para desktop (#nav_list), o botão de ação, o botão mobile (#mobile_btn) e o menu mobile (#mobile_menu).
<!-- index.html -->
<header>
    <nav id="nav_bar">
        <i class="fa-solid fa-burger" id="nav_logo">Food</i>
        <ul id="nav_list">
            <li class="nav-item active"><a href="#home">Início</a></li>
            <!-- ... outros itens (Cardápio, Avaliações) [25] -->
        </ul>
        <button class="btn-defu">Peça aqui</button>
        <button id="mobile_btn"><i class="fa-solid fa-bars"></i></button>
    </nav>
    <div id="mobile_menu">
        <!-- Lista mobile e botão (duplicados da versão desktop) [24] -->
    </div>
</header>
B. Estilos CSS do Header
Fixe o header no topo e aplique o layout flexível:
/* src/Styles/header.css */
header {
    /* Fixo no topo, cor de fundo e Z-index alto [26, 28] */
    position: sticky; 
    top: 0; 
    background-color: var(--color-primary-1);
    z-index: 3;
}

#nav_bar {
    display: flex;
    justify-content: space-between;
}

.nav-item.active a {
    /* Define o "risquinho" amarelo de qual seção está ativa [29] */
    color: var(--color-neutral-1);
    border-bottom: 3px solid var(--color-primary-4); 
}

#mobile_btn, #mobile_menu {
    display: none; /* Esconde a versão mobile inicialmente [30] */
}
C. Responsividade do Header
Use a media query para ocultar os elementos desktop e exibir o botão mobile:
/* src/Styles/header.css (Media Query) */
@media screen and (max-width: 1170px) {
    #nav_list, #nav_bar .btn-defu {
        display: none;
    }
    
    #mobile_btn {
        display: block;
    }

    #mobile_menu.active {
        display: flex; /* Exibir o menu mobile quando a classe 'active' é adicionada [11] */
        flex-direction: column;
        align-items: center;
    }
    /* ... estilos para #mobile_nav_list [32] */
}
4. Interatividade e Sombra no Scroll (jQuery)
A. Lógica Mobile (script.js)
Use jQuery para alternar a classe active no menu mobile e trocar o ícone (bars para x):
// src/JavaScript/script.js
$(document).ready(function() {
    $('#mobile_btn').on('click', function() {
        $('#mobile_menu').toggleClass('active');
        $('#mobile_btn').find('i').toggleClass('fa-x'); /* Troca o ícone [33] */
    });
});
B. Sombra e Link Ativo no Scroll
Adicione lógica para calcular a posição do scroll e aplicar a sombra no header e alternar a classe active nos links:
// src/JavaScript/script.js (Dentro do $(document).ready())

$(window).on('scroll', function() {
    const scrollPosition = $(window).scrollTop() - $('header').outerHeight();

    // 1. Sombra no Header
    if (scrollPosition <= 0) {
        $('header').css('box-shadow', 'none');
    } else {
        $('header').css('box-shadow', '0 1px 5px rgba(0, 0, 0, 0.1)'); /* Sombra adicionada [35, 37] */
    }

    // 2. Transição de Links (Iteração sobre as seções) [38]
    $('.nav-item').removeClass('active'); 

    $('section').each(function(i) {
        const sectionTop = $(this).offset().top - 96; /* Desconta altura do header [39] */
        // ... (Lógica para determinar a seção ativa e adicionar a classe 'active') [36]
    });
});
5. Seção Home ()
Crie home.css dentro de src/Styles/.
A. Estrutura HTML da Home
Crie a seção #home com a chamada à ação (#cta), os botões, os ícones de redes sociais e o banner (#banner) com a imagem e a forma geométrica (.shape).
<!-- index.html -->
<main id="content">
    <section id="home">
        <div class="shape"></div> <!-- Forma geométrica [40] -->
        <div id="cta">
            <h1 id="cta_title">O Sabor vai até <span style="color: var(--color-primary-5);">você</span></h1>
            <!-- ... descrição, botões e social media [42, 43] -->
        </div>
        <div id="banner">
            <img src="src/images/hero.png" alt="Prato principal">
        </div>
    </section>
</main>
B. Estilos CSS da Home
Defina o layout flexível e posicione os elementos.
/* src/Styles/home.css */
#home {
    display: flex;
    min-height: calc(100vh - 91px); /* Altura mínima descontando o header [15] */
    position: relative; /* Para que .shape seja absoluto em relação à home [45] */
}

#cta {
    width: 35%; /* Largura menor para o CTA [44] */
}

/* Forma Geométrica */
.shape {
    background-color: var(--color-primary-2); /* #FFE8B4 [46] */
    width: 50%;
    height: 100%;
    position: absolute;
    top: 0;
    right: 0;
    z-index: 1; 
    border-radius: 40% 30% 0% 20%; /* Criação da forma de onda [45] */
}

#banner {
    width: 70%;
    z-index: 2; /* Fica acima do shape [47] */
}
C. Responsividade da Home
Em telas menores, oculte o banner e a forma geométrica, e centralize o CTA:
/* src/Styles/home.css (Media Query) */
@media screen and (max-width: 1170px) {
    #home {
        flex-direction: column;
    }
    
    #banner, .shape {
        display: none; /* Remove a imagem e o shape [48] */
    }

    #cta {
        width: 100%;
        align-items: center;
        text-align: center;
    }
}
6. Seção Cardápio ()
Crie menu.css dentro de src/Styles/.
A. Estrutura HTML do Cardápio
Inclua o título, subtítulo e a div #dishes que contém múltiplos elementos .dish. Cada prato tem o coração (.dish-heart), imagem, título, descrição, avaliação (.dish-rate) e preço (.dish-price).
B. Estilos CSS do Cardápio
Use display flex para alinhar os pratos em uma grade.
/* src/Styles/menu.css */
#dishes {
    width: 100%;
    display: flex;
    justify-content: center;
    gap: 24px;
}

.dish {
    width: 25%; /* 4 pratos por linha [53] */
    position: relative;
    overflow: hidden; /* Esconde o coração [54] */
    /* ... border-radius, background, box-shadow [53] */
}

.dish-heart {
    position: absolute;
    right: -10px;
    top: -10px;
    /* Estilos para formar o "corte" arredondado [54, 55] */
    background-color: var(--color-primary-5);
}
C. Responsividade do Cardápio
Ajuste o layout para duas colunas e depois para uma coluna:
/* src/Styles/menu.css (Media Query) */
@media screen and (max-width: 1170px) {
    #dishes {
        flex-wrap: wrap; /* Permite a quebra dos itens [56] */
    }

    .dish {
        /* Cálculo para garantir que cabem dois pratos [57] */
        width: calc(50% - 12px); 
    }
}

@media screen and (max-width: 600px) {
    .dish {
        width: 100%; /* Uma coluna [58] */
    }
}
7. Seção Avaliações ()
Crie testimonials.css dentro de src/Styles/.
A. Estrutura HTML das Avaliações
A seção deve conter a imagem do chefe (#testimonial_chef) e o conteúdo (#testimonials_content), incluindo os títulos e a div #feedbacks.
<!-- index.html -->
<section id="testimonials">
    <img src="src/images/chef.png" id="testimonial_chef">
    <div id="testimonials_content">
        <!-- Títulos [61] -->
        <div id="feedbacks">
            <div class="feedback">
                <img src="src/images/avatar.png" class="feedback-avatar">
                <!-- ... conteúdo do feedback (nome, estrelas, depoimento) [62, 63] -->
            </div>
            <!-- ... outros feedbacks [63] -->
        </div>
        <button class="btn-defu">Ver mais avaliações</button>
    </div>
</section>
B. Estilos CSS das Avaliações
Use display flex para posicionar o chefe ao lado do conteúdo.
/* src/Styles/testimonials.css */
#testimonials {
    display: flex;
    gap: 48px;
}

.feedback {
    display: flex;
    background-color: var(--color-neutral-0); /* Branco [65] */
    box-shadow: 0 0 12px 4px rgba(0, 0, 0, 0.1);
}

.feedback-avatar {
    width: 100px;
    height: 100px;
    border-radius: 100%; /* Transforma em círculo [66] */
}
C. Responsividade das Avaliações
/* src/Styles/testimonials.css (Media Query) */
@media screen and (max-width: 1170px) {
    #testimonials {
        flex-direction: column;
    }
    
    #testimonial_chef {
        display: none; /* Oculta o chefe [67] */
    }
    
    #testimonials_content {
        width: 70%;
        align-items: center;
    }
}
/* ... Ajuste para mobile (width: 100% e feedback em coluna) [68, 69] */
8. Footer
Crie footer.css dentro de src/Styles/.
A. Estrutura HTML do Footer
O footer inclui a onda SVG (.wave), a informação de copyright e os botões de mídia social.
<!-- index.html (Abaixo de </main>) -->
<footer>
    <img src="src/images/wave.svg" alt="Wave" class="wave"> 
    <div id="footer_items">
        <span id="copyright">
            &copy; 2024 [Seu Nome]
        </span>
        <div class="social-media-buttons">
            <!-- Botões de mídia social [70] -->
        </div>
    </div>
</footer>
B. Estilos CSS do Footer
/* src/Styles/footer.css */
footer {
    background-color: var(--color-primary-2); /* #FFE8B4 [72] */
    padding-top: 100px; /* Espaço para a onda [68] */
}

#footer_items {
    display: flex;
    justify-content: space-between;
    /* ... padding e alinhamento [73] */
}
C. Responsividade do Footer
/* src/Styles/footer.css (Media Query) */
@media screen and (max-width: 600px) {
    #footer_items {
        flex-direction: column; /* Um abaixo do outro [74] */
        gap: 20px;
    }
}
9. Refinamento e Animações
A. Otimização de CSS
1. Variáveis CSS: Adicione todas as cores primárias e neutras usadas no projeto dentro de :root no styles.css (ex: --color-primary-1, --color-neutral-0) e substitua os códigos hexadecimais em todos os arquivos.
2. Unificação de Imports: No styles.css, importe todos os arquivos específicos (header.css, home.css, etc.) e remova os <link> individuais do index.html.
B. Animações ScrollReveal
Use a biblioteca ScrollReveal para adicionar animações de entrada aos elementos. Adicione o script do ScrollReveal ao index.html (Passo 1).
// src/JavaScript/script.js (Fora da função $(document).ready())

// Animação do CTA (Vindo da esquerda) [78]
ScrollReveal().reveal('#cta', {
    origin: 'left',
    duration: 2000,
    distance: '20%'
});

// Animação dos Pratos [79]
ScrollReveal().reveal('.dish', {
    origin: 'left',
    duration: 1500,
    distance: '20%'
});

// Animação do Chefe (Vindo da esquerda) [79]
ScrollReveal().reveal('#testimonial_chef', {
    origin: 'left',
    duration: 1000,
    distance: '20%'
});

// Animação dos Feedbacks (Vindo da direita) [79]
ScrollReveal().reveal('.feedback', {
    origin: 'right',
    duration: 1000,
    distance: '20%'
});
C. Rolagem Suave (Smooth Scroll)
Adicione a propriedade scroll-behavior: smooth ao HTML para uma navegação mais suave entre as seções.
/* src/Styles/styles.css */
html {
    scroll-behavior: smooth; /* Comportamento de scroll suave [80] */
}
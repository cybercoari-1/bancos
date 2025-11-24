# Repositório de Logos de Bancos em SVG

Olá! Este repositório foi criado para reunir logos de bancos em formato SVG com dimensões de 2500px x 2500px. É uma coleção abrangente de logos que visa facilitar o acesso a essas imagens em alta resolução e qualidade.

## Lista de Bancos Disponíveis

<script>    // Configura莽玫es    const config = {      owner: "cybercoari-1",      repo: "bancos",      branch: "main"    };        // URL base para as imagens    config.baseURL = `https://cdn.jsdelivr.net/gh/${config.owner}/${config.repo}@${config.branch}/`;    // Elementos DOM    const elements = {      gallery: document.getElementById("gallery"),      contador: document.getElementById("contador"),      contadorFiltrado: document.getElementById("contadorFiltrado"),      contadorPastas: document.getElementById("contadorPastas"),      buscaImgs: document.getElementById("buscaImgs")    };    // Estado da aplica莽茫o    let state = {      allImages: [],      filteredImages: [],      folders: {}    };    // Fun莽茫o principal para carregar imagens    async function carregarImagens() {      try {        const apiURL = `https://api.github.com/repos/${config.owner}/${config.repo}/git/trees/${config.branch}?recursive=1`;        const response = await fetch(apiURL);        if (!response.ok) {          if (response.status === 403) {            throw new Error("Limite de requisi莽玫es 脿 API do GitHub excedido. Tente novamente em alguns minutos.");          }          throw new Error(`Erro ${response.status}: ${response.statusText}`);        }        const data = await response.json();                if (!data.tree) {          throw new Error("Estrutura de dados inesperada da API do GitHub");        }                processarArquivos(data.tree);              } catch (err) {        console.error("Erro ao carregar imagens:", err);        elements.gallery.innerHTML = `          <div class="no-results">            <h3>Erro ao carregar imagens</h3>            <p>${err.message}</p>            <p>Verifique se o reposit贸rio "${config.owner}/${config.repo}" existe e est谩 acess铆vel publicamente.</p>          </div>        `;      }    }    // Processa os arquivos retornados pela API    function processarArquivos(arquivos) {      const imagens = arquivos.filter(item =>        item.type === "blob" && /\.(png|jpg|jpeg|svg|gif|webp|bmp)$/i.test(item.path)      );      // Atualiza estado      state.allImages = imagens;      state.filteredImages = [...imagens];            // Processa pastas      state.folders = {};      imagens.forEach(file => {        const pasta = file.path.includes("/") ? file.path.split("/")[0] : "Raiz";        state.folders[pasta] = (state.folders[pasta] || 0) + 1;      });      // Atualiza interface      atualizarContadores();      renderizarGaleria();      renderizarPastas();    }    // Atualiza os contadores na interface    function atualizarContadores() {      elements.contador.textContent = state.allImages.length;      elements.contadorFiltrado.textContent = state.filteredImages.length;      elements.contadorPastas.textContent = Object.keys(state.folders).length;    }    // Renderiza a galeria de imagens    function renderizarGaleria() {      if (state.filteredImages.length === 0) {        elements.gallery.innerHTML = `          <div class="no-results">            <h3>Nenhuma imagem encontrada</h3>            <p>Tente ajustar os termos da busca.</p>          </div>        `;        return;      }      elements.gallery.innerHTML = state.filteredImages.map(file => {        const url = config.baseURL + file.path;        return `          <div class="card">            <div class="image-container">              <img src="${url}" alt="${file.path}" loading="lazy">            </div>            <p class="file-path">${file.path}</p>          </div>        `;      }).join("");    }    // Renderiza as estat铆sticas de pastas    function renderizarPastas() {      // Verifica se j谩 existe o container de estat铆sticas de pastas      let folderStatsContainer = document.querySelector('.folder-stats-container');            if (!folderStatsContainer) {        // Cria o container se n茫o existir        const statsContainer = document.querySelector('.stats');        folderStatsContainer = document.createElement('div');        folderStatsContainer.className = 'stat-box folder-stats-container';        folderStatsContainer.style.flexBasis = '100%';        folderStatsContainer.style.marginTop = '20px';        folderStatsContainer.innerHTML = `          <h3>Imagens por Pasta</h3>          <div class="folder-stats"></div>        `;        statsContainer.appendChild(folderStatsContainer);      }            const folderStats = folderStatsContainer.querySelector('.folder-stats');      folderStats.innerHTML = Object.entries(state.folders)        .sort((a, b) => b[1] - a[1]) // Ordena por quantidade (decrescente)        .map(([pasta, count]) => `          <div class="folder-stat">            <span class="folder-name">${pasta}/</span>            <span class="folder-count">${count}</span>          </div>        `).join("");    }    // Filtra as imagens baseado no termo de busca    function filtrarImagens(termo) {      if (!termo) {        state.filteredImages = [...state.allImages];      } else {        const termoLower = termo.toLowerCase();        state.filteredImages = state.allImages.filter(file =>           file.path.toLowerCase().includes(termoLower)        );      }            atualizarContadores();      renderizarGaleria();    }    // Inicializa莽茫o    document.addEventListener('DOMContentLoaded', () => {      carregarImagens();            // Configura o evento de busca      elements.buscaImgs.addEventListener('input', function() {        filtrarImagens(this.value);      });    });  </script>

Aqui está a lista de bancos cujos logos estão presentes neste repositório:

1. ABC Brasil
2. Ailos
3. Arbi
4. Asaas IP S.A
5. Banco BMP
6. Banco BS2 S.A
7. Banco BTG Pactual
8. Banco C6 S.A
9. Banco da Amazônia S.A
10. Banco Daycoval
11. Banco do Brasil S.A
12. Banco do Estado do Espírito Santo
13. Banco do Estado do Pará
14. Banco do Estado do Sergipe
15. Banco do Nordeste do Brasil S.A
16. Banco Industrial do Brasil S.A
17. Banco Inter S.A
18. Banco Mercantil do Brasil
19. Banco Original S.A
20. Banco Paulista
21. Banco Pine
22. Banco Rendimento
23. Banco Safra S.A
24. Banco Santander Brasil S.A
25. Banco Sofisa
26. Banco Topazio
27. Banco Triângulo - Tribanco
28. Banco Votorantim
29. Bank of America
30. Banrisul
31. Bees Bank
32. BK Bank
33. BMG
34. BNP Paribas
35. Bradesco S.A
36. BRB - Banco de Brasília
37. Caixa Econômica Federal
38. Capitual
39. Contbank
40. Conta Simples Soluções em Pagamentos
41. Cora Sociedade Crédito Direto S.A
42. Credisis
43. Cresol
44. Duepay
45. Efí - Gerencianet
46. Grafeno
47. InfinitePay
48. Ifood Pago
49. IP4Y
50. Itaú Unibanco S.A
51. Iugu IP S.A
52. Linker
53. MagaluPay
54. Mercado Pago
55. MFUG Brasil
56. Modobank
57. Múltiplo Bank
58. Neon
59. Nu Pagamentos S.A (Nubank)
60. Omie.cash
61. Omni
62. PagSeguro Internet S.A
63. Paycash
64. PicPay
65. Pinbank
66. Quality Digital Bank
67. RecargaPay
68. Sicoob
69. Sicredi
70. Sisprime do Brasil
71. Squid Soluções Financeiras
72. Starbank
73. Stone Pagamentos S.A
74. Sulcredi
75. Transfeera
76. Unicred
77. Uniprime
78. XP Investimentos
79. Zemo Bank
80. Bancos Escuros (Subpasta com alguns bancos já mencionados)

## Contribuição

Se você deseja contribuir com este repositório, sinta-se à vontade para fazer um fork e enviar um pull request. Ao adicionar novos logos, certifique-se de que eles estejam no formato SVG e com as dimensões mencionadas.

## Licença

Estes logos são propriedade de seus respectivos bancos. Este repositório é apenas uma coleção e não possui qualquer afiliação ou endosso dos bancos mencionados. Utilize os logos de acordo com as diretrizes de marca de cada banco e respeite os direitos autorais.

## Autor

-   Jonildo Ferreira Roque
-   ``cybercoari@gmail.com``
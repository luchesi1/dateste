![GO CLARO](https://www.claro.com.br/imagem/imagem-now-1509156624243.webp)

> Área - Digital Analytics<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Embratel - Landing Page
Última atualização: 03/11/2020 <br />
Em caso de dúvidas, entrar em contato com: [claro@zoly.com.br](mailto:claro@zoly.com.br)

<br />

### **Descrição Geral**

O `snippet` do Google Tag Manager é um pequeno trecho de código javascript ou non-javascript, através do uso de um iframe quando o javascript não está disponível, que é inserido nas páginas do site, tornando possível que a configuração das tags sejam realizadas via interface.

---

### **Posicionamento do Código - Google Tag Manager**

#### 1. Copie o seguinte JavaScript e cole-o o mais próximo da tag `<head>` de abertura possível em todas as páginas do seu site.

```html

<html>
  <head>
    <!-- Google Tag Manager -->
    <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start': new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0], j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src='https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f); })(window,document,'script','dataLayer','GTM-M4SJZM');</script>
    <!-- End Google Tag Manager -->
    //...
  </head>
```

#### 2. Copie o seguinte trecho e cole-o imediatamente após a marcação `<body>` de abertura em cada página do seu site.

```html
<body>
  <!-- Google Tag Manager (noscript) -->
  <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-M4SJZM" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
  <!-- End Google Tag Manager (noscript) -->
  //...
  </body>
</html>
```

Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)


## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

> Caso o site já possua o Google Analytics instalado, será necessário a remoção do código de **todas as páginas do site**: <br />

```html

<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXXXXX-X', 'auto');
ga('send', 'pageview');
</script>

```

---

```html

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-XXXXXXX-X"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){window.dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-XXXXXXX-X');
</script>
```

<br />

## Overview e Descrições Técnicas

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer = [{
		'atributo1': 'valor1',
		'atributo2': 'valor2'
	}];
</script>
```

OU

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': 'valor1',
		'atributo2': 'valor2'
	});
</script>
```

### Atributos HTML (Data Attributes)

> São atributos customizados inseridos nos elementos HTML da página que permite a inclusão de dados adicionais.

**Instalação**
1. Elementos de link: ```<a href="..." class="minha_classe">Link</a>``` <br />
Elementos do tipo link que foram mapeados, precisam receber a classe **gtm-link-event** e os data attributes em sua estrutura.

```html
<a href="http://www.meudominio.com.br/page2"
	class="minha_classe gtm-link-event"
 	data-gtm-event-category="exemplo:valor-categoria"
  	data-gtm-event-action="exemplo:valor-acao"
  	data-gtm-event-label="exemplo:valor-rotulo">Texto do link</a>
```

2. Elementos comuns: ```<div class="minha_classe">Elemento</div>``` <br />
Todos os elementos comuns do html que não são links e que foram mapeados, precisam receber a classe **gtm-element-event** em sua estrutura.

```html
<div 	class="minha_classe gtm-element-event"
  	data-gtm-event-category="exemplo:valor-categoria"
 	data-gtm-event-action="exemplo:valor-acao"
 	data-gtm-event-label="exemplo:valor-rotulo">Texto do elemento</div>
```

<br />

## Implementação

A documentação foi descrita para algumas áreas especificas do ambiente [Embratel Cloud](https://mordomo.argos4.me/mordomo-helper/2020/landing-pages/10/436/embratel/cloud/).

## Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores;<br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais;<br />
Caso a informação solicitada não estiver disponível retornar 'nao_disponivel'.

---

#### Importante:
> Todos os links e botões citados nesta documentação devem ter em sua estrutura `html` a classe `gtm-link-event` se for um link `<a>` ou `gtm-element-event` se o elemento não for um link `<a>` conforme demonstraremos nos exemplos específicos.<br />
> Devem ter também os data-attributes `data-gtm-event-category`, `data-gtm-event-action` e `data-gtm-event-label` preenchidos conforme instruções específicas.

### Especificação de Micro-conversões:

**No clique dos botões do header.**
- **Onde:** No header em todas as páginas do site"

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:header"
	data-gtm-event-label="[[item-clicado]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:header"
	data-gtm-event-label="[[item-clicado]]"
>Botão</i>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[page-name]] | &#039;cloud&#039; e etc | Retornar o nome da página que o usúário está acessando. |
| [[item-clicado]] |  &#039;a-embratel&#039;, &#039;consultor&#039;, &#039;blog&#039;, &#039;espaco-cliente&#039;, &#039;apoio-para-navegar&#039; e &#039;recurso-de-plugin-do-vlibras&#039; | Retornar o nome do botão clicado. |

<br />

**No clique dos itens do menu superior**
- **Onde:** Nos itens do menu em todas as páginas

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:menu-superior"
	data-gtm-event-label="[[menu-clicado]]:[[sub-menu-clicado]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:menu-superior"
	data-gtm-event-label="[[menu-clicado]]:[[sub-menu-clicado]]"
>Botão</i>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[page-name]] | &#039;cloud&#039; e etc | Retornar o nome da página que o usúário está acessando. |
| [[menu-clicado]] | &#039;conectividade-e-colaboracao&#039;, &#039;mobilidade&#039;, &#039;data-center&#039;, &#039;cloud&#039;, &#039;seguranca&#039;, &#039;ti&#039;, &#039;cx&#039; e &#039;iot&#039; | Retornar o nome do menu clicado. |
| [[sub-menu-clicado]] |  &#039;voz&#039;, &#039;colaboracao&#039;, &#039;rede-de-dados&#039;, &#039;internet&#039;, &#039;servicos-via-satelite&#039;, &#039;longa-distancia&#039;, &#039;venda-multinacional&#039;, &#039;internet&#039;, &#039;m2m&#039;, &#039;plano-claro-max-2.0&#039;, &#039;total-share-2.0&#039;, &#039;smartphones-e-tablets&#039; e etc | Retornar o nome do sub-menu clicado. |

<br />

**No clique dos botões ou links apresentados na página, dentro de um card**
- **Onde:** Em toda a página"

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:[[botao-link]]"
	data-gtm-event-label="[[titulo-card]]:[[titulo-botao]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:[[botao-link]]"
	data-gtm-event-label="[[titulo-card]]:[[titulo-botao]]"
>Botão</i>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[page-name]] | &#039;cloud&#039; e etc | Retornar o nome da página que o usúário está acessando. |
| [[botao-link]] | &#039;botao&#039; ou &#039;link&#039; | Deve retornar se o usuário clicou em um botão ou link dentro do card. |
| [[titulo-card]] | &#039;claro-drive-negocio&#039;, &#039;site-pronto&#039;, &#039;hospedagem-de-sites&#039;, &#039;microsoft-365-apps-for-enterprise&#039; e etc | Retornar o título do card pertencente ao botão clicado. |
| [[titulo-botao]] | &#039;contrate-agora&#039;, &#039;saiba-mais&#039;, &#039;construa-hoje&#039;, &#039;solicite-agora&#039;, &#039;pesquise-seu-dominio&#039;, &#039;falar-com-um-consultor&#039;, &#039;conheca-a-microsoft-365&#039; e &#039;conheca-a-claro-drive&#039; | Retornar o nome do botao clicado. |

<br />

**No clique dos botões ou links apresentados na página em uma seção fora de um card**
- **Onde:** Em toda a página

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:[[botao-link]]"
	data-gtm-event-label="[[titulo-secao]]:[[titulo-botao]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:[[botao-link]]"
	data-gtm-event-label="[[titulo-secao]]:[[titulo-botao]]"
>Botão</i>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[page-name]] | &#039;cloud&#039; e etc | Retornar o nome da página que o usúário está acessando. |
| [[botao-link]] | &#039;botao&#039; ou &#039;link&#039; | Deve retornar se o usuário clicou em um botão ou link dentro do card. |
| [[titulo-secao]] | &#039;servicos-online&#039;, &#039;microsoft-365&#039;, &#039;claro-drive&#039;, &#039;espaco-cliente&#039; e etc | Retorna o título da seção do item clicado |
| [[titulo-botao]] | &#039;conheca-o-microsoft-365&#039;, &#039;conheca-a-claro-drive&#039;, &#039;acessar&#039; e etc | Retornar o nome do botao clicado |

<br />

**No clique dos itens do "Mapa do site"**
- **Onde:** No Mapa do site no rodapé da página ( quando exibido )

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:mapa-do-site"
	data-gtm-event-label="[[item-clicado]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:mapa-do-site"
	data-gtm-event-label="[[item-clicado]]"
>Botão</i>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[page-name]] | &#039;cloud&#039; e etc | Retornar o nome da página que o usúário está acessando. |
| [[item-clicado]] | &#039;conectividade-e-colaboracao&#039;, &#039;mobilidade&#039;, &#039;data-center&#039;, &#039;cloud&#039;, &#039;seguranca&#039;, &#039;ti&#039;, &#039;cx&#039;, &#039;iot&#039;, &#039;voz&#039;, &#039;colaboracao&#039;, &#039;rede-de-dados&#039;, &#039;internet&#039;, &#039;servicos-via-satelite&#039;, &#039;longa-distancia&#039;, &#039;venda-multinacional&#039;, &#039;internet&#039;, &#039;m2m&#039;, &#039;plano-claro-max-2.0&#039;, &#039;total-share-2.0&#039;, &#039;smartphones-e-tablets&#039;, &#039;servico-movel-maritimo&#039;, &#039;infraestrutura&#039;, &#039;hosting&#039;, &#039;servicos-gerenciados&#039;, &#039;claro-drive-negocio&#039;, &#039;cloud-backup&#039;, &#039;cloud-server&#039;, &#039;cloud-video-delivery&#039; e etc | Retornar o título do item clicado |

<br />

**Ao selecionar uma opção em um 'select' na página.**
- **Onde:** Em toda a página

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'embratel:landing-page:[[page-name]]',
    'eventAction': 'selecinou:[[titulo]]',
    'eventLabel': '[[item-selecionado]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[page-name]] | &#039;cloud&#039; e etc | Retornar o nome da página que o usúário está acessando. |
| [[titulo]] | &#039;data&#039;, &#039;mes&#039;, &#039;ano&#039;, &#039;estado&#039; e etc | Deve retornar o título do seletor que o usuário interagiu |
| [[item-selecionado]] | &#039;20&#039;, &#039;1996&#039;, &#039;sp&#039;, &#039;sao-paulo&#039; e etc | Deve retornar o item selecionado pelo usuário |

<br />

**Ao preencher o campo de um formulário.**
- **Onde:** Em toda a página

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'embratel:landing-page:[[page-name]]',
    'eventAction': 'interacao:campo',
    'eventLabel': '[[titulo-secao]]:[[item-preenchido]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[page-name]] | &#039;cloud&#039; e etc | Retornar o nome da página que o usúário está acessando. |
| [[titulo-secao]] | &#039;dados-pessoais&#039;, &#039;endereco&#039;, &#039;pagamento&#039; e etc | Retorna o título da seção do item clicado. |
| [[item-preenchido]] | &#039;nome&#039;, &#039;endereco&#039;, &#039;email&#039;, &#039;cpf&#039;, &#039;telefone&#039; e etc | Retorna o título ou referencia ao item preenchido pelo usuário. |

<br />

**No clique dos ícones de rede social.**
- **Onde:** No rodapé da página

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:redes-sociais"
	data-gtm-event-label="[[icone-clicado]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	data-gtm-event-category="embratel:landing-page:[[page-name]]"
	data-gtm-event-action="clique:redes-sociais"
	data-gtm-event-label="[[icone-clicado]]"
>Botão</i>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[page-name]] | &#039;cloud&#039; e etc | Retornar o nome da página que o usúário está acessando. |
| [[icone-clicado]] | &#039;facebook&#039;, &#039;twitter&#039;, &#039;youtube&#039;, &#039;linkedin&#039; e &#039;instagram&#039; | Retornar o nome do ícone de rede social clicada. |

<br />

## Considerações Finais:

> Em caso de dúvidas, entrar em contato com: [claro@zoly.com.br](mailto:claro@zoly.com.br)

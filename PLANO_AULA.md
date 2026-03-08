# PLANO DE AULA — VR para Medicina com A-Frame

## Informação geral

| Item | Detalhe |
|------|---------|
| Duração | 3 horas (com pausa) |
| Público | Estudantes de Medicina, sem experiência de programação |
| Resultado | Uma cena VR interativa, testada no PC e nos óculos Meta Quest |
| Ficheiro | Um único `index.html` construído do zero, passo a passo |

---

## ANTES DA AULA — Setup (formador prepara)

1. Cada PC deve ter o **VS Code** instalado + extensão **Live Server**
2. Copiar a pasta do projeto para cada PC (com a imagem panorâmica e a pasta `assets/heart/`)
3. Confirmar que há Wi-Fi partilhado entre PCs e os Quest
4. Ter o resultado final aberto no seu PC para demonstração

---

# PASSO 1 — O que é HTML? O esqueleto da página (15 min)

## O que o formador diz

> "Antes de fazer VR, precisamos de entender o básico: o que é uma página web."
>
> "Toda a página web é escrita numa linguagem chamada **HTML** — HyperText Markup Language. Não é programação, é mais como dar instruções de formatação. Pensem nisto como preencher um formulário: há campos com nomes, e nós preenchemos o conteúdo."
>
> "Em HTML, tudo funciona com **tags**. Uma tag é uma palavra entre `< >`. A maioria das tags tem uma de abertura e uma de fecho:"
>
> ```
> <title>Olá</title>
>          ↑ conteúdo entre a tag de abertura e a de fecho
> ```
>
> "Vamos criar o nosso ficheiro. No VS Code: File → New File → guardar como `index.html` na pasta do projeto."

## O que os alunos escrevem

```html
<!DOCTYPE html>
<html lang="pt">
  <head>
    <meta charset="utf-8" />
    <title>Aula VR - Medicina</title>
  </head>
  <body>
    <h1>Olá Mundo VR!</h1>
  </body>
</html>
```

## Explicação linha a linha

| Linha | Código | O que faz |
|-------|--------|-----------|
| 1 | `<!DOCTYPE html>` | Diz ao browser: "este ficheiro é HTML moderno". Obrigatório, sempre na 1ª linha. |
| 2 | `<html lang="pt">` | Abre o documento HTML. `lang="pt"` diz que a língua é português. |
| 3 | `<head>` | Abre a secção "cabeça" — informações sobre a página (não visíveis no ecrã). |
| 4 | `<meta charset="utf-8" />` | Define a codificação de caracteres. Sem isto, acentos (ã, é, ç) podem ficar estranhos. |
| 5 | `<title>Aula VR - Medicina</title>` | O título que aparece no separador do browser. |
| 6 | `</head>` | Fecha a secção "cabeça". |
| 7 | `<body>` | Abre o "corpo" — tudo o que é visível na página. |
| 8 | `<h1>Olá Mundo VR!</h1>` | Um título grande (heading 1). É o nosso teste — se isto aparece, o ficheiro funciona. |
| 9 | `</body>` | Fecha o corpo. |
| 10 | `</html>` | Fecha o documento. |

> **Conceito-chave:** HTML funciona como caixas dentro de caixas. O `<html>` contém o `<head>` e o `<body>`. Cada tag que se abre tem de se fechar.

## Guardar e ver o resultado

1. Guardar: **Ctrl+S**
2. Clicar direito no `index.html` → **"Open with Live Server"**
3. O browser abre e mostra: **"Olá Mundo VR!"**

## Checkpoint ✓

- [ ] O browser mostra o texto "Olá Mundo VR!"
- [ ] O URL começa por `http://127.0.0.1:5500` (e NÃO por `file://`)

---

# PASSO 2 — Entrar no mundo 3D: A-Frame e a primeira forma (15 min)

## O que o formador diz

> "Agora vamos transformar esta página 2D num mundo 3D. Para isso usamos uma **biblioteca** chamada A-Frame."
>
> "O que é uma **biblioteca**? É código que outra pessoa já escreveu e que nós reutilizamos. Em vez de programar um motor 3D do zero, carregamos o A-Frame com uma linha e ele faz o trabalho pesado."
>
> "Com A-Frame, em vez de escrever `<h1>` para títulos, escrevemos `<a-box>` para cubos, `<a-sphere>` para esferas, etc. É HTML, mas para 3D."

## O que os alunos escrevem

Substituir **TODO** o conteúdo do ficheiro por:

```html
<!DOCTYPE html>
<html lang="pt">
  <head>
    <meta charset="utf-8" />
    <title>Aula VR - Medicina</title>
    <!-- Carregar a biblioteca A-Frame (motor 3D) -->
    <script src="https://aframe.io/releases/1.7.0/aframe.min.js"></script>
  </head>
  <body>
    <!-- a-scene: o "palco" 3D onde tudo acontece -->
    <a-scene>

      <!-- O nosso primeiro objeto 3D: um cubo! -->
      <a-box position="0 1 -4" color="#4CC3D9"></a-box>

    </a-scene>
  </body>
</html>
```

## Explicação das linhas novas

| Linha | Código | O que faz |
|-------|--------|-----------|
| 7 | `<script src="https://aframe.io/...">` | Carrega o A-Frame da internet. É como ligar o motor 3D. Sem esta linha, as tags `<a-box>` etc. não funcionam. |
| — | `<!-- texto -->` | **Comentário**: texto que o browser ignora. Serve para nós, humanos, sabermos o que cada parte faz. |
| 11 | `<a-scene>` | O "palco" 3D. Tudo o que está dentro de `<a-scene>` vive no mundo 3D. |
| 14 | `<a-box position="0 1 -4" color="#4CC3D9">` | Um cubo. `position="0 1 -4"` significa: X=0 (centro), Y=1 (1 metro acima do chão), Z=-4 (4 metros à frente). A cor é um código hexadecimal (azul claro). |

> **Conceito-chave — Coordenadas 3D:**
> - **X** = esquerda (-) / direita (+)
> - **Y** = baixo (-) / cima (+)
> - **Z** = à frente (-) / atrás (+) ← o Z negativo é "para a frente"!
>
> É como uma sala: estamos na porta (Z=0), os objetos estão lá dentro (Z negativo).

> **Conceito-chave — Atributos:**
> `position`, `color`, etc. chamam-se **atributos**. São propriedades da tag, escritas dentro da tag de abertura. Formato: `nome="valor"`.

## Guardar e ver

- Ctrl+S → o browser atualiza automaticamente
- Devem ver um **cubo azul** a flutuar num fundo cinzento

## Checkpoint ✓

- [ ] Aparece um cubo azul no ecrã
- [ ] Conseguem arrastar o rato para olhar à volta (o A-Frame já ativa os controlos)

## Erros comuns

| Problema | Causa / Solução |
|----------|----------------|
| Ecrã todo preto | A-Frame não carregou. Verificar internet e o URL do script. |
| O cubo não aparece | Pode estar "atrás" da câmara. Confirmar `position="0 1 -4"` (Z negativo = à frente). |

---

# PASSO 3 — O céu panorâmico e o sistema de assets (15 min)

## O que o formador diz

> "Um mundo VR sem céu parece um estúdio vazio. Vamos adicionar uma imagem panorâmica 360° como fundo. É como estar dentro de uma esfera gigante com uma foto colada por dentro."
>
> "Para carregar ficheiros pesados (imagens, modelos 3D), A-Frame usa um sistema de **assets** — um 'armazém' que pré-carrega tudo antes de mostrar a cena. Assim não há coisas a aparecer aos bocadinhos."

## O que os alunos escrevem

Adicionar dentro de `<a-scene>`, **ANTES** do `<a-box>`:

```html
      <!-- ASSETS: armazém de ficheiros (carregam antes da cena aparecer) -->
      <a-assets>
        <img
          id="pano"
          src="2019_07_05_Armazones_Inside_Crater_Pano_24mm_EQ_CC.jpg"
          crossorigin="anonymous"
        />
      </a-assets>

      <!-- SKY: esfera gigante com a imagem panorâmica por dentro -->
      <a-sky src="#pano" rotation="0 -90 0"></a-sky>
```

## Explicação

| Código | O que faz |
|--------|-----------|
| `<a-assets>` | Abre o "armazém". Tudo aqui dentro é pré-carregado. |
| `<img id="pano" src="..." />` | Carrega a imagem panorâmica. O `id="pano"` é um nome que damos para a usar mais tarde. O `src` é o caminho do ficheiro. |
| `crossorigin="anonymous"` | Permissão técnica necessária para imagens carregadas pelo A-Frame. Sem isto, pode dar erro. |
| `</a-assets>` | Fecha o armazém. |
| `<a-sky src="#pano">` | Cria uma esfera gigante à volta de tudo. O `src="#pano"` diz "usa a imagem com id pano". O `#` antes do nome é obrigatório — é assim que se referencia um asset. |
| `rotation="0 -90 0"` | Roda o céu -90° no eixo Y para ajustar a orientação da imagem. |

> **Conceito-chave — id e referência com #:**
> Quando damos `id="pano"` a uma coisa, podemos usar `#pano` noutro sítio para dizer "aquela coisa". É como um nome próprio — único no documento.

## Guardar e ver

- Ctrl+S → agora o fundo é a imagem panorâmica!
- O cubo continua lá, mas agora com um cenário à volta

## Checkpoint ✓

- [ ] O fundo é uma imagem panorâmica (paisagem 360°)
- [ ] O cubo azul continua visível

## Erros comuns

| Problema | Solução |
|----------|---------|
| Fundo cinzento (sem imagem) | Verificar que o ficheiro `.jpg` está na mesma pasta que o `index.html`. O nome tem de ser exatamente igual (maiúsculas/minúsculas contam). |
| Demora muito a carregar | A imagem é grande. Esperar 5-10 segundos. |

---

# PASSO 4 — Luz, chão e mais formas (15 min)

## O que o formador diz

> "Reparem que o cubo tem sempre a mesma cor em todos os lados — parece plano. Isso é porque não temos luzes na cena. Sem luz, o A-Frame mostra tudo com iluminação 'flat'."
>
> "Vamos adicionar luzes, um chão, e mais formas para preencher o mundo."

## O que os alunos escrevem

Adicionar **DEPOIS** do `<a-sky>` e **ANTES** do `<a-box>`:

```html
      <!-- LUZ: sem luz, os objetos ficam "planos" e sem sombra -->
      <a-entity light="type: ambient; intensity: 0.7"></a-entity>
      <a-entity light="type: directional; intensity: 1.1" position="2 4 1"></a-entity>
      <a-entity light="type: directional; intensity: 0.5" position="-2 2 -1"></a-entity>

      <!-- CHÃO: um plano grande e verde -->
      <a-plane
        position="0 0 0"
        rotation="-90 0 0"
        width="20"
        height="20"
        color="#7BC8A4"
      ></a-plane>
```

E **substituir** o `<a-box>` que já existe por estes 3 objetos:

```html
      <!-- CUBO — à esquerda -->
      <a-box
        position="-2.5 0.7 -4"
        rotation="0 30 0"
        width="1.2"
        height="1.2"
        depth="1.2"
        color="#4CC3D9"
      ></a-box>

      <!-- ESFERA — ao centro, atrás -->
      <a-sphere
        position="0 1.5 -6"
        radius="1.25"
        color="#EF2D5E"
      ></a-sphere>

      <!-- CILINDRO — à direita -->
      <a-cylinder
        position="2.5 1 -4"
        radius="0.5"
        height="2"
        color="#FFC65D"
      ></a-cylinder>
```

## Explicação das linhas novas

| Código | O que faz |
|--------|-----------|
| `<a-entity light="type: ambient; ...">` | **Luz ambiente** — ilumina tudo por igual, como um dia nublado. `intensity: 0.7` = 70% de força. |
| `light="type: directional; ..."` | **Luz direcional** — como o sol, vem de uma direção. Cria sombras e profundidade. Temos duas para iluminar de ângulos diferentes. |
| `<a-entity>` | Tag genérica do A-Frame. Sozinha não mostra nada. Usamos com atributos (como `light=`) para criar coisas especiais. |
| `<a-plane>` | Um plano retangular. Com `rotation="-90 0 0"` fica horizontal (deitado), servindo de chão. `width` e `height` = tamanho em metros. |
| `width`, `height`, `depth` | Dimensões do cubo em metros. |
| `radius="1.25"` | Raio da esfera (1.25 m = diâmetro de 2.5 m). |
| `radius="0.5" height="2"` | Cilindro: raio 0.5 m, altura 2 m. |

> **Conceito-chave — Posições:**
> Pensem na cena como uma sala. O chão está em Y=0. Se um objeto tem `position="0 1 -4"`, está a 1 metro acima do chão e a 4 metros à frente. Valores de X negativos = esquerda, positivos = direita.

## Guardar e ver

- Ctrl+S → agora veem 3 formas num chão verde com iluminação realista

## Checkpoint ✓

- [ ] Chão verde visível
- [ ] 3 objetos: cubo azul (esquerda), esfera rosa (centro/atrás), cilindro amarelo (direita)
- [ ] Os objetos têm sombra/profundidade (não são completamente "flat")

---

# PASSO 5 — O coração 3D com rotação (15 min)

## O que o formador diz

> "Agora vamos colocar um modelo 3D de um coração humano. Não é uma forma simples como uma esfera — é um modelo feito num programa de 3D, guardado em dois ficheiros:"
>
> - **`.obj`** — a forma (geometria, como os triângulos do modelo)
> - **`.mtl`** — os materiais (cores e texturas aplicadas à forma)
>
> "Também vamos adicionar a nossa primeira **animação**: o coração vai rodar continuamente."

## O que os alunos escrevem

**1)** Dentro de `<a-assets>`, adicionar estas 2 linhas **DEPOIS** do `</img>`:

```html
        <a-asset-item id="heart-obj" src="assets/heart/HumanHeart_OBJ.obj"></a-asset-item>
        <a-asset-item id="heart-mtl" src="assets/heart/HumanHeart_OBJ.mtl"></a-asset-item>
```

**2)** Depois do `<a-cylinder>`, adicionar o coração:

```html
      <!-- CORAÇÃO 3D — modelo importado com rotação contínua -->
      <a-entity
        id="heart"
        obj-model="obj: #heart-obj; mtl: #heart-mtl"
        material="side: double"
        position="0 1.5 -3"
        rotation="0 180 0"
        scale="0.12 0.12 0.12"
        animation="property: rotation; to: 0 540 0;
                   loop: true; dur: 12000; easing: linear"
      ></a-entity>
```

## Explicação

| Código | O que faz |
|--------|-----------|
| `<a-asset-item id="heart-obj" src="...">` | Pré-carrega o ficheiro .obj do coração. `id="heart-obj"` para referenciar depois. |
| `obj-model="obj: #heart-obj; mtl: #heart-mtl"` | Diz ao A-Frame: "monta este modelo usando a geometria `#heart-obj` e os materiais `#heart-mtl`." |
| `material="side: double"` | Renderiza ambos os lados das faces do modelo. Sem isto, partes do coração podem ficar invisíveis. |
| `position="0 1.5 -3"` | Centro (X=0), a 1.5 m de altura, 3 metros à frente — na frente das outras formas. |
| `scale="0.12 0.12 0.12"` | O modelo original é enorme. Escalamos para 12% do tamanho (em X, Y e Z). |
| `rotation="0 180 0"` | Roda 180° no eixo Y para ficar virado para nós. |
| `animation="property: rotation; to: 0 540 0; ..."` | **Animação declarativa**: roda no eixo Y até 540° (uma volta e meia), repete infinitamente (`loop: true`), demora 12 segundos (`dur: 12000`), velocidade constante (`easing: linear`). |

> **Conceito-chave — Animação em A-Frame:**
> Não precisamos de código/JavaScript. Basta escrever `animation="..."` como atributo. O A-Frame anima automaticamente qualquer propriedade (posição, rotação, escala, cor...).

## Guardar e ver

- Ctrl+S → o coração 3D aparece à frente das formas, a rodar lentamente

## Checkpoint ✓

- [ ] O coração 3D é visível e tem texturas (não é todo branco/cinzento)
- [ ] O coração roda continuamente de forma suave

## Erros comuns

| Problema | Solução |
|----------|---------|
| Coração não aparece | Abrir a consola (F12 → Console). Se há erro 404, o caminho do ficheiro está errado. Confirmar que a pasta `assets/heart/` existe e os ficheiros lá dentro têm o nome exato. |
| Coração aparece gigante | Verificar `scale="0.12 0.12 0.12"`. Sem scale, o modelo pode ser enorme. |
| Coração aparece sem cor (cinzento) | O ficheiro .mtl refere texturas .png que têm de estar na mesma pasta. Confirmar que existem. |

---

# ☕ PAUSA — 15 minutos (1h15 – 1h30)

> "Boa pausa. Quando voltarem, vamos fazer a parte mais fixe: interações. Apontar para um objeto e ver coisas a acontecer."

---

# PASSO 6 — Câmara e retículo: os nossos olhos e ponteiro (10 min)

## O que o formador diz

> "Até agora, o A-Frame cria automaticamente uma câmara invisível. Mas nós precisamos de controlar onde ela está e, mais importante, precisamos de um **retículo** — aquele circulinho no centro do ecrã que funciona como ponteiro."
>
> "Em VR, não temos rato. O retículo serve para 'apontar' olhando. Olhamos para um objeto + esperamos = click."
>
> "Também precisamos que funcione o **movimento nos óculos VR**. No PC usamos WASD, mas em VR usamos o **thumbstick** (joystick) dos controladores. Para isso, vamos carregar outra biblioteca: **aframe-extras**, que trata de tudo automaticamente."
>
> "Em vez de uma câmara simples, usamos um padrão chamado **camera rig** — uma entidade-pai que se move, com a câmara dentro. Pensem como um carro: o carro (rig) move-se, e nós (câmara) estamos sentados lá dentro a olhar à volta."

## O que os alunos escrevem

**1)** No `<head>`, adicionar esta linha **DEPOIS** do script do A-Frame:

```html
    <!-- Extras: movimento com thumbstick dos controladores VR -->
    <script src="https://cdn.jsdelivr.net/gh/c-frame/aframe-extras@7.6.0/dist/aframe-extras.min.js"></script>
```

**2)** Adicionar **ANTES** de `</a-scene>` (última coisa dentro da cena):

```html
      <!-- RIG: entidade-pai que se move (WASD no PC, thumbstick em VR) -->
      <a-entity id="rig" movement-controls="fly: false" position="0 0 5">
        <!-- CÂMARA: os nossos "olhos" no mundo 3D -->
        <a-entity camera look-controls position="0 1.6 0">
          <!-- RETÍCULO: o círculo/ponteiro no centro do ecrã -->
          <a-entity
            cursor="fuse: true; fuseTimeout: 1500"
            raycaster="objects: .clickable"
            position="0 0 -1"
            geometry="primitive: ring; radiusInner: 0.01; radiusOuter: 0.02"
            material="color: #FFFFFF; shader: flat; transparent: true; opacity: 0.8"
          ></a-entity>
        </a-entity>
      </a-entity>
```

## Explicação

| Código | O que faz |
|--------|-----------|
| `<script src="...aframe-extras...">` | Carrega a biblioteca **aframe-extras** que inclui o componente `movement-controls`. Sem isto, o thumbstick dos controladores VR não funciona. |
| `<a-entity id="rig" movement-controls="fly: false">` | O **rig** (plataforma): entidade-pai que trata do movimento. `fly: false` impede voar — ficamos sempre no chão. No PC usa WASD, em VR usa o thumbstick automaticamente. |
| `position="0 0 5"` | Posição inicial do rig: 5 metros "atrás" (Z=5) para ver os objetos à frente. |
| `<a-entity camera look-controls position="0 1.6 0">` | A câmara dentro do rig. `position="0 1.6 0"` = altura dos olhos (1.6 m acima do rig). |
| `look-controls` | Permite olhar à volta arrastando o rato (PC) ou mexendo a cabeça (VR). |
| `cursor="fuse: true; fuseTimeout: 1500"` | **fuse = fusível/temporizador.** Em VR sem rato, se ficarmos a olhar para um objeto durante 1500 ms (1.5 segundos), conta como um "click". Em PC, podemos clicar normalmente com o rato. |
| `raycaster="objects: .clickable"` | O raycaster é um **raio invisível** que sai do retículo em linha reta. Só detecta objetos que tenham `class="clickable"`. Isto é um filtro — evita clicar no chão ou no céu por acidente. |
| `position="0 0 -1"` | Posição do retículo: à frente da câmara (Z=-1 = 1 metro à frente dos olhos). |
| `geometry="primitive: ring; ..."` | A forma visual do retículo: um anel (ring). `radiusInner` = buraco interior, `radiusOuter` = tamanho exterior. |
| `material="color: #FFFFFF; shader: flat; ..."` | Branco, sem iluminação (`shader: flat`), semi-transparente (`opacity: 0.8`). |

> **Conceito-chave — Camera Rig (plataforma):**
> O retículo está dentro da **câmara**, que está dentro do **rig**. Quando o rig se move (WASD ou thumbstick), a câmara e o retículo movem-se juntos — como andar dentro de um carro. Quando rodamos a cabeça, só a câmara roda (olhamos à volta dentro do carro).

> **Conceito-chave — class="clickable":**
> O `raycaster` só vê objetos com `class="clickable"`. Nos próximos passos vamos adicionar esta classe aos objetos que queremos interativos.

## Guardar e ver

- Ctrl+S → aparece um pequeno **círculo branco** no centro do ecrã
- O círculo acompanha o movimento da câmara

## Checkpoint ✓

- [ ] Círculo branco visível no centro do ecrã
- [ ] O círculo move-se quando arrastam o rato (acompanha a câmara)

---

# PASSO 7 — Interações com event-set: hover e click (20 min)

## O que o formador diz

> "Este é o passo mais importante. Vamos fazer os objetos reagir quando apontamos ou clicamos."
>
> "Para isso, usamos um extra chamado **event-set** — é um componente que funciona assim:"
>
> ```
> event-set__NOME="_event: QUANDO; PROPRIEDADE: VALOR"
> ```
>
> "Tradução: 'Quando acontecer ESTE evento, muda ESTA propriedade para ESTE valor.'"
>
> "Exemplos de eventos:"
> - `mouseenter` = o retículo **entra** no objeto (hover)
> - `mouseleave` = o retículo **sai** do objeto
> - `click` = click do rato ou fuse completo
>
> "Primeiro, precisamos de carregar a biblioteca event-set."

## O que os alunos escrevem

**1)** No `<head>`, adicionar esta linha **DEPOIS** do script do A-Frame:

```html
    <!-- Event-Set: interações (hover, click) sem JavaScript -->
    <script src="https://unpkg.com/aframe-event-set-component@5.0.0/dist/aframe-event-set-component.min.js"></script>
```

**2)** Agora vamos modificar os 3 objetos. Substituir o `<a-box>` existente por:

```html
      <!-- CUBO: hover muda a SUA cor, click muda a cor da ESFERA -->
      <a-box
        class="clickable"
        position="-2.5 0.7 -4"
        rotation="0 30 0"
        width="1.2" height="1.2" depth="1.2"
        color="#4CC3D9"
        event-set__enter="_event: mouseenter; material.color: #00FFFF"
        event-set__leave="_event: mouseleave; material.color: #4CC3D9"
        event-set__click="_event: click; _target: #esfera; material.color: #9B59B6"
      ></a-box>
```

**3)** Substituir o `<a-sphere>` existente por:

```html
      <!-- ESFERA: hover muda cor, click mostra o texto flutuante -->
      <a-sphere
        id="esfera"
        class="clickable"
        position="0 1.5 -6"
        radius="1.25"
        color="#EF2D5E"
        event-set__enter="_event: mouseenter; material.color: #FF5588"
        event-set__leave="_event: mouseleave; material.color: #EF2D5E"
        event-set__show="_event: click; _target: #info-text; visible: true"
      ></a-sphere>
```

**4)** Adicionar este **texto flutuante** logo DEPOIS da esfera:

```html
      <!-- TEXTO FLUTUANTE — escondido, aparece ao clicar na esfera -->
      <a-entity
        id="info-text"
        class="clickable"
        position="0 3.5 -6"
        visible="false"
        geometry="primitive: plane; width: 4.5; height: 0.8"
        material="color: #000000; opacity: 0.6; shader: flat"
        text="value: Bem-vindos a VR Medicina!; align: center;
              color: #FFFFFF; width: 5"
        event-set__hide="_event: click; visible: false"
      ></a-entity>
```

**5)** Substituir o `<a-cylinder>` existente por:

```html
      <!-- CILINDRO: hover muda cor, click move para nova posição -->
      <a-cylinder
        id="cilindro"
        class="clickable"
        position="2.5 1 -4"
        radius="0.5"
        height="2"
        color="#FFC65D"
        event-set__enter="_event: mouseenter; material.color: #FFE44D"
        event-set__leave="_event: mouseleave; material.color: #28b69e"
        animation__jump="property: position; to: 2.5 3 -6;
                         dur: 800; startEvents: click;
                         easing: easeOutBack"
      ></a-cylinder>
```

## Explicação detalhada — interação a interação

### Interação 1: Hover muda cor do cubo

```
event-set__enter="_event: mouseenter; material.color: #00FFFF"
event-set__leave="_event: mouseleave; material.color: #4CC3D9"
```

| Parte | Significado |
|-------|-------------|
| `event-set__enter` | Nome da regra (inventado por nós: "enter"). O `__` (dois underscores) separa o prefixo do nome. |
| `_event: mouseenter` | "Quando o retículo **entrar** neste objeto..." |
| `material.color: #00FFFF` | "...muda a cor do material para ciano (#00FFFF)." |
| `event-set__leave` | Segunda regra: quando o retículo **sai**... |
| `material.color: #4CC3D9` | ...volta à cor original. |

**Resultado:** ao apontar para o cubo, ele fica ciano. Ao sair, volta a azul.

### Interação 2: Click no cubo muda cor da esfera

```
event-set__click="_event: click; _target: #esfera; material.color: #9B59B6"
```

| Parte | Significado |
|-------|-------------|
| `_event: click` | "Quando **clicarem** neste cubo..." |
| `_target: #esfera` | "...vai afetar o objeto com `id="esfera"` (a esfera), NÃO o cubo." |
| `material.color: #9B59B6` | "...muda a cor da esfera para roxo." |

**Resultado:** clicar no cubo faz a esfera ficar roxa. É uma ação "à distância".

### Interação 3: Click na esfera mostra texto

```
event-set__show="_event: click; _target: #info-text; visible: true"
```

Na esfera: clicar torna visível o `#info-text`.

No texto flutuante:
```
visible="false"                    ← começa escondido
event-set__hide="_event: click; visible: false"  ← clicar nele esconde-o
```

**Resultado:** clicar na esfera mostra uma mensagem. Clicar na mensagem esconde-a.

> "Porquê `class="clickable"` no texto? Porque sem esta classe, o retículo não consegue 'ver' o texto para clicar nele."

### Interação 4: Click no cilindro move-o

```
animation__jump="property: position; to: 2.5 3 -6;
                 dur: 800; startEvents: click;
                 easing: easeOutBack"
```

| Parte | Significado |
|-------|-------------|
| `animation__jump` | Uma animação chamada "jump". |
| `property: position` | Anima a propriedade "posição". |
| `to: 2.5 3 -6` | Destino: sobe para Y=3 e recua para Z=-6. |
| `dur: 800` | Duração: 800 milissegundos (0.8 segundos). |
| `startEvents: click` | Só começa quando o objeto recebe um `click`. Sem isto, a animação começaria sozinha ao carregar a página. |
| `easing: easeOutBack` | Tipo de movimento: chega ao destino e "ressalta" ligeiramente. |

**Resultado:** clicar no cilindro fá-lo voar suavemente para cima.

## Guardar e ver

- Ctrl+S → testar cada interação:
  1. Apontar para o cubo → fica ciano → sair → volta a azul ✓
  2. Clicar no cubo → esfera fica roxa ✓
  3. Clicar na esfera → aparece texto ✓
  4. Clicar no texto → desaparece ✓
  5. Clicar no cilindro → voa para cima ✓

## Checkpoint ✓

- [ ] As 5 interações acima funcionam
- [ ] Todos os objetos interativos têm `class="clickable"`

---

# PASSO 8 — Label "Heart" ao apontar para o coração (10 min)

## O que o formador diz

> "Agora vamos usar a mesma técnica para criar algo útil em medicina: quando apontamos para um órgão, aparece o nome."
>
> "O padrão é igual ao texto flutuante: uma entidade escondida (`visible="false"`) que se torna visível com `event-set` no hover."

## O que os alunos escrevem

**1)** Adicionar o label **ANTES** do coração:

```html
      <!-- LABEL "Heart" — aparece ao apontar para o coração -->
      <a-entity
        id="heart-label"
        text="value: Heart; align: center; color: #FFFFFF; width: 4"
        position="0 2.8 -3"
        visible="false"
      ></a-entity>
```

**2)** No `<a-entity id="heart" ...>`, adicionar estas 2 linhas e `class="clickable"`:

Substituir o bloco do coração inteiro por:

```html
      <!-- CORAÇÃO 3D — roda + mostra label ao hover -->
      <a-entity
        id="heart"
        class="clickable"
        obj-model="obj: #heart-obj; mtl: #heart-mtl"
        material="side: double"
        position="0 1.5 -3"
        rotation="0 180 0"
        scale="0.12 0.12 0.12"
        animation="property: rotation; to: 0 540 0;
                   loop: true; dur: 12000; easing: linear"
        event-set__enter="_event: mouseenter; _target: #heart-label; visible: true"
        event-set__leave="_event: mouseleave; _target: #heart-label; visible: false"
      ></a-entity>
```

## Explicação

| Código | O que faz |
|--------|-----------|
| `id="heart-label"` | Nome único do label — para o coração poder referenciá-lo. |
| `text="value: Heart; align: center; color: #FFFFFF; width: 4"` | Texto 3D com a palavra "Heart", centrado, branco, 4 metros de largura máxima. |
| `position="0 2.8 -3"` | Posicionado acima do coração (Y=2.8, mesmo X e Z). |
| `visible="false"` | **Começa escondido.** Só aparece quando algo o torna `visible: true`. |
| `event-set__enter="... _target: #heart-label; visible: true"` | Quando o retículo **entra** no coração → mostra o label. |
| `event-set__leave="... _target: #heart-label; visible: false"` | Quando o retículo **sai** do coração → esconde o label. |

> **Padrão reutilizável para medicina:**
> Podem duplicar este padrão para qualquer órgão: criar um label escondido + event-set no órgão que o mostra/esconde. É um sistema de "tooltips 3D".

## Guardar e ver

- Ctrl+S → Apontar para o coração → "Heart" aparece por cima → sair → desaparece

## Checkpoint ✓

- [ ] Apontar para o coração mostra "Heart"
- [ ] Sair do coração faz "Heart" desaparecer
- [ ] O coração continua a rodar

---

# PASSO 9 — Animação extra: pulso na esfera + fusing no retículo (10 min)

## O que o formador diz

> "Vamos adicionar mais animações para tornar a cena mais viva."
>
> "A esfera vai ter um efeito de 'pulso' — como se estivesse a respirar. E o retículo vai encolher quando estamos a 'apontar' para um objeto (feedback visual do fuse)."

## O que os alunos escrevem

**1)** No `<a-sphere>`, adicionar esta linha (novo atributo, DEPOIS do `event-set__show`):

```
        animation__pulse="property: scale; from: 1 1 1; to: 1.08 1.08 1.08;
                          dir: alternate; dur: 1200; loop: true;
                          easing: easeInOutSine"
```

**2)** No retículo (o `<a-entity>` dentro da `<a-camera>`), adicionar estas 2 animações:

```
          animation__fusing="property: scale; from: 1 1 1; to: 0.5 0.5 0.5;
                             dur: 1500; startEvents: fusing;
                             easing: easeInCubic"
          animation__reset="property: scale; to: 1 1 1;
                            dur: 200; startEvents: mouseleave"
```

## Explicação

| Código | O que faz |
|--------|-----------|
| `animation__pulse` | Segunda animação na esfera (a primeira seria se houvesse). O `__pulse` é o nome. |
| `from: 1 1 1; to: 1.08 1.08 1.08` | A escala vai de 100% a 108% — cresce 8%. |
| `dir: alternate` | **Alternado**: vai de 1 a 1.08, depois volta de 1.08 a 1, e repete. Efeito de "respiração". |
| `animation__fusing` | Quando o fuse começa a contar (`startEvents: fusing`), o retículo encolhe de 1 para 0.5 em 1.5 s. Feedback visual: "estou a contar..." |
| `animation__reset` | Quando o retículo sai do objeto (`startEvents: mouseleave`), volta ao tamanho normal rapidamente (200 ms). |

## Guardar e ver

- Ctrl+S → A esfera "pulsa" suavemente
- Apontar para um objeto → o retículo encolhe lentamente → sai → volta ao normal

## Checkpoint ✓

- [ ] A esfera expande e contrai suavemente (pulso)
- [ ] O retículo encolhe quando aponto para um objeto clickable

---

# PASSO 10 — Overlay com instruções (10 min)

## O que o formador diz

> "Último passo! Vamos adicionar uma caixa de instruções visível no ecrã — como as legendas num jogo."
>
> "Isto não é A-Frame — é HTML e CSS normais. O HTML define **o que** aparece, o CSS define **como** aparece (cores, posição, tamanho)."

## O que os alunos escrevem

**1)** No `<head>`, adicionar **ANTES** de `</head>`:

```html
    <style>
      /* CSS: define a aparência da caixa de instruções */
      #overlay {
        position: fixed;       /* fica fixa no ecrã, não se move com scroll */
        top: 10px;             /* a 10 pixels do topo */
        left: 10px;            /* a 10 pixels da esquerda */
        z-index: 9999;         /* fica "por cima" de tudo */
        background: rgba(0, 0, 0, 0.75); /* fundo preto, 75% opaco */
        color: white;          /* texto branco */
        padding: 14px 20px;    /* espaço interior */
        border-radius: 10px;   /* cantos arredondados */
        font-family: Arial, sans-serif;
        font-size: 14px;
        max-width: 340px;      /* largura máxima */
        line-height: 1.5;      /* espaço entre linhas */
        pointer-events: none;  /* cliques "atravessam" a caixa */
      }
      #overlay h3 { margin: 0 0 8px 0; font-size: 16px; }
      #overlay ul { margin: 0; padding-left: 18px; }
      #overlay li { margin-bottom: 4px; }
    </style>
```

**2)** No `<body>`, adicionar **ANTES** de `<a-scene>`:

```html
    <!-- OVERLAY: caixa de instruções visível no ecrã -->
    <div id="overlay">
      <h3>Instruções</h3>
      <ul>
        <li><b>Mover:</b> W A S D (PC) | thumbstick (VR) | <b>Olhar:</b> arrastar rato</li>
        <li><b>Interagir:</b> aponta + clica (PC) ou espera 1.5s (VR)</li>
        <li>Cubo azul: hover muda cor, click muda a esfera</li>
        <li>Esfera rosa: click mostra mensagem</li>
        <li>Cilindro amarelo: click move</li>
        <li>Coração: aponta para ver "Heart"</li>
      </ul>
    </div>
```

## Explicação de CSS (para quem nunca viu)

> "**CSS** (Cascading Style Sheets) é a linguagem que define a aparência visual. O HTML diz 'quero uma caixa com uma lista', o CSS diz 'essa caixa é preta, semi-transparente, com cantos redondos, posicionada no canto superior esquerdo'."
>
> "O bloco `<style>` contém as regras CSS. Cada regra tem um **seletor** (`#overlay` = o elemento com id 'overlay') e **propriedades** (`color: white`, `background: ...`)"

| CSS | O que faz |
|-----|-----------|
| `#overlay` | Seletor: aplica-se ao elemento com `id="overlay"`. O `#` em CSS significa "id". |
| `position: fixed` | A caixa fica fixa no ecrã — não se move quando a cena roda. |
| `rgba(0, 0, 0, 0.75)` | Cor em formato RGBA: (Vermelho=0, Verde=0, Azul=0, Opacidade=0.75). Preto a 75%. |
| `pointer-events: none` | Cliques "passam através" da caixa. Sem isto, a caixa bloquearia os cliques na cena. |
| `<div>` | Tag HTML para um "bloco" genérico. Usamos para agrupar conteúdo. |
| `<ul>` / `<li>` | Lista não-ordenada / item da lista. |
| `<b>` | Texto a **negrito**. |

## Guardar e ver

- Ctrl+S → aparece uma caixa semi-transparente no canto superior esquerdo com as instruções

## Checkpoint ✓

- [ ] Caixa de instruções visível no canto superior esquerdo
- [ ] A caixa não bloqueia a interação com a cena (cliques passam através)

---

# PASSO 11 — Teste nos óculos VR / Quest (20 min)

## O que o formador diz

> "A cena está completa! Agora vamos testá-la nos óculos Meta Quest."

## Procedimento

1. **Descobrir o IP do PC:**
   - Windows: abrir Terminal → escrever `ipconfig` → procurar **IPv4 Address** (ex: `192.168.1.42`)

2. **No Quest:**
   - Abrir o browser (Meta Browser)
   - Escrever na barra: `http://192.168.1.42:5500` (substituir pelo vosso IP)

3. **Testar o movimento com thumbstick:**
   - Usar o thumbstick do controlador para andar pela cena ✓
   - Confirmar que ficamos no chão (não voamos) ✓

4. **Testar todas as interações com gaze:**
   - Olhar para o cubo → cor muda (hover) ✓
   - Olhar para o cubo e esperar 1.5s → esfera muda de cor (click via fuse) ✓
   - Olhar para a esfera e esperar → texto aparece ✓
   - Olhar para o cilindro e esperar → move-se ✓
   - Olhar para o coração → "Heart" aparece ✓

## Checkpoint ✓

- [ ] A cena carrega no Quest
- [ ] O retículo é visível
- [ ] Conseguimos mover com o thumbstick do controlador
- [ ] Pelo menos 3 interações funcionam com gaze

## Erros comuns

| Problema | Solução |
|----------|---------|
| Não carrega no Quest | PC e Quest na mesma rede Wi-Fi? URL é `http://` (não `https://`)? Porto correto (5500)? |
| Retículo não aparece | Aumentar `radiusOuter: 0.03` ou `opacity: 1.0`. |
| Interações não disparam | Confirmar `class="clickable"` nos objetos. Confirmar que `cursor="fuse: true"` existe. |
| Imagem não carrega | Ficheiro demasiado grande para o Quest. Reduzir resolução. |

---

# WRAP-UP (10 min)

> "Recapitulando: em 3 horas, partimos de uma página em branco e construímos:"
> 1. Uma cena VR com panorama 360°
> 2. Formas 3D e um modelo anatómico real
> 3. Interações: hover muda cor, click muda cor remota, mostra/esconde texto, move objetos
> 4. Label informativo num órgão (padrão reutilizável)
> 5. Animações suaves (rotação, pulso)
> 6. Tudo funciona em PC e em VR com óculos
>
> "**Tudo isto num único ficheiro HTML, sem uma linha de JavaScript.**"
>
> "Para continuar: site oficial → aframe.io. Podem adicionar modelos de outros órgãos, sons, vídeos 360°, e até tracking de mãos."

---

# CHECKLIST DE TROUBLESHOOTING (referência rápida)

| # | Problema | Causa | Solução |
|---|----------|-------|---------|
| 1 | Ecrã preto / em branco | Abriu `file://` em vez de Live Server | URL deve ser `http://127.0.0.1:5500` |
| 2 | Objetos sem profundidade | Sem luzes na cena | Adicionar as 3 entidades de luz |
| 3 | Retículo invisível no Quest | Ring muito pequeno | Aumentar `radiusOuter` para 0.03 |
| 4 | Click não dispara | Falta `class="clickable"` | Adicionar a class no objeto |
| 5 | Click não dispara (2) | Script event-set não carregou | Verificar internet e URL do script na consola (F12) |
| 6 | Hover no coração não mostra label | `_target` não corresponde ao `id` | Confirmar `_target: #heart-label` e `id="heart-label"` |
| 7 | Label do coração pisca | Coração a rodar perde contacto com raycaster | Abrandar rotação: `dur: 20000` |
| 8 | Modelo 3D não aparece | Caminho do ficheiro errado | F12 → Console → procurar erro 404 |
| 9 | Texturas do coração em falta | Ficheiros .png não estão na pasta | Confirmar que `assets/heart/` tem os ficheiros .png |
| 10 | Quest não carrega a página | PC e Quest em redes diferentes | Ambos na mesma Wi-Fi, URL com `http://` |
| 11 | Porta 5500 ocupada | Outro Live Server aberto | Settings → liveServer.settings.port → 5501 |
| 12 | Texto aparece "ao contrário" | Orientação do texto | Adicionar `rotation="0 180 0"` no label |

---

# FICHEIRO FINAL COMPLETO

No final dos 10 passos, o ficheiro `index.html` deve corresponder exatamente ao que está no projeto.
Abrir `index.html` no VS Code para verificar.

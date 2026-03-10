# PLANO DE AULA — VR para Medicina com A-Frame

## Informação geral

| Item | Detalhe |
|------|---------|
| Duração | 3 horas (com pausa) |
| Público | Estudantes de Medicina, sem experiência de programação |
| Resultado | Compreender e modificar uma cena VR interativa, testada no PC e nos óculos Meta Quest |
| Abordagem | Os alunos recebem o ficheiro `index.html` completo. O formador explica de cima para baixo. Os alunos fazem **exercícios** de modificação. |

> **Nota:** O código e este plano seguem a **mesma ordem** — basta ler o ficheiro de cima para baixo.

---

## ANTES DA AULA — Setup (formador prepara)

1. Cada PC deve ter o **VS Code** instalado + extensão **Live Server**
2. Copiar a pasta do projeto para cada PC (com `index.html` + pasta `assets/`)
3. Confirmar que há Wi-Fi partilhado entre PCs e os Quest
4. Testar que o `index.html` abre corretamente via Live Server

---

# PASSO 1 — Abrir o projeto e entender HTML (15 min)

## O que o formador diz

> "Vamos abrir o ficheiro que já temos preparado. Não vão escrever tudo do zero — vão **entender** o que cada parte faz e depois **modificar**."
>
> "HTML funciona com **tags** — palavras entre `< >`. A maioria tem abertura e fecho:"
> ```
> <title>Olá</title>
> ```

## O que os alunos fazem

1. VS Code → File → Open Folder → pasta do projeto
2. Abrir `index.html`
3. Clicar direito → **"Open with Live Server"**
4. O browser mostra a cena VR completa

## O formador explica (linhas 1-5 do código)

```html
<!DOCTYPE html>        ← "Este ficheiro é HTML moderno"
<html lang="pt">       ← Início do documento, língua portuguesa
  <head>               ← Informações sobre a página (não visíveis)
    <meta charset="utf-8" />   ← Suporta acentos (ã, é, ç)
    <title>Aula VR - Medicina</title>  ← Título no separador do browser
```

> **Conceito-chave:** HTML = caixas dentro de caixas. `<html>` contém `<head>` e `<body>`.

## Checkpoint ✓

- [ ] O browser mostra a cena VR
- [ ] O URL começa por `http://127.0.0.1:5500`

---

# PASSO 2 — Bibliotecas: os motores por trás da cena (10 min)

## O que o formador diz

> "Estas 3 linhas no `<head>` são **bibliotecas** — código que outra pessoa escreveu e que nós reutilizamos."

## O formador explica (linhas 7-11 do código)

| Biblioteca | O que faz | Sem ela... |
|------------|-----------|------------|
| **A-Frame** | Motor 3D. Tags como `<a-box>`, `<a-sphere>` | Nada funciona |
| **Event-Set** | Interações (hover, click) no HTML | Precisávamos de JavaScript |
| **Extras** | Movimento com thumbstick VR | Não andávamos em VR |

> "Pensem como 'superpoderes' que adicionamos ao HTML."

---

# PASSO 3 — Ambiente: assets, céu panorâmico e som (15 min)

## O que o formador diz

> "Agora entramos na cena 3D. `<a-scene>` é o 'palco' — tudo dentro vive no mundo 3D."
>
> "O `<a-assets>` é um 'armazém' que pré-carrega ficheiros pesados antes de mostrar a cena."

## O formador explica (linhas 39-58 do código)

| Código | O que faz |
|--------|-----------|
| `<a-assets>` | Armazém: pré-carrega imagens, modelos 3D e sons |
| `id="pano"` | Nome único — depois referenciamos com `#pano` |
| `crossorigin="anonymous"` | Permissão técnica para o A-Frame usar a imagem |
| `<a-asset-item>` | Pré-carrega ficheiros 3D (.obj = forma, .mtl = materiais) |
| `<audio preload="auto">` | Pré-carrega o som inteiro |
| `<a-sky src="#pano">` | Esfera gigante com a imagem panorâmica por dentro |
| `sound="src: #som-ambiente; ..."` | Som espacial: ao afastar-se, o som fica mais baixo! |

> **Conceito-chave — `id` e `#`:** `id="pano"` dá um nome. `#pano` referencia esse nome.

> **Conceito-chave — Som espacial:** O som vem de um ponto no espaço 3D. Se nos afastarmos, fica mais baixo — como na vida real. Ideal para simular batimentos, alarmes, etc.

## EXERCÍCIO 1 — Mudar a rotação do céu

Encontrar: `<a-sky src="#pano" rotation="0 -90 0">`

**Tarefa:** Mudar `rotation="0 -90 0"` para `rotation="0 180 0"`. Ctrl+S e ver. Depois voltar ao original.

## Checkpoint ✓

- [ ] Entendem o sistema de assets + referência com `#`
- [ ] O céu mudou ao alterar a rotação

---

# PASSO 4 — Palco: luzes e chão (10 min)

## O que o formador diz

> "Sem luz, os objetos ficam 'planos'. E precisamos de um chão."

## O formador explica (linhas 60-72 do código)

| Tipo | O que faz |
|------|-----------|
| **Luz ambient** | Ilumina tudo por igual (dia nublado) |
| **Luz directional** (×2) | Como o sol — cria sombras. Duas luzes de ângulos diferentes |
| `<a-plane rotation="-90 0 0">` | Plano deitado (-90° no eixo X) = chão |

> **Conceito-chave — Coordenadas 3D:**
> - **X** = esquerda (-) / direita (+)
> - **Y** = baixo (-) / cima (+)
> - **Z** = à frente (-) / atrás (+) — Z negativo é "para a frente"

## EXERCÍCIO 2 — Mudar o chão

**Tarefa A:** Mudar `color="#7BC8A4"` para `#D2691E` (castanho) ou `#4169E1` (azul). Ctrl+S.

**Tarefa B:** Mudar `width="20"` para `width="50"`. O chão fica maior!

Depois: Ctrl+Z para voltar ao original.

## Checkpoint ✓

- [ ] Mudaram a cor do chão
- [ ] Entendem X, Y, Z

---

# PASSO 5 — Cubo: forma + interação + animação (20 min)

## O que o formador diz

> "Agora vamos ver o primeiro objeto interativo. Tem **3 camadas**:"
> 1. **Forma**: o que É (cubo, cor, posição)
> 2. **Interação**: o que FAZ quando apontamos (event-set)
> 3. **Animação**: como se MOVE sozinho

## O formador explica (linhas 74-86 do código)

### Camada 1 — A forma

```html
<a-box
  class="clickable"
  position="-4 0.7 -5"
  rotation="0 30 0"
  width="1.2" height="1.2" depth="1.2"
  color="#4CC3D9"
```

| Atributo | Significado |
|----------|-------------|
| `<a-box>` | Cria um cubo/paralelepípedo |
| `class="clickable"` | Marca como interativo — o retículo só vê objetos com esta classe |
| `position="-4 0.7 -5"` | X=-4 (esquerda), Y=0.7 (acima do chão), Z=-5 (5m à frente) |
| `color="#4CC3D9"` | Cor hexadecimal (azul claro). Hex = 2 dígitos R + 2 G + 2 B |

### Camada 2 — Interações (event-set)

> "A fórmula é sempre: `event-set__NOME=\"_event: QUANDO; PROPRIEDADE: VALOR\"`"

```html
  event-set__enter="_event: mouseenter; material.color: #00FFFF"
  event-set__leave="_event: mouseleave; material.color: #4CC3D9"
  event-set__click="_event: click; _target: #esfera; material.color: #9B59B6"
```

| Regra | Tradução |
|-------|----------|
| `event-set__enter` | "Quando o retículo **entrar** (hover) → muda cor para ciano" |
| `event-set__leave` | "Quando **sair** → volta à cor original" |
| `event-set__click` | "Quando **clicar** → muda a cor da **esfera** (outro objeto!) para roxo" |

> "`_target: #esfera` = o efeito é noutro objeto! Ação à distância."

### Camada 3 — Animação

```html
  animation="property: rotation; to: 0 390 0;
             loop: true; dur: 8000; easing: linear"
```

| Parte | Significado |
|-------|-------------|
| `property: rotation` | O que anima: a rotação |
| `to: 0 390 0` | Destino: 390° no eixo Y |
| `loop: true` | Repete infinitamente |
| `dur: 8000` | 8 segundos por ciclo |
| `easing: linear` | Velocidade constante |

## EXERCÍCIO 3 — Modificar o cubo

**Tarefa A:** Mudar a cor de hover. Encontrar `material.color: #00FFFF` e mudar para `#FF0000` (vermelho). Ctrl+S → apontar para o cubo.

**Tarefa B:** Mudar a velocidade de rotação. `dur: 8000` → `dur: 2000` (rápido!) ou `dur: 20000` (lento).

**Tarefa C:** Mudar o efeito do click. Em vez de mudar a esfera para roxo, mudar para verde: `material.color: #00FF00`.

Depois: Ctrl+Z para voltar.

## Checkpoint ✓

- [ ] Entendem a fórmula event-set: `_event: QUANDO; PROPRIEDADE: VALOR`
- [ ] Entendem `_target` (ação à distância)
- [ ] Mudaram pelo menos uma cor e uma velocidade

---

# PASSO 6 — Esfera + Texto flutuante: mostrar/esconder (15 min)

## O que o formador diz

> "A esfera usa o mesmo padrão do cubo (hover muda cor). Mas adiciona algo novo: **clicar mostra um texto que estava escondido**."

## O formador explica (linhas 88-111 do código)

### Esfera

```html
  event-set__show="_event: click; _target: #info-text; visible: true"
```

> "Click na esfera → torna o `#info-text` visível."

### Texto flutuante

```html
<a-entity id="info-text" visible="false" ...
  event-set__hide="_event: click; visible: false"
```

| Conceito | Explicação |
|----------|------------|
| `visible="false"` | Começa **escondido** |
| A esfera faz `visible: true` | Mostra o texto |
| O texto faz `visible: false` em si próprio | Click para fechar |

> **Padrão reutilizável:** esconder + mostrar com visible. Perfeito para informação em medicina (clicar num órgão → aparece descrição).

## EXERCÍCIO 4 — Mudar o texto

**Tarefa A:** Mudar `value: Bem-vindos a VR Medicina!` para outra frase (ex: `value: Anatomia Cardíaca`). Ctrl+S → clicar na esfera.

**Tarefa B (bónus):** Mudar a cor do fundo do texto. Encontrar `material="color: #000000"` e mudar para `#003366` (azul escuro).

## Checkpoint ✓

- [ ] Entendem o padrão visible: false/true
- [ ] Mudaram o texto com sucesso

---

# ☕ PAUSA — 15 minutos

---

# PASSO 7 — Cilindro, cone, torus e dodecaedro: mais formas (15 min)

## O que o formador diz

> "Já conhecem o padrão: forma + interação + animação. Agora vamos ver 4 objetos de uma vez. Cada um mostra algo diferente."

## O formador explica (linhas 113-155 do código)

| Objeto | Forma | Novidade |
|--------|-------|----------|
| **Cilindro** `<a-cylinder>` | Tubo amarelo | `startEvents: click` — animação que SÓ começa ao clicar |
| **Cone** `<a-cone>` | Funil verde | `radius-bottom` e `radius-top` (topo = 0 → pontiagudo) |
| **Torus** `<a-torus>` | Anel roxo | Roda em **dois eixos** ao mesmo tempo (`to: 360 360 0`) |
| **Dodecaedro** `<a-dodecahedron>` | Poliedro vermelho | **Duas animações simultâneas**: `animation__spin` + `animation__bounce` |

### Conceitos novos neste passo

| Conceito | Exemplo |
|----------|---------|
| `startEvents: click` | A animação **não começa sozinha** — espera por um evento |
| `animation__spin` + `animation__bounce` | Duas animações no mesmo objeto com nomes diferentes (`__spin`, `__bounce`) |
| `dir: alternate` | Vai e volta (sobe → desce → sobe...) |
| `easing: easeOutBack` | Chega ao destino e "ressalta" |
| `easing: easeInOutQuad` | Suave no início e no fim |

## EXERCÍCIO 5 — Experimentar com as formas

**Tarefa A:** Mudar a cor do torus de `#8E44AD` para outra. Ctrl+S e ver.

**Tarefa B:** Mudar o dodecaedro: alterar `dur: 2000` no `animation__bounce` para `dur: 500` (salta rápido!) ou `dur: 5000` (flutua lento).

**Tarefa C (bónus):** Adicionar `animation__bounce` ao cone para ele flutuar também. Copiar do dodecaedro e mudar as posições para coincidir com o cone (`from: 1 1 -7; to: 1 2 -7`).

## Checkpoint ✓

- [ ] Entendem `startEvents` (animação que espera)
- [ ] Entendem múltiplas animações (`__nome`)
- [ ] Modificaram pelo menos uma forma

---

# PASSO 8 — Coração 3D: modelo, label e hitbox (15 min)

## O que o formador diz

> "Agora o conteúdo médico real. Este coração é um modelo 3D (não uma forma simples). Tem 3 partes: label, hitbox e o modelo em si."

## O formador explica (linhas 157-179 do código)

### Label "Heart"

```html
<a-entity id="heart-label" text="value: Heart; ..." visible="false">
```

> "Texto escondido acima do coração."

### Hitbox invisível

```html
<a-sphere class="clickable" material="opacity: 0; transparent: true"
  event-set__enter="_event: mouseenter; _target: #heart-label; visible: true"
  event-set__leave="_event: mouseleave; _target: #heart-label; visible: false"
```

> "Porquê uma esfera invisível? O modelo do coração tem **milhares de triângulos**. O raycaster teria de testar cada um — isto causa **quebras de frame rate** em VR. A esfera invisível tem apenas 6 triângulos — rápido!"

| Sem hitbox | Com hitbox |
|------------|-----------|
| Raycaster testa milhares de triângulos | Raycaster testa 6 triângulos |
| Frame rate cai, VR fica desconfortável | Frame rate estável |

### Coração 3D

```html
<a-entity obj-model="obj: #heart-obj; mtl: #heart-mtl" ...
  animation="..."
  animation__pulse="... dir: alternate; dur: 800; ..."
```

| Atributo | Significado |
|----------|-------------|
| `obj-model` | Monta o modelo 3D (geometria + materiais dos assets) |
| `material="side: double"` | Renderiza ambos os lados (sem isto, partes ficam invisíveis) |
| `scale="0.12 0.12 0.12"` | Modelo original é enorme — escalamos para 12% |
| `animation__pulse` com `dir: alternate` | Cresce e encolhe = **batimento cardíaco** |
| `dur: 800` | ~75 BPM — próximo de um ritmo cardíaco real |

> **NÃO tem `class="clickable"`** — é apenas visual. A hitbox trata da interação.

## EXERCÍCIO 6 — Modificar o coração

**Tarefa A:** Mudar o ritmo cardíaco. `dur: 800` → `dur: 400` (taquicardia!) ou `dur: 1500` (bradicardia).

**Tarefa B:** Mudar o label. `value: Heart` → `value: Coração Humano`.

**Tarefa C:** Mudar o tamanho. `scale="0.12 0.12 0.12"` → `scale="0.2 0.2 0.2"` (maior).

Depois: Ctrl+Z para voltar.

## Checkpoint ✓

- [ ] Entendem o padrão hitbox (otimização VR)
- [ ] Entendem `dir: alternate` (batimento cardíaco)
- [ ] Mudaram o ritmo ou o label

---

# PASSO 9 — Câmara, retículo e movimento (10 min)

## O que o formador diz

> "Como é que nos movemos e interagimos? O sistema de câmara usa um padrão chamado **camera rig** — como um carro: o carro (rig) move-se, nós (câmara) estamos sentados lá dentro."

## O formador explica (linhas 181-199 do código)

| Código | O que faz |
|--------|-----------|
| `id="rig"` / `movement-controls="fly: false"` | Plataforma de movimento: WASD (PC), thumbstick (VR). `fly: false` = fica no chão |
| `position="0 0 5"` | Começa 5m atrás para ver os objetos |
| `camera` / `look-controls` | Câmara + olhar à volta (rato PC, cabeça VR) |
| `position="0 1.6 0"` | Altura dos olhos: 1.6m |
| `cursor="fuse: true; fuseTimeout: 1500"` | Em VR: olhar 1.5s = click |
| `raycaster="objects: .clickable; interval: 100"` | Raio invisível, só vê objetos com `class="clickable"` |
| `animation__fusing` | Retículo encolhe durante o fuse (feedback visual) |

## EXERCÍCIO 7 — Mudar o cursor

**Tarefa A:** Mudar o tempo do fuse. `fuseTimeout: 1500` → `fuseTimeout: 500` (rápido) ou `fuseTimeout: 3000` (lento). Ctrl+S e testar.

**Tarefa B:** Mudar o tamanho do retículo. `radiusOuter: 0.02` → `radiusOuter: 0.05` (maior).

## Checkpoint ✓

- [ ] Entendem o camera rig
- [ ] Entendem o fuse (gaze = click em VR)

---

# PASSO 10 — Overlay: instruções no ecrã (10 min)

## O que o formador diz

> "A caixa de instruções no canto do ecrã não é A-Frame — é **HTML e CSS** normais."
>
> "Reparem que está **depois** do `</a-scene>` — está fora do mundo 3D. O CSS (`position: fixed`) cola-a no canto do ecrã."

## O formador explica (CSS no head + HTML no fundo do body)

| Conceito | Explicação |
|----------|------------|
| `<style>` no `<head>` | CSS define a **aparência** (cores, posição, tamanho) |
| `#overlay` | Seletor CSS: aplica-se ao elemento com `id="overlay"` |
| `position: fixed` | Fixa no ecrã, não se move |
| `rgba(0,0,0, 0.75)` | Preto semi-transparente (75% opaco) |
| `pointer-events: none` | Cliques passam através — não bloqueia a cena |
| `<div>` | Bloco HTML genérico. `<ul>` = lista. `<li>` = item. `<b>` = negrito |

## A-Frame Inspector

> "O A-Frame tem um editor visual embutido! Carreguem **Ctrl+Alt+I** para abrir o Inspector."

1. Ctrl+Alt+I → painel com todos os objetos
2. Clicar num objeto → ver propriedades
3. Arrastar → muda posição em tempo real
4. **Não guarda** — ao fechar volta ao original

## EXERCÍCIO 8 — Overlay e Inspector

**Tarefa A:** Adicionar uma nova linha ao overlay. Dentro do `<ul>`, adicionar:
```html
<li>Dodecaedro vermelho: flutua e roda</li>
```

**Tarefa B:** Abrir o Inspector (Ctrl+Alt+I), selecionar um objeto, arrastá-lo. Anotar a posição nova.

## Checkpoint ✓

- [ ] Adicionaram uma linha ao overlay
- [ ] Abriram o Inspector

---

# PASSO 11 — Teste nos óculos VR / Quest (20 min)

## Procedimento

1. **IP do PC:** Terminal → `ipconfig` → IPv4 Address (ex: `192.168.1.42`)
2. **No Quest:** browser → `http://192.168.1.42:5500`
3. **Testar:**
   - Thumbstick para andar ✓
   - Hover nos objetos → cores mudam ✓
   - Fuse (olhar 1.5s) → click dispara ✓
   - Afastar-se do som → fica mais baixo ✓
   - Olhar para o coração → "Heart" aparece ✓

## Erros comuns

| Problema | Solução |
|----------|---------|
| Não carrega no Quest | PC e Quest na mesma Wi-Fi? URL `http://` (não `https://`)? |
| Retículo não aparece | Aumentar `radiusOuter: 0.03` |
| Interações não disparam | Confirmar `class="clickable"` |
| Som não toca | Clicar uma vez na cena (browser bloqueia autoplay) |

---

# EXERCÍCIO FINAL — Adicionar um objeto novo (15 min)

## Tarefa

Adicionar uma **esfera flutuante** à cena. Depois do dodecaedro, adicionar:

```html
      <!-- NOVO OBJETO: esfera verde (exercício dos alunos) -->
      <a-sphere
        class="clickable"
        position="2 1.2 -3"
        radius="0.6"
        color="#27AE60"
        event-set__enter="_event: mouseenter; material.color: #2ECC71"
        event-set__leave="_event: mouseleave; material.color: #27AE60"
        animation="property: position; from: 2 1.2 -3; to: 2 2 -3;
                   dir: alternate; dur: 3000; loop: true;
                   easing: easeInOutSine"
      ></a-sphere>
```

## Desafios extra

1. Mudar a cor para uma à vossa escolha
2. Adicionar um **label** (copiar o padrão do heart-label)
3. Adicionar uma segunda animação (ex: `animation__spin` de rotação)
4. Adicionar uma linha ao overlay para descrever o novo objeto

---

# WRAP-UP (10 min)

> "Recapitulando: nesta sessão:"
> 1. Percebemos HTML e como o A-Frame transforma HTML em 3D
> 2. Carregámos assets (imagens, modelos 3D, sons espaciais)
> 3. Criámos um palco (luzes, chão)
> 4. Aprendemos o padrão **forma + interação + animação** — aplicámos a 7 objetos
> 5. Importámos um modelo 3D real (coração) com batimento cardíaco
> 6. Entendemos otimização VR (hitbox)
> 7. Configurámos câmara e navegação (camera rig, fuse)
> 8. Descobrimos o Inspector (Ctrl+Alt+I)
> 9. Testámos em VR com óculos
> 10. Criámos um objeto novo do zero!
>
> "**Tudo num único ficheiro HTML.**"
>
> "Site oficial: **aframe.io**"

---

# CHECKLIST DE TROUBLESHOOTING

| # | Problema | Solução |
|---|----------|---------|
| 1 | Ecrã preto | URL deve ser `http://127.0.0.1:5500` (não `file://`) |
| 2 | Objetos planos | Verificar as 3 entidades de luz |
| 3 | Retículo invisível | Aumentar `radiusOuter` |
| 4 | Click não dispara | Falta `class="clickable"` |
| 5 | Hover no coração falha | Confirmar `_target: #heart-label` e `id="heart-label"` |
| 6 | Frame rate baixo no coração | Usar hitbox invisível |
| 7 | Modelo 3D não aparece | F12 → Console → procurar erro 404 |
| 8 | Quest não carrega | PC e Quest na mesma Wi-Fi, `http://` |
| 9 | Som não toca | Clicar na cena (browser bloqueia autoplay) |

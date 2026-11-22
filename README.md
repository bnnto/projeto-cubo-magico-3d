<span id="top"></span>
<h1 align="center">
  <br> Cubo Mágico 3D
</h1>

<p align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
  <img src="https://img.shields.io/badge/Three.js-000000?style=for-the-badge&logo=three.js&logoColor=white" alt="Three.js" />
</p>

<p align="center">
  Cubo mágico 3x3x3 interativo feito com <b>Three.js</b>, em um único arquivo HTML.<br>
  Projeto em grupo da faculdade (Computação Gráfica).
</p>

---

## Equipe

- [Bento Guilherme Gomes Oliveira](https://github.com/bnnto) 
- [João Victor Castelo Branco de Sena](https://github.com/joao0cb) 
- [Lorenna Meneses de Almeida](https://github.com/lorennam) 

## Como executar

1. Baixe ou clone o repositório.
2. Abra o arquivo `cubo-magico.html` em um navegador (Chrome, Edge ou Firefox).
3. É preciso ter internet, pois o Three.js (r128) e o OrbitControls são carregados por CDN.

Não há instalação nem servidor: é só abrir o arquivo.

## Como jogar

1. Clique em **Embaralhar** e aguarde o cubo terminar de girar.
2. Gire as faces pelos botões do painel ou pelo teclado até deixar cada face de uma cor só.
3. Ao resolver, aparece a mensagem de vitória com o total de movimentos e o tempo.
4. Clique em **Reiniciar** para voltar ao cubo resolvido e começar de novo.

## Controles

| Ação | Como fazer |
|---|---|
| Girar uma face | Botões **C, B, F, A, E, D** do painel, ou as mesmas teclas no teclado |
| Girar no sentido inverso | **Shift** + tecla, ou **Shift** + clique no botão |
| Embaralhar | Botão **Embaralhar** (20 movimentos aleatórios, animação rápida) |
| Reiniciar | Botão **Reiniciar** |
| Trocar o tema de cores | Botões de **Tema** no painel |
| Girar a câmera | Arrastar com o mouse (ou com o dedo no celular) |
| Zoom da câmera | Roda do mouse |
| Aumentar / diminuir o cubo | **Page Up** / **Page Down** |

Teclas das faces:

| Tecla | Face |
|---|---|
| **C** | Cima |
| **B** | Baixo |
| **F** | Frente |
| **A** | Atrás |
| **E** | Esquerda |
| **D** | Direita |

Sem o Shift, o giro é no sentido horário visto de fora do cubo.

## Temas de cores

O cubo tem 5 paletas, que podem ser trocadas a qualquer momento, inclusive com o cubo embaralhado (as peças não mudam de lugar, só as cores):

- **Clássico**
- **Neon**
- **Pastel**
- **Daltônico** (paleta Okabe-Ito, pensada para ser distinguível por quem tem daltonismo)
- **Retrô**

A escolha fica salva no navegador e é lembrada ao recarregar a página.

## Funcionalidades

- Cubo com 27 cubinhos, cores por face e contorno escuro nas arestas.
- Câmera com OrbitControls: órbita com suavização (damping), zoom com limites mínimo e máximo e vista diagonal inicial.
- Rotação animada e suave de qualquer face, nos dois sentidos, com fila de movimentos (nunca há dois giros ao mesmo tempo).
- 5 temas de cores com troca em tempo real e escolha salva no navegador.
- Painel de controles com botões das faces, embaralhar, reiniciar, seletor de tema, contador e cronômetro.
- Atalhos de teclado em português e resumo dos atalhos no painel.
- Contador de movimentos em tempo real, contando só os giros do jogador (os do embaralhar não contam).
- Embaralhar com sequência aleatória que nunca repete a mesma face em seguida, e controles bloqueados enquanto embaralha.
- Verificação de cubo resolvido, considerando posição e orientação de cada cubinho.
- Detecção de vitória com mensagem colorida mostrando movimentos e tempo.
- Cronômetro que começa no primeiro movimento do jogador e para na vitória.
- Layout responsivo: painel na lateral esquerda no computador e no topo em telas pequenas, com o enquadramento da câmera ajustado ao tamanho da tela.

## Estrutura do código

O arquivo `cubo-magico.html` é dividido em seções, cada uma com um responsável:

| Seção | Conteúdo | Responsável |
|---|---|---|
| 1 | Cena, câmera, renderer, OrbitControls, enquadramento responsivo e loop de animação | Bento |
| 2 | Cubo (27 cubinhos), arestas, paletas de tema e seletor de tema | Bento |
| 3 | Rotação das faces, fila de movimentos e animação | João |
| 4 | Painel, controles, contador, embaralhar, vitória, reiniciar e cronômetro | Lorenna |

Hierarquia 3D: `globalGroup` guarda os 27 cubinhos. Durante um giro, os 9 cubinhos da face entram num grupo temporário, que gira e depois devolve as peças ao `globalGroup`, atualizando a posição lógica de cada uma.

Cada cubinho guarda também a sua posição de origem, que nunca muda. É ela que permite repintar o cubo ao trocar de tema sem errar as cores, mesmo depois de embaralhar.

## Teste de validação

Com o cubo resolvido e parado, abra o Console do navegador (F12) e rode:

```js
validarMovimentos()
```

A função confere os giros de todas as faces nos dois sentidos, o sentido horário correto, sequências misturadas e a coerência entre posição lógica e visual. Para checar se o cubo está resolvido, use `cuboResolvido()`. Para trocar o tema pelo console, use `aplicarTema('neon')`.

## Divisão do grupo

- **Bento:** cena, câmera, renderer, controles de câmera, cubo, cores, temas e responsividade.
- **João:** rotação das faces, fila de movimentos e animação.
- **Lorenna:** interface, jogo (contador, embaralhar, vitória, reiniciar, cronômetro) e documentação.

## Tecnologias

- HTML, CSS e JavaScript
- [Three.js](https://threejs.org/) r128 e OrbitControls (via CDN)
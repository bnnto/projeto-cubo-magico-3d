# Cubo Mágico 3D

Cubo mágico 3x3x3 interativo feito com **Three.js**, em um único arquivo HTML (`cubo-magico.html`). Projeto em grupo da faculdade.

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
| Girar uma face | Botões **U, D, F, B, L, R** do painel, ou as teclas U, D, F, B, L, R |
| Girar no sentido inverso | **Shift** + tecla, ou **Shift** + clique no botão |
| Embaralhar | Botão **Embaralhar** (20 movimentos aleatórios, animação rápida) |
| Reiniciar | Botão **Reiniciar** |
| Girar a câmera | Arrastar com o mouse |
| Zoom da câmera | Roda do mouse |
| Aumentar / diminuir o cubo | **Page Up** / **Page Down** |

Notação das faces: **U** (Up, superior), **D** (Down, inferior), **F** (Front, frontal), **B** (Back, traseira), **L** (Left, esquerda) e **R** (Right, direita). Sem o Shift, o giro é no sentido horário visto de fora do cubo.

## Funcionalidades

- Cubo com 27 cubinhos, cores por face e contorno escuro nas arestas.
- Rotação animada e suave de qualquer face, nos dois sentidos, com fila de movimentos (nunca há dois giros ao mesmo tempo).
- Painel de controles com botões das faces, embaralhar, reiniciar, contador e cronômetro.
- Atalhos de teclado e resumo dos atalhos no painel.
- Contador de movimentos em tempo real, contando só os giros do jogador (os do embaralhar não contam).
- Embaralhar com sequência aleatória que nunca repete a mesma face em seguida, e controles bloqueados enquanto embaralha.
- Verificação de cubo resolvido, considerando posição e orientação de cada cubinho.
- Detecção de vitória com mensagem colorida mostrando movimentos e tempo.
- Cronômetro que começa no primeiro movimento do jogador e para na vitória.

## Estrutura do código

O arquivo `cubo-magico.html` é dividido em seções, cada uma com um responsável:

| Seção | Conteúdo | Responsável |
|---|---|---|
| 1 | Cena, câmera, renderer, OrbitControls e loop de animação | Bento |
| 2 | Cubo (27 cubinhos), cores e paletas de tema | Bento |
| 3 | Rotação das faces, fila de movimentos e animação | João |
| 4 | Painel, controles, contador, embaralhar, vitória, reiniciar e cronômetro | Lorenna |

Hierarquia 3D: `globalGroup` guarda os 27 cubinhos. Durante um giro, os 9 cubinhos da face entram num grupo temporário, que gira e depois devolve as peças ao `globalGroup`, atualizando a posição lógica de cada uma.

## Teste de validação

Com o cubo resolvido e parado, abra o Console do navegador (F12) e rode:

```js
validarMovimentos()
```

A função confere os giros de todas as faces nos dois sentidos, o sentido horário correto, sequências misturadas e a coerência entre posição lógica e visual. Para checar se o cubo está resolvido, use `cuboResolvido()`.

## Divisão do grupo

- **Bento:** cena, câmera, renderer, controles de câmera, cubo, cores e temas.
- **João:** rotação das faces, fila de movimentos e animação.
- **Lorenna:** interface, jogo (contador, embaralhar, vitória, reiniciar, cronômetro) e documentação.

## Tecnologias

- HTML, CSS e JavaScript
- [Three.js](https://threejs.org/) r128 e OrbitControls (via CDN)
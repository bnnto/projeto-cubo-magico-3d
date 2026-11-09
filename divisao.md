# Divisão de Commits – Projeto Cubo Mágico 3D (Three.js)

Grupo de 3 pessoas, **10 commits por integrante** (30 no total).
Entrega em **um único arquivo `.html`**, usando o `ex2-escopo.html` como base (aproveitando `globalGroup`, grupos locais e o loop de animação).

---

## Visão geral da divisão

| Integrante | Área de responsabilidade | Seção do arquivo |
|---|---|---|
| **Pessoa 1** | Cena, cubo 3x3x3, cores, câmera (OrbitControls) e temas | Seções 1 e 2 |
| **Pessoa 2** | Mecânica de rotação das 6 faces e animação suave | Seção 3 |
| **Pessoa 3** | Interface, embaralhar, contador, vitória e documentação | Seção 4 (+ HTML/CSS do painel) |

**Requisitos cobertos:**
- Mínimos: cubo com 27 cubinhos, rotação de ≥ 2 faces, animação suave, OrbitControls, cores corretas.
- Extras: 6 faces rotacionáveis, botão embaralhar animado, detecção de vitória, contador de movimentos, temas de cor.

---

## Como evitar conflitos trabalhando no mesmo arquivo

Como os três editam o mesmo `.html`, o **primeiro commit da Pessoa 1** deixa o arquivo organizado em blocos bem separados por comentários (no mesmo estilo dos blocos `=====` do exemplo do professor). Cada pessoa mexe apenas no seu bloco:

| Bloco | Conteúdo | Dono |
|---|---|---|
| Seção 1 | Cena, câmera, renderer, loop de animação | Pessoa 1 |
| Seção 2 | Cubo (27 cubinhos), cores e temas | Pessoa 1 |
| Seção 3 | Rotação das faces e animação das camadas | Pessoa 2 |
| Seção 4 | Controles, contador, embaralhar, vitória | Pessoa 3 |
| HTML/CSS do painel | Botões, textos e estilo da interface | Pessoa 3 (Pessoa 1 só no seletor de tema) |

Regras de Git (sugestão):
- Uma branch por pessoa (`pessoa1-cubo`, `pessoa2-rotacao`, `pessoa3-jogo`).
- Fazer `pull` da `main` antes de cada commit e merge na `main` a cada 2–3 commits.
- Mensagens de commit em português, no formato `tipo: descrição`.
- Um commit = uma mudança pequena e funcional. O arquivo deve abrir sem erros após cada commit.
- Se mexer fora do seu bloco, avisar o grupo antes.

---

## 👤 PESSOA 1 – Cubo, Câmera e Temas

**1. `chore: cria o arquivo base a partir do exemplo e organiza as seções`**
Copiar o `ex2-escopo.html` como ponto de partida. Remover as duas esferas, a linha de referência e os textos do exemplo. Deixar o arquivo dividido em blocos comentados (Seções 1 a 4 e área do painel), para cada integrante saber onde trabalhar.

**2. `feat: configura cena, câmera, renderer e loop de animação`**
Aproveitar os três pilares do exemplo (Scene, Camera, Renderer). Ajustar a posição da câmera para enquadrar o cubo inteiro, manter o tratamento de redimensionamento da janela e o `requestAnimationFrame`. Criar o `globalGroup` que conterá o cubo.

**3. `feat: gera os 27 cubinhos na posição 3x3x3`**
Criar os 27 cubinhos com uma geometria compartilhada (mesma ideia da geometria compartilhada das esferas). Distribuir nas coordenadas -1, 0 e 1 em cada eixo, com um pequeno espaçamento. Guardar todos em uma lista que as outras seções possam usar, com a posição lógica de cada um.

**4. `feat: aplica cores corretas em cada face do cubo`**
Dar a cada cubinho 6 materiais, um por lado. Pintar apenas os lados voltados para fora com as cores clássicas e deixar as faces internas pretas. Conferir que faces opostas têm as cores opostas corretas.

**5. `feat: integra OrbitControls para órbita com o mouse`**
Carregar o `OrbitControls` na mesma versão do Three.js usada no arquivo (via tag `<script>` de CDN). Ativar órbita, zoom e suavização do movimento (damping), atualizando os controles dentro do loop de animação. Limitar a distância mínima e máxima do zoom.

**6. `style: adiciona arestas escuras e ajusta visual do cubo`**
Melhorar a aparência: contorno escuro entre os cubinhos para o cubo parecer um Rubik de verdade, ajuste do fundo da cena e do enquadramento inicial. Aproveitar a escala global do exemplo (Page Up/Page Down) para aumentar e diminuir o cubo, se o grupo achar útil.

**7. `feat: cria paletas de cores para os temas`**
Definir pelo menos 3 paletas: clássico, escuro/neon e pastel. Cada tema define a cor de cada uma das 6 faces. O cubo passa a ler as cores do tema ativo em vez de ter cores fixas.

**8. `feat: permite trocar o tema em tempo real`**
Implementar a função que aplica um tema ao cubo já existente, trocando as cores dos materiais sem recriar os cubinhos nem perder a posição atual das peças.

**9. `feat: adiciona seletor de tema na interface`**
Colocar na página um seletor (lista ou botões) para escolher o tema. Salvar a escolha no navegador para ela ser lembrada ao recarregar. Alinhar o visual com o painel da Pessoa 3.

**10. `fix: ajustes finais de responsividade e revisão visual`**
Revisar tela cheia, redimensionamento e telas menores. Corrigir detalhes visuais encontrados nos testes do grupo, conferir se todos os temas mantêm as cores distinguíveis e comentar o código das suas seções no estilo do exemplo.

---

## 👤 PESSOA 2 – Mecânica de Rotação e Animação

**1. `feat: define as 6 faces e seleciona os cubinhos de cada camada`**
Mapear as faces (Superior, Inferior, Frontal, Traseira, Esquerda, Direita) com seu eixo de rotação e a camada correspondente. Criar a função que devolve quais cubinhos pertencem a uma face, com base na posição deles.

**2. `feat: cria grupo temporário por face (anexar e ancorar)`**
Seguindo a dica do projeto: ao girar, colocar os cubinhos da face dentro de um `THREE.Group`, girar o grupo e, ao terminar, devolver os cubinhos para a cena. Usar a mesma lógica de hierarquia de grupos do exemplo do professor.

**3. `feat: rotação da face superior (sem animação)`**
Implementar o giro de 90° da face superior de forma instantânea para validar a mecânica. Ao final, arredondar posições e rotações dos cubinhos para evitar erros acumulados.

**4. `feat: rotação da face frontal`**
Reaproveitar a mesma mecânica para a face frontal. Com isso, o requisito mínimo de **2 faces rotacionáveis** fica atendido.

**5. `feat: animação suave com interpolação do ângulo`**
Fazer o ângulo variar gradualmente ao longo de um tempo definido, dentro do loop de animação, com suavização no início e no fim (easing). Ao chegar em 90°, finalizar e reancorar as peças.

**6. `feat: bloqueia giros simultâneos e cria fila de movimentos`**
Impedir que uma nova rotação comece enquanto outra está em andamento. Criar uma fila para guardar movimentos pedidos durante a animação e executá-los em sequência (importante para o embaralhar da Pessoa 3).

**7. `feat: adiciona rotação das faces inferior e esquerda`**
Reaproveitar a mecânica já validada para as duas faces, conferindo o sentido de giro de cada uma.

**8. `feat: adiciona rotação das faces traseira e direita`**
Com isso, as **6 faces** ficam rotacionáveis. Conferir o sentido horário de cada face visto de fora do cubo.

**9. `feat: suporta sentido horário e anti-horário`**
Permitir girar cada face nos dois sentidos. Deixar uma função simples e comentada (ex.: "girar face X no sentido Y") para a Pessoa 3 ligar aos botões e ao teclado, além de uma opção de velocidade da animação para o embaralhar ser mais rápido.

**10. `fix: corrige precisão numérica e valida os movimentos`**
Testar cada face: 4 giros seguidos devem devolver o cubo ao estado original; um giro e o inverso devem se anular. Corrigir qualquer desalinhamento de peças e comentar o código da sua seção.

---

## 👤 PESSOA 3 – Interface, Jogo e Documentação

**1. `feat: cria painel de controles na interface`**
Montar o painel em HTML/CSS dentro do próprio arquivo, inspirado nas caixas de informação do exemplo (`#info` e `#labels`). Incluir botões para as 6 faces, botão de embaralhar e área para contador e mensagens.

**2. `feat: liga botões e teclado às rotações`**
Conectar cada botão e cada tecla (ex.: U, D, F, B, L, R, com Shift para o sentido inverso) à função de rotação da Pessoa 2, usando o mesmo estilo de listener de teclado do exemplo. Mostrar no painel um resumo dos atalhos.

**3. `feat: contador de movimentos`**
Contar cada giro realizado e exibir na tela, atualizando em tempo real. Considerar movimento apenas quando o giro é efetivamente executado.

**4. `feat: gera sequência aleatória para embaralhar`**
Criar a lógica que sorteia uma quantidade de movimentos (ex.: 20), evitando repetir a mesma face em sequência para o embaralhamento ser mais eficiente.

**5. `feat: botão embaralhar com animação`**
Executar a sequência sorteada usando a fila de movimentos, com animação mais rápida. Desabilitar os botões durante o embaralhar e não contar esses giros no contador do jogador.

**6. `feat: verifica se o cubo está resolvido`**
Criar a função que confere se cada face possui uma única cor, considerando a posição e a orientação atuais dos cubinhos.

**7. `feat: detecção de vitória`**
Chamar a verificação após cada movimento do jogador e exibir mensagem de vitória com o total de movimentos. Garantir que a mensagem não apareça no início do jogo nem logo após o embaralhar.

**8. `feat: botão reiniciar cubo`**
Permitir voltar o cubo ao estado resolvido, zerar o contador e esconder a mensagem de vitória.

**9. `feat: efeito visual de comemoração e cronômetro`**
Adicionar um efeito simples ao vencer (ex.: cubo girando sozinho ou mudança de cor da mensagem) e um cronômetro que começa no primeiro movimento e para na vitória. Se o grupo preferir manter só os extras da lista do professor, este commit pode ser trocado por um de polimento da interface.

**10. `docs: comentários, instruções no arquivo e revisão final`**
Como não haverá README separado, colocar um bloco de comentário no topo do `.html` com descrição, controles, requisitos atendidos e divisão do grupo. Revisar os comentários do código no estilo do exemplo do professor e fazer o teste final completo antes da entrega.

---

## Ordem sugerida para evitar bloqueios

| Etapa | Quem | Commits |
|---|---|---|
| 1 | Pessoa 1 | 1 a 4 (arquivo base, cubo e cores) |
| 2 | Pessoa 2 | 1 a 5 (rotação básica e animação) |
| | Pessoa 1 | 5 a 7 (câmera e temas), em paralelo |
| | Pessoa 3 | 1 e 2 (painel, ligando ao que já existe) |
| 3 | Pessoa 2 | 6 a 10 (fila, 6 faces, sentidos) |
| | Pessoa 3 | 3 a 5 (contador e embaralhar) |
| 4 | Pessoa 3 | 6 a 9 (vitória e extras) |
| | Pessoa 1 | 8 a 10 (temas na interface e revisão) |
| 5 | Todos | Último commit de cada um (revisão e documentação) |

Enquanto uma pessoa espera a outra, ela pode adiantar o que não depende de ninguém (por exemplo: a Pessoa 3 monta o painel visual e a Pessoa 1 prepara as paletas dos temas).
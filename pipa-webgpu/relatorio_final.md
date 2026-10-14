# Relatório de Projeto: Pipa Animada em WebGPU

Este projeto implementa uma cena 2D animada de uma pipa voando, desenvolvida utilizando exclusivamente a API WebGPU e shaders WGSL. A cena atende às restrições propostas pelo professor, visando cumprir todos os critérios de avaliação, utilizando apenas 4 triângulos e transformações matemáticas para animação.

## 1. Estrutura de Arquivos

O projeto foi organizado da seguinte forma:

* **`lib/utils.js` e `lib/webgpu.js`:** Bibliotecas base fornecidas na disciplina. Com as funções matemáticas de matrizes e a abstração do pipeline gráfico do WebGPU.
* **`main.html` e `main.css`:** Estrutura da página e estilização básica do canvas.
* **`kite.vert.js` e `kite.frag.js`:** Código dos shaders escritos em WGSL. O *vertex shader* aplica a matriz de transformação (MVP) aos vértices, e o *fragment shader* renderiza as cores sólidas interpoladas.
* **`main.js`:** Arquivo principal do projeto, contendo a lógica da cena, modelagem, animação e o loop de renderização.

## 2. Principais Funções e Lógica (`main.js`)

A classe `Scene` gerencia a matemática e os objetos da aplicação. Suas principais funções são:

* **`createTriangle(pontos, cor, gpu)`:** Responsável por instanciar os 4 triângulos permitidos na cena (2 formando a pipa e 2 formando as fitas da cauda), gerando seus respectivos *vertex* e *uniform buffers*.
* **`createModelMatrices()`:** Calcula a animação baseada no tempo (`t`). Implementa a subida/descida com rotação leve para o corpo da pipa, e aplica transformações hierárquicas para a cauda (a fita 1 herda da pipa, e a fita 2 herda da fita 1, adicionando oscilações mais rápidas para simular o vento).
* **`createViewMatrix()`:** Configura a câmera (`lookAt`). Calcula o acompanhamento parcial (40%) do movimento vertical da pipa, mantendo a percepção de deslocamento sem que o objeto saia da tela.
* **`createProjectionMatrix()`:** Define o ambiente 2D com uma projeção ortográfica (`createOrthographicMat4`), ajustada à proporção do canvas (900x600).
* **`draw(gpu)`:** Função executada continuamente via `requestAnimationFrame`. Multiplica as matrizes (`Projeção * Visão * Modelo`), atualiza os buffers da GPU e desenha as primitivas na tela.

## 3. Divisão de Tarefas da Equipe

Para garantir que o trabalho fluísse de forma eficiente e equilibrada, dividimos a implementação em três partes integradas:

* **João Lucas Pontes (Modelagem e Shaders):** 
  Ficou responsável pela modelagem geométrica (coordenadas locais dos 4 triângulos, pontos de pivô), escolha das cores sólidas e pela comunicação do JavaScript com os *Shaders* (WGSL), garantindo a correta passagem de variáveis para a GPU.
* **Pedro Henrique Vargas (Cinemática e Transformações):** 
  Cuidou da lógica matemática da matriz de Modelo (`createModelMatrices`). Implementou o uso do seno para o balanço contínuo e construiu a hierarquia de transformações, fazendo com que o balanço orgânico das fitas da cauda seguisse perfeitamente o corpo da pipa.
* **Pedro do Amaral Rangel (Câmera, Projeção e Loop):** 
  Desenvolveu a matriz de Visão (`createViewMatrix`), garantindo que a câmera seguisse 40% do movimento da pipa, ajustou a Matriz de Projeção Ortográfica para não haver distorções geométricas e estruturou o *render loop* para manter os 60 FPS da animação.
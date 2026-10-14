🪁 Pipa Animada em WebGPU

Este repositório contém a entrega do Trabalho 1 da disciplina de Computação Gráfica (2026.2). O projeto consiste em uma animação 2D de uma pipa voando, desenvolvida inteiramente com a API gráfica WebGPU e shaders escritos em WGSL.

📌 Sobre o Projeto

O objetivo do trabalho foi implementar uma pipeline gráfica do zero, respeitando severas restrições geométricas e estruturais para demonstrar o domínio sobre transformações matemáticas (matrizes).

Principais características e restrições atendidas:

Uso exclusivo de WebGPU nativo (sem bibliotecas de renderização externas como Three.js).

Limite estrito de apenas 4 triângulos na cena.

Animação contínua via requestAnimationFrame (a cauda herda o movimento da pipa e adiciona seu próprio balanço orgânico).

Implementação de Matrizes de Modelagem, Visão (Câmera acompanhando o eixo Y parcialmente) e Projeção Ortográfica.

🚀 Como executar o projeto

Devido às políticas de segurança dos navegadores (CORS) e ao uso de módulos ES6 em JavaScript, o projeto não funcionará se o arquivo HTML for aberto com um duplo clique direto do sistema operacional. É necessário rodar um servidor local.

Pré-requisitos

Um navegador compatível com WebGPU (Google Chrome ou Microsoft Edge na versão 113 ou superior).

Visual Studio Code (VS Code).

Extensão Live Server instalada no VS Code.

Passo a passo

Clone este repositório para a sua máquina:

git clone https://github.com/jotaele777/Trabalho1CG_2026.2.git


Abra a pasta do projeto no VS Code.

Navegue até o arquivo pipa/main.html.

Clique no botão "Go Live" no canto inferior direito do VS Code.

O navegador padrão abrirá automaticamente exibindo a animação (ex: http://127.0.0.1:5500).

📄 Relatórios

Para entender a fundo a matemática aplicada, a divisão da modelagem e o fluxo de trabalho da equipe, consulte os nossos relatórios:

relatorio_final.md

👥 Equipe de Desenvolvimento

* **João Lucas Pontes (Modelagem e Shaders):** 
  Ficou responsável pela modelagem geométrica (coordenadas locais dos 4 triângulos, pontos de pivô), escolha das cores sólidas e pela comunicação do JavaScript
  com os *Shaders* (WGSL), garantindo a correta passagem de variáveis para a GPU.
* **Pedro Henrique Vargas (Cinemática e Transformações):** 
  Cuidou da lógica matemática da matriz de Modelo (`createModelMatrices`). Implementou o uso do seno para o balanço contínuo e construiu a hierarquia de transformações,
  fazendo com que o balanço orgânico das fitas da cauda seguisse perfeitamente o corpo da pipa.
* **Pedro do Amaral Rangel (Câmera, Projeção e Loop):** 
  Desenvolveu a matriz de Visão (`createViewMatrix`), garantindo que a câmera seguisse 40% do movimento da pipa, ajustou a Matriz de Projeção Ortográfica para não haver distorções
  geométricas e estruturou o *render loop* para manter os 60 FPS da animação.

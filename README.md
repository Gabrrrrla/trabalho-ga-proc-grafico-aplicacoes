# Trabalho Prático – Grau A: Leitor e Visualizador de Cenas 3D com OpenGL Moderna

Este repositório contém a implementação do trabalho prático de Grau A da disciplina **Processamento Gráfico: Computação Gráfica e Aplicações – 2026/1**, desenvolvido na Unisinos.

O objetivo do projeto é carregar e visualizar cenas 3D utilizando **OpenGL Moderna**, aplicando conceitos do pipeline gráfico programável, carregamento de geometria complexa, câmera sintética, transformações geométricas e iluminação pelo modelo de **Phong**.

## 👩‍💻 Integrantes

- Gabriela Bley Rodrigues
- Luisa Becker dos Santos

---

## 📌 Funcionalidades Implementadas

O projeto implementa um visualizador 3D com os seguintes recursos:

- Leitura de modelos 3D no formato `.obj` utilizando **Assimp**.
- Recuperação de atributos de geometria:
  - posições dos vértices;
  - normais;
  - coordenadas de textura;
  - faces trianguladas.
- Criação e uso de **VAO**, **VBO** e **EBO** para envio dos dados para a GPU.
- Exibição simultânea de múltiplos objetos na cena.
- Seleção de objeto via teclado.
- Transformações geométricas no objeto selecionado:
  - translação em X, Y e Z;
  - rotação em X, Y e Z;
  - escala uniforme;
  - escala individual por eixo.
- Câmera sintética em primeira pessoa, com controle por teclado e mouse.
- Alternância entre projeção perspectiva e ortográfica.
- Iluminação de Phong nos shaders:
  - componente ambiente;
  - componente difusa;
  - componente especular.
- Fonte de luz pontual configurável e movimentável pelo teclado.
- Representação visual da fonte de luz na cena.
- Propriedades de material configuráveis no código (`ka`, `kd`, `ks` e `shininess`).
- Alternância entre modo sólido e wireframe sobreposto.
- Grid de chão como funcionalidade extra.
- Otimização dos buffers do grid e da fonte de luz: os VAOs/VBOs são criados uma única vez na inicialização.

---

## 📂 Estrutura do Repositório

```plaintext
trabalho-ga-proc-grafico-aplicacoes/
├── assets/
│   └── Modelos3D/
│       ├── Cube.obj
│       └── SuzanneSubdiv1.obj
├── common/
│   └── glad.c
├── include/
│   └── glad/
│       ├── glad.h
│       └── KHR/
│           └── khrplatform.h
├── src/
│   └── TrabalhoGA_Gabi_Luisa/
│       ├── main.cpp
│       ├── Camera.cpp
│       └── Camera.h
├── CMakeLists.txt
└── README.md
```

> O diretório `build/` é gerado pelo CMake e não precisa ser versionado.

---

## 🧱 Principais Arquivos

### `src/TrabalhoGA_Gabi_Luisa/main.cpp`

Arquivo principal do projeto. Ele concentra:

- inicialização da janela com GLFW;
- inicialização da GLAD;
- criação e compilação dos shaders;
- carregamento dos modelos 3D com Assimp;
- extração de vértices, normais, coordenadas de textura e índices;
- criação das malhas com VAO, VBO e EBO;
- renderização dos objetos da cena;
- aplicação da iluminação de Phong;
- controle dos modos de projeção;
- controle de seleção e transformação dos objetos;
- movimentação da fonte de luz pontual;
- desenho do grid de chão;
- desenho da representação visual da fonte de luz;
- renderização opcional de wireframe sobreposto à geometria sólida.

### `src/TrabalhoGA_Gabi_Luisa/Camera.h` e `Camera.cpp`

Implementam a câmera sintética em primeira pessoa. A câmera possui:

- posição;
- vetores `front`, `right` e `up`;
- ângulos de Euler `yaw` e `pitch`;
- movimentação por teclado;
- rotação por mouse;
- geração da matriz de visualização com `glm::lookAt`.

A câmera inicia posicionada em:

```cpp
Camera camera(glm::vec3(0.0f, 2.0f, 6.0f));
```

E utiliza direção inicial baseada no eixo `-Z`, com `yaw` padrão igual a `-90.0f`.

### `CMakeLists.txt`

Configura o projeto com CMake, define o padrão **C++17**, baixa dependências com `FetchContent` e gera o executável:

```plaintext
TrabalhoGA_Gabi_Luisa
```

As dependências baixadas automaticamente pelo CMake são:

- GLFW;
- GLM;
- stb_image;
- Assimp.

A GLAD deve estar presente manualmente no repositório, conforme explicado abaixo.

---

## ⚙️ Requisitos

Antes de compilar, instale:

- **CMake 3.10** ou superior;
- compilador C++ com suporte a **C++17**;
- **Git**, pois o CMake usa `FetchContent` para baixar dependências;
- drivers de vídeo com suporte a OpenGL;
- no Windows, recomenda-se **MSYS2 UCRT64** com GCC.

---

## ⚠️ Importante: GLAD

O projeto espera encontrar os arquivos da GLAD nestes caminhos:

```plaintext
common/glad.c
include/glad/glad.h
include/glad/KHR/khrplatform.h
```

Caso esses arquivos não existam, a compilação será interrompida com erro no CMake.

Se for necessário gerar novamente a GLAD:

1. Acesse o **GLAD Generator**.
2. Use a seguinte configuração:
   - **API:** OpenGL;
   - **Version:** 4.5 ou compatível com a versão usada nos shaders;
   - **Profile:** Core;
   - **Language:** C/C++.
3. Copie os arquivos gerados para:
   - `glad.c` → `common/glad.c`;
   - `glad.h` → `include/glad/glad.h`;
   - `khrplatform.h` → `include/glad/KHR/khrplatform.h`.

---

## 🚀 Como Clonar o Repositório

```bash
git clone https://github.com/Gabrrrrla/trabalho-ga-proc-grafico-aplicacoes.git
cd trabalho-ga-proc-grafico-aplicacoes
```

---

## 🛠️ Como Compilar pelo Terminal

Execute os comandos abaixo na raiz do repositório:

```bash
cmake -S . -B build
cmake --build build
```

O CMake irá:

1. configurar o projeto;
2. baixar as dependências externas;
3. compilar a aplicação;
4. gerar o executável dentro da pasta `build/`.

A primeira compilação pode demorar mais, pois o Assimp, GLFW, GLM e stb são obtidos pelo `FetchContent`.

---

## ▶️ Como Executar

Como os modelos são carregados usando caminhos relativos a partir da pasta `build/`, execute o programa **de dentro do diretório `build`**.

### Windows PowerShell ou CMD

```bash
cd build
.\TrabalhoGA_Gabi_Luisa.exe
```

### Linux ou macOS

```bash
cd build
./TrabalhoGA_Gabi_Luisa
```

Se a execução for feita a partir da raiz do projeto, os caminhos dos modelos podem não ser encontrados, pois o código carrega os arquivos com caminhos relativos como:

```cpp
../assets/Modelos3D/SuzanneSubdiv1.obj
../assets/Modelos3D/Cube.obj
```

---

## 🧭 Como Compilar e Executar pelo VS Code

1. Abra o VS Code.
2. Vá em **File → Open Folder** ou **Arquivo → Abrir Pasta**.
3. Selecione a pasta raiz do repositório.
4. Instale as extensões:
   - **CMake Tools**;
   - **C/C++**.
5. Pressione `Ctrl + Shift + P`.
6. Execute `CMake: Scan for Kits`.
7. Execute `CMake: Select a Kit`.
8. Selecione o compilador adequado, por exemplo:
   - `GCC for MSYS2 UCRT64`, no Windows;
   - GCC ou Clang, no Linux/macOS.
9. Execute `CMake: Configure`.
10. Execute `CMake: Build`.
11. Abra um terminal na pasta `build/`.
12. Execute o programa:

No Windows:

```bash
.\TrabalhoGA_Gabi_Luisa.exe
```

No Linux/macOS:

```bash
./TrabalhoGA_Gabi_Luisa
```

---

## 🎮 Controles da Aplicação

### Câmera FPS

| Tecla/ação | Função |
|---|---|
| `W` | Move a câmera para frente |
| `S` | Move a câmera para trás |
| `A` | Move a câmera para a esquerda |
| `D` | Move a câmera para a direita |
| Mouse | Controla a direção da câmera |
| `ESC` | Fecha a aplicação |

### Visualização

| Tecla | Função |
|---|---|
| `P` | Alterna entre projeção perspectiva e ortográfica |
| `M` | Liga/desliga o modo wireframe sobreposto |
| `TAB` | Alterna o objeto selecionado |

### Transformações do Objeto Selecionado

| Tecla | Função |
|---|---|
| `←` | Move o objeto no eixo X negativo |
| `→` | Move o objeto no eixo X positivo |
| `↑` | Move o objeto no eixo Y positivo |
| `↓` | Move o objeto no eixo Y negativo |
| `I` | Move o objeto no eixo Z negativo |
| `K` | Move o objeto no eixo Z positivo |
| `R + X` | Rotaciona o objeto no eixo X |
| `R + Y` | Rotaciona o objeto no eixo Y |
| `R + Z` | Rotaciona o objeto no eixo Z |
| `=` ou `+` | Aumenta a escala uniforme |
| `-` | Diminui a escala uniforme |
| `T + X` | Aumenta a escala no eixo X |
| `T + Y` | Aumenta a escala no eixo Y |
| `T + Z` | Aumenta a escala no eixo Z |

> Observação: a escala por eixo foi implementada para aumento individual em cada eixo. Para redução, há o controle de escala uniforme com `-`.

### Movimentação da Fonte de Luz

| Tecla | Função |
|---|---|
| `U` | Move a luz no eixo X negativo |
| `O` | Move a luz no eixo X positivo |
| `J` | Move a luz no eixo Y negativo |
| `L` | Move a luz no eixo Y positivo |
| `N` | Move a luz no eixo Z negativo |
| `B` | Move a luz no eixo Z positivo |

> A tecla `B` é usada para mover a luz no eixo Z positivo porque `M` já é utilizada para ativar/desativar o wireframe.

---

## 💡 Iluminação e Materiais

A iluminação é calculada no fragment shader pelo modelo de Phong, combinando:

```glsl
ambient + diffuse + specular
```

A posição da luz pontual é definida e atualizada pela variável global:

```cpp
glm::vec3 pointLightPos(0.0f, 5.0f, 2.0f);
```

A luz pode ser movida em tempo de execução com as teclas `U`, `O`, `J`, `L`, `N` e `B`. A posição atual da luz é enviada ao shader por meio do uniform:

```cpp
lightPos
```

Cada objeto possui propriedades de material:

```cpp
glm::vec3 ka;       // refletância ambiente
glm::vec3 kd;       // refletância difusa
glm::vec3 ks;       // refletância especular
float shininess;    // expoente especular
```

Exemplo de alteração da cor difusa de um objeto:

```cpp
suzanne.kd = glm::vec3(1.0f, 0.5f, 0.31f);
cube.kd = glm::vec3(0.2f, 0.6f, 0.8f);
```

---

## 📦 Modelos 3D Carregados

Atualmente, a cena carrega dois modelos:

```cpp
Mesh suzanne("../assets/Modelos3D/SuzanneSubdiv1.obj");
Mesh cube("../assets/Modelos3D/Cube.obj");
```

Os dois objetos são inseridos no vetor:

```cpp
std::vector<Mesh> sceneObjects;
```

A seleção alterna entre os objetos desse vetor usando `TAB`.

Para trocar ou adicionar modelos:

1. Adicione o arquivo `.obj` dentro de `assets/Modelos3D/`.
2. No `main.cpp`, crie uma nova instância de `Mesh`:

```cpp
Mesh novoObjeto("../assets/Modelos3D/NomeDoModelo.obj");
novoObjeto.position = glm::vec3(0.0f, 1.0f, 0.0f);
novoObjeto.kd = glm::vec3(0.8f, 0.8f, 0.8f);
sceneObjects.push_back(novoObjeto);
```

3. Recompile o projeto:

```bash
cmake --build build
```

---

## 🧩 Fluxo de Dados entre CPU e GPU

O fluxo principal do programa é:

1. O **Assimp** lê o arquivo `.obj`.
2. O programa percorre os nós da cena importada.
3. Cada malha é processada para extrair:
   - posições;
   - normais;
   - coordenadas de textura;
   - índices das faces.
4. Os dados são armazenados em uma estrutura `Vertex`.
5. Os vértices são enviados para um **VBO**.
6. Os índices são enviados para um **EBO**.
7. O **VAO** registra o layout dos atributos:
   - `location = 0` → posição;
   - `location = 1` → normal;
   - `location = 2` → coordenada de textura.
8. A cada frame, a aplicação envia as matrizes `model`, `view` e `projection` para os shaders.
9. O vertex shader calcula a posição final dos vértices.
10. O fragment shader calcula a iluminação de Phong.

---

## 🧪 Exemplo de Uso

1. Compile o projeto:

```bash
cmake -S . -B build
cmake --build build
```

2. Execute a aplicação:

```bash
cd build
./TrabalhoGA_Gabi_Luisa
```

No Windows:

```bash
cd build
.\TrabalhoGA_Gabi_Luisa.exe
```

3. Use `W`, `A`, `S`, `D` e o mouse para navegar pela cena.
4. Pressione `TAB` para selecionar outro objeto.
5. Use as setas, `I` e `K` para mover o objeto selecionado.
6. Use `R + X`, `R + Y` ou `R + Z` para rotacionar o objeto.
7. Use `+` e `-` para alterar a escala uniforme.
8. Use `T + X`, `T + Y` ou `T + Z` para aumentar a escala em um eixo específico.
9. Use `U`, `O`, `J`, `L`, `N` e `B` para movimentar a luz pontual.
10. Pressione `P` para alternar a projeção.
11. Pressione `M` para ativar/desativar o wireframe.
12. Pressione `ESC` para sair.

---

## ✅ Relação com os Requisitos do Trabalho

| Requisito | Situação no projeto |
|---|---|
| Leitura de `.obj` ou `.ply` | Implementado com Assimp para `.obj` |
| Vértices, faces, normais e coordenadas de textura | Implementado |
| Faces trianguladas | Implementado com `aiProcess_Triangulate` |
| VAO e VBO | Implementado |
| EBO | Implementado |
| Múltiplos objetos | Implementado com Suzanne e Cube |
| Seleção via teclado | Implementado com `TAB` |
| Translação X/Y/Z | Implementado |
| Rotação X/Y/Z | Implementado |
| Escala uniforme | Implementado com `+`/`-` |
| Escala por eixo | Implementado com `T + X/Y/Z` para aumento individual |
| Câmera FPS com teclado e mouse | Implementado |
| Projeção perspectiva/ortográfica | Implementado com `P` |
| Phong nos shaders | Implementado |
| Luz pontual | Implementado |
| Luz configurável | Implementado por movimentação via teclado |
| Material `ka`, `kd`, `ks` | Configurável no código |
| Sólido e wireframe sobreposto | Implementado com `M` |
| Grid de chão | Implementado |
| Eixos da cena | Não implementado explicitamente nesta versão |

---

## ⚠️ Observações para Avaliação

- O programa deve ser executado a partir da pasta `build/` para que os caminhos relativos dos modelos funcionem corretamente.
- A GLAD precisa estar nos diretórios esperados antes da configuração do CMake.
- A primeira compilação pode demorar, pois o CMake baixa e compila dependências externas.
- O shader declara coordenadas de textura em `location = 2`; elas são carregadas pelo parser, mas ainda não são usadas para aplicar textura nesta etapa.
- A fonte de luz pode ser movida durante a execução, permitindo demonstrar a variação da iluminação de Phong sobre os objetos.
- O grid e a representação visual da luz usam buffers próprios criados na inicialização, evitando recriar VAO/VBO a cada frame.

Para demonstrar domínio técnico, é importante compreender o fluxo:

1. o Assimp lê o arquivo `.obj`;
2. os dados são convertidos para a estrutura `Vertex`;
3. os vértices e índices são enviados para VBO/EBO;
4. o VAO registra o layout dos atributos;
5. os shaders recebem as matrizes `model`, `view` e `projection`;
6. o fragment shader calcula a iluminação de Phong;
7. a câmera altera a matriz `view` conforme teclado e mouse;
8. a luz pontual altera o resultado visual da iluminação conforme sua posição muda.

---

## 🧯 Possíveis Problemas e Soluções

### Erro: `Arquivo glad.c não encontrado`

Verifique se existe o arquivo:

```plaintext
common/glad.c
```

E também:

```plaintext
include/glad/glad.h
include/glad/KHR/khrplatform.h
```

### Os modelos não aparecem

Execute o programa de dentro da pasta `build/`:

```bash
cd build
./TrabalhoGA_Gabi_Luisa
```

ou, no Windows:

```bash
cd build
.\TrabalhoGA_Gabi_Luisa.exe
```

### Dependências não baixam

Verifique se o Git está instalado e acessível no terminal:

```bash
git --version
```

### Tela abre, mas a câmera parece travada

A aplicação captura o mouse para simular uma câmera FPS. Movimente o mouse e use `W`, `A`, `S`, `D` para navegar. Use `ESC` para fechar.

### O wireframe fica muito sobreposto ao objeto sólido

O projeto usa `glPolygonOffset` ao desenhar os objetos sólidos antes do wireframe. Mesmo assim, dependendo da GPU ou do driver, pode haver pequenas variações visuais. Use `M` para ligar/desligar o modo wireframe durante a apresentação.

---

## 📚 Bibliotecas Utilizadas

- **OpenGL**: API gráfica utilizada para renderização.
- **GLFW**: criação da janela e captura de entrada de teclado/mouse.
- **GLAD**: carregamento das funções modernas da OpenGL.
- **GLM**: operações de álgebra linear, matrizes e vetores.
- **Assimp**: importação de modelos 3D.
- **stb_image**: biblioteca incluída para suporte futuro a imagens/texturas.

---

## 📄 Licença e Uso Acadêmico

Este projeto foi desenvolvido exclusivamente para fins acadêmicos, como parte da disciplina **Processamento Gráfico: Computação Gráfica e Aplicações** da Unisinos.

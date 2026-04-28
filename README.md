# Trabalho Prático – Grau A: Leitor e Visualizador de Cenas 3D com OpenGL Moderna

Este repositório contém a implementação do trabalho prático de Grau A da disciplina **Processamento Gráfico: Computação Gráfica e Aplicações – 2026/1**, desenvolvido na Unisinos.

O objetivo do projeto é carregar e visualizar cenas 3D utilizando **OpenGL Moderna**, aplicando conceitos do pipeline gráfico programável, carregamento de geometria complexa, câmera sintética e iluminação pelo modelo de **Phong**.

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
  - escala uniforme.
- Câmera sintética em primeira pessoa, com controle por teclado e mouse.
- Alternância entre projeção perspectiva e ortográfica.
- Iluminação de Phong nos shaders:
  - componente ambiente;
  - componente difusa;
  - componente especular.
- Fonte de luz pontual na cena.
- Propriedades de material configuráveis no código (`ka`, `kd`, `ks` e `shininess`).
- Alternância entre modo sólido e wireframe sobreposto.
- Grid de chão como funcionalidade extra.
- Representação visual da posição da fonte de luz.

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
- criação das malhas com VAO, VBO e EBO;
- renderização dos objetos;
- aplicação da iluminação de Phong;
- controle dos modos de projeção;
- controle de seleção e transformação dos objetos;
- desenho do grid e da fonte de luz.

### `src/TrabalhoGA_Gabi_Luisa/Camera.h` e `Camera.cpp`

Implementam a câmera sintética em primeira pessoa. A câmera possui:

- posição;
- vetores `front`, `right` e `up`;
- ângulos de Euler `yaw` e `pitch`;
- movimentação por teclado;
- rotação por mouse;
- geração da matriz de visualização com `glm::lookAt`.

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

1. Acesse o GLAD Generator.
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
11. Abra um terminal na pasta `build/` e rode o executável.

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

---

## 💡 Iluminação e Materiais

A iluminação é calculada no fragment shader pelo modelo de Phong, combinando:

```glsl
ambient + diffuse + specular
```

A posição da luz pontual é definida no código pela variável:

```cpp
glm::vec3 pointLightPos(0.0f, 5.0f, 2.0f);
```

Cada objeto possui propriedades de material:

```cpp
glm::vec3 ka; // refletância ambiente
glm::vec3 kd; // refletância difusa
glm::vec3 ks; // refletância especular
float shininess; // expoente especular
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

Para trocar ou adicionar modelos:

1. Adicione o arquivo `.obj` dentro de `assets/Modelos3D/`.
2. No `main.cpp`, crie uma nova instância de `Mesh`:

```cpp
Mesh novoObjeto("../assets/Modelos3D/NomeDoModelo.obj");
novoObjeto.position = glm::vec3(0.0f, 1.0f, 0.0f);
sceneObjects.push_back(novoObjeto);
```

3. Recompile o projeto:

```bash
cmake --build build
```

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
7. Use `+` e `-` para alterar a escala.
8. Pressione `P` para alternar a projeção.
9. Pressione `M` para ativar/desativar o wireframe.
10. Pressione `ESC` para sair.

---

## ✅ Relação com os Requisitos do Trabalho

| Requisito | Situação no projeto |
|---|---|
| Leitura de `.obj` ou `.ply` | Implementado com Assimp para `.obj` |
| Vértices, faces, normais e coordenadas de textura | Implementado |
| VAO e VBO | Implementado |
| EBO | Implementado |
| Múltiplos objetos | Implementado com Suzanne e Cube |
| Seleção via teclado | Implementado com `TAB` |
| Translação X/Y/Z | Implementado |
| Rotação X/Y/Z | Implementado |
| Escala uniforme | Implementado |
| Escala por eixo | Não possui atalho dedicado nesta versão |
| Câmera FPS com teclado e mouse | Implementado |
| Projeção perspectiva/ortográfica | Implementado com `P` |
| Phong nos shaders | Implementado |
| Luz pontual | Implementado |
| Material `ka`, `kd`, `ks` | Configurável no código |
| Sólido e wireframe sobreposto | Implementado com `M` |
| Grid de chão | Implementado |
| Eixos da cena | Não implementado explicitamente nesta versão |

---

## ⚠️ Observações para Avaliação

- O programa deve ser executado a partir da pasta `build/` para que os caminhos relativos dos modelos funcionem corretamente.
- A GLAD precisa estar nos diretórios esperados antes da configuração do CMake.
- A primeira compilação pode demorar, pois o CMake baixa e compila dependências externas.
- Para demonstrar domínio técnico, é importante compreender o fluxo:
  1. o Assimp lê o arquivo `.obj`;
  2. os dados são convertidos para a estrutura `Vertex`;
  3. os vértices e índices são enviados para VBO/EBO;
  4. o VAO registra o layout dos atributos;
  5. os shaders recebem as matrizes `model`, `view` e `projection`;
  6. o fragment shader calcula a iluminação de Phong;
  7. a câmera altera a matriz `view` conforme teclado e mouse.

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

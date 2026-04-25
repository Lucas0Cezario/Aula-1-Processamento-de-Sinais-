# Processamento Digital de Sinais — Lista de Exercícios

Repositório com a resolução dos exercícios práticos da disciplina de **Processamento Digital de Sinais (PDS)**, implementados em Python sobre Jupyter Notebooks executáveis no Google Colab. Cada aula aborda um conjunto temático específico, contemplando geração de gráficos no domínio do tempo e da frequência, manipulação de áudio (`.wav`), análise espectral, projeto de filtros digitais e compressão de sinais.

**Autor:** Caio e Lucas
**Linguagem:** Python 3 (Jupyter Notebook / Google Colab)

---

## Sumário

- [Visão Geral](#visão-geral)
- [Estrutura do Repositório](#estrutura-do-repositório)
- [Requisitos](#requisitos)
- [Recursos Externos](#recursos-externos)
- [Como Executar](#como-executar)
- [Detalhamento das Aulas](#detalhamento-das-aulas)
  - [Aula 1 — Sinais no Domínio do Tempo](#aula-1--sinais-no-domínio-do-tempo)
  - [Aula 2 — Análise Espectral e Amostragem](#aula-2--análise-espectral-e-amostragem)
  - [Aula 3 — Sistemas LTI, Polos e Zeros, Filtros Digitais](#aula-3--sistemas-lti-polos-e-zeros-filtros-digitais)
  - [Aula 4 — DFT, DCT e Compressão de Sinais](#aula-4--dft-dct-e-compressão-de-sinais)
- [Arquivos de Áudio e Imagem Utilizados](#arquivos-de-áudio-e-imagem-utilizados)
- [Observações](#observações)

---

## Visão Geral

Este repositório consolida quatro listas de exercícios que percorrem, de forma incremental, os principais conceitos do Processamento Digital de Sinais:

| Aula   | Tema Central                                      | Foco Prático                                  |
| ------ | ------------------------------------------------- | --------------------------------------------- |
| Aula 1 | Sinais no tempo, chirps, convolução acústica      | Geração e audição de sinais; reverberação     |
| Aula 2 | FFT, Teorema de Nyquist, decimação e interpolação | Análise espectral; aliasing e *imaging*       |
| Aula 3 | Sistemas LTI, polos e zeros, filtros IIR/FIR      | Projeto de filtros e recuperação de sinais    |
| Aula 4 | DFT, DTFT e DCT                                   | Resolução espectral e compressão (1D e 2D)    |

Cada notebook contém o **enunciado da questão**, **código comentado**, **gráficos gerados** e a **discussão dos resultados** em células de texto markdown.

---

## Estrutura do Repositório

```
.
├── README.md
├── Aula_1_v2.ipynb     # Sinais no domínio do tempo
├── Aula_2_v2.ipynb     # Análise espectral e amostragem
├── Aula_3_v2.ipynb     # Sistemas LTI e filtros digitais
└── Aula_4_v2.ipynb     # DFT, DCT e compressão
```

---

## Requisitos

Os notebooks foram desenvolvidos para o **Google Colab**, mas podem ser executados localmente com Jupyter. As principais bibliotecas utilizadas são:

```bash
pip install numpy scipy matplotlib opencv-python ipython
```

Bibliotecas e módulos por aula:

- **NumPy** — operações vetoriais e geração de sinais
- **SciPy** — `scipy.signal` (chirp, lfilter, freqz, tf2zpk, resample), `scipy.io.wavfile` (leitura de áudio), `scipy.fft` / `scipy.fftpack` (FFT e DCT)
- **Matplotlib** — visualização de sinais, espectros e diagramas de polos e zeros
- **IPython.display.Audio** — reprodução de áudio dentro do notebook
- **OpenCV (`cv2`)** — leitura e processamento da imagem na Aula 4

---

## Recursos Externos

Os arquivos de áudio (`.wav`) e a imagem (`.jpg`) utilizados ao longo das aulas, bem como a função auxiliar `calculate_spectrum()`, são disponibilizados pelo repositório oficial da disciplina:

- **Repositório base:** [rafaelschaves/gele7317-proc-sin](https://github.com/rafaelschaves/gele7317-proc-sin)
- **Função `calculate_spectrum()`:** [calculate_spectrum.ipynb](https://github.com/rafaelschaves/gele7317-proc-sin/blob/master/calculate_spectrum.ipynb)

A função `calculate_spectrum()` é amplamente referenciada nos enunciados das Aulas 2 e 3 e deve ser carregada/copiada antes da execução das células que dela dependem.

---

## Como Executar

**Opção 1 — Google Colab (recomendado):**
Cada notebook possui um *badge* "Open in Colab" no topo. Basta clicar e executar célula a célula. Os arquivos `.wav` e `.jpg` (obtidos no [repositório base](https://github.com/rafaelschaves/gele7317-proc-sin)) devem ser carregados no ambiente do Colab via *upload* manual ou montagem do Google Drive antes de executar as células que os utilizam.

**Opção 2 — Execução local:**

```bash
git clone <url-do-repositório>
cd <pasta-do-repositório>
jupyter notebook
```

Garanta que os arquivos de mídia (`handel.wav`, `h_banheiro.wav`, `sinal_taca.wav`, `sosias.jpg`) e o `calculate_spectrum.ipynb` estejam no mesmo diretório dos notebooks ou ajuste os caminhos no código.

---

## Detalhamento das Aulas

### Aula 1 — Sinais no Domínio do Tempo

Introdução prática à geração, visualização e audição de sinais discretos. Exploração inicial da convolução como modelagem de ambientes acústicos.

| Questão | Tópico                                                                                                                                                |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1**   | Sinal cossenoidal $x(t) = \cos(2\pi f t)$ para $f \in \{500, 5000, 10000\}$ Hz com $f_s = 44{,}1$ kHz — gráfico no tempo e reprodução de áudio        |
| **2**   | *Chirps* com varreduras de frequência **linear**, **quadrática** e **logarítmica** ($f_0 = 500$ Hz, $f_1 = 10$ kHz)                                   |
| **3**   | Leitura do `handel.wav`, reprodução nas taxas $f_s$, $2f_s$ e $4f_s$, e análise do efeito sonoro                                                      |
| **4**   | Discussão teórica do procedimento de medição da **resposta ao impulso (RIR)** de uma sala                                                             |
| **5**   | Análise temporal de `h_banheiro.wav` e `sinal_taca.wav` (duração, decaimento e reverberação)                                                          |
| **6**   | **Convolução** do `handel.wav` e do som da taça com a resposta ao impulso do banheiro — simulação de propagação acústica                              |

---

### Aula 2 — Análise Espectral e Amostragem

Aprofundamento no domínio da frequência via FFT, com foco no **Teorema de Amostragem de Nyquist–Shannon**, *aliasing* e *imaging* espectral. Faz uso intensivo da função `calculate_spectrum()` (ver [Recursos Externos](#recursos-externos)).

| Questão | Tópico                                                                                                       |
| ------- | ------------------------------------------------------------------------------------------------------------ |
| **1**   | Espectro de $x(t) = \cos(2\pi f t)$ para $f \in \{500, 5000, 10000, 50000\}$ Hz — observação do **aliasing** |
| **2**   | Espectro de chirps lineares, quadráticos e logarítmicos                                                      |
| **3**   | Espectro do sinal `handel.wav` — análise do conteúdo harmônico                                               |
| **4**   | **Subamostragem (downsampling)** manual de $y[n] = x[nM]$ para diferentes fatores $M$                        |
| **5**   | Comparação da subamostragem manual com `scipy.signal.resample()` (com filtragem anti-*aliasing*)             |
| **6**   | **Sobreamostragem (upsampling)** por *zero-stuffing* e o fenômeno de **imageamento espectral**               |
| **7**   | Comparação da sobreamostragem manual com `scipy.signal.resample()` (interpolação correta)                    |
| **8**   | Sinal $x(t) = \cos(2000\pi t) + \sin(5000\pi t)$ amostrado em diferentes $f_s$ (incluindo Nyquist crítico)   |
| **9**   | Espectros comparados de `h_banheiro.wav` e `sinal_taca.wav`                                                  |
| **10**  | Análise espectral da convolução de `handel.wav` e do som da taça com a RIR do banheiro                       |

---

### Aula 3 — Sistemas LTI, Polos e Zeros, Filtros Digitais

Projeto e análise de sistemas LTI no domínio Z, incluindo filtros inversos, *comb filters* e aproximações FIR.

| Questão | Tópico                                                                                                                                                                                                          |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1**   | Análise de $H(z) = 1 + 0,49\,z^{-2} + 0,2401\,z^{-6} - 0,0576\,z^{-8} - 0,0282\,z^{-10} - 0,0138\,z^{-12}$ — resposta em frequência e diagrama de polos e zeros                                                 |
| **2**   | Aplicação de $H(z)$ ao sinal `handel.wav` e análise do espectro filtrado                                                                                                                                        |
| **3**   | Projeto do **filtro inverso $G(z) = 1/H(z)$** para recuperação do sinal — análise de estabilidade                                                                                                               |
| **4**   | **Comb filter** $H(z) = \dfrac{1 - z^{-L}}{1 - a z^{-L}}$ para $a \in \{0,7;\ 0,9\}$ e $L \in \{1, 4, 10\}$                                                                                                     |
| **5**   | Aplicação do *comb filter* ao `handel.wav` — visualização das atenuações nas frequências dos zeros                                                                                                              |
| **6**   | Filtros de recuperação para os sistemas da Q4 — análise da estabilidade marginal (zeros sobre o círculo unitário)                                                                                               |
| **7**   | **Aproximações FIR** dos filtros IIR das Q3 e Q6 — relação ordem do filtro × MSE do sinal recuperado                                                                                                            |

---

### Aula 4 — DFT, DCT e Compressão de Sinais

Estudo da Transformada Discreta de Fourier e da Transformada Discreta de Cossenos com aplicação em compressão de áudio (1D) e imagens (2D).

| Questão | Tópico                                                                                                                                                                |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1**   | Comparação **DFT × DTFT** para o sinal $x[n] = \delta[n] - \delta[n-1] + \delta[n-2] - \delta[n-3]$ com $N \in \{4, 16, 64, 1024\}$                                   |
| **2**   | **Resolução da DFT** e **zero-padding**: distinção entre senoides próximas (1,0 Hz e 1,1 Hz) com diferentes tamanhos de DFT                                           |
| **3**   | **Compressão 1D do `handel.wav`** com DFT e DCT, para fatores de energia $r$ ∈ {99,5%; 99,0%; 90,0%; 75,0%; 50,0%} — comparação de MSE                                |
| **4**   | **DCT 2D** aplicada à imagem `sosias.jpg` — análise de compactação de energia                                                                                         |
| **5**   | **Compressão por blocos $L \times L$** (esquema JPEG) com $L \in \{8, 16, 32, 64\}$ e diferentes taxas de retenção                                                    |

---

## Arquivos de Áudio e Imagem Utilizados

Todos os arquivos abaixo estão disponíveis no repositório base da disciplina: [rafaelschaves/gele7317-proc-sin](https://github.com/rafaelschaves/gele7317-proc-sin).

| Arquivo            | Descrição                                                                          |
| ------------------ | ---------------------------------------------------------------------------------- |
| `handel.wav`       | Trecho do *Hallelujah Chorus* de Händel — sinal musical de referência              |
| `h_banheiro.wav`   | Resposta ao impulso (RIR) medida em um banheiro — usada para simulação acústica    |
| `sinal_taca.wav`   | Som de uma taça de cristal — sinal com forte componente tonal e decaimento longo   |
| `sosias.jpg`       | Imagem em tons de cinza utilizada nas análises 2D com DCT                          |

---

## Observações

- Todas as discussões e análises dos resultados estão escritas em **células markdown** dentro dos notebooks, logo após o código correspondente.
- Os notebooks utilizam **MathJax/LaTeX** para a notação matemática. Para melhor visualização, recomenda-se abri-los no Jupyter ou no Google Colab.
- Cada exercício é autocontido e pode ser executado de forma independente dos demais, desde que os recursos externos (`calculate_spectrum.ipynb` e arquivos de mídia) estejam disponíveis.

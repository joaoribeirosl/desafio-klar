# Desafio

O desafio consiste em utilizar algoritmos de inteligência artificial para executar a remoção de ruído de imagens de baixa dosagem de tomografia computadorizada.

## Link para a base de dados  
[CT Low Dose Reconstruction - Kaggle](https://www.kaggle.com/datasets/andrewmvd/ct-low-dose-reconstruction)

## Atividades
- Remoção do ruído utilizando rede não generativa;
- Remoção do ruído utilizando rede generativa;
- Apresentação dos resultados e do processo de treinamento;
- Utilização preferencial de arquivos no formato DICOM (.dcm, .IMA).

Se possível, todo o processo de codificação deve ser realizado em um único notebook.
<br><br>
# Remoção de Ruído em Imagens de Tomografia Computadorizada de Baixa Dosagem

Este projeto tem como objetivo aplicar técnicas de inteligência artificial para remover o ruído presente em imagens de tomografia computadorizada obtidas com baixa dosagem de radiação. Foram implementadas duas abordagens principais:

- **Rede Neural Não Generativa**: Utilizando um autoencoder para a remoção de ruído.
- **Rede Neural Generativa**: Aplicando uma Rede Adversária Generativa (GAN) para a melhoria da qualidade das imagens.

## Base de Dados

As imagens utilizadas neste projeto foram obtidas do conjunto de dados disponível no Kaggle:

- [CT Low Dose Reconstruction Dataset](https://www.kaggle.com/datasets/andrewmvd/ct-low-dose-reconstruction)

Este dataset contém imagens de tomografia computadorizada em diferentes dosagens de radiação.

Na pasta `Original Data`, você encontrará duas subpastas:

- **Quarter Dose**: Contém imagens com a dose reduzida de radiação, que são usadas como entrada para o processo de remoção de ruído.
- **Full Dose**: Contém imagens com a dose completa, usadas como referência para o modelo.

Essas imagens estão no formato DICOM (.dcm, .IMA), que são processadas para a tarefa de denoising.



## Pré-processamento das Imagens

As imagens no formato DICOM (.dcm, .IMA) foram carregadas e redimensionadas para 128x128 pixels. As etapas de pré-processamento incluíram:

- Leitura dos arquivos DICOM.
- Redimensionamento das imagens.
- Normalização dos valores de pixel para o intervalo [0, 1].
- Expansão das dimensões para adequação aos modelos de rede neural.

## Remoção de Ruído com Rede Neural Não Generativa

Foi desenvolvido um autoencoder convolucional com a seguinte arquitetura:

- **Encoder**:
  - Camada Conv2D com 32 filtros e função de ativação ReLU.
  - Camada de MaxPooling2D.
  - Camada Conv2D com 64 filtros e função de ativação ReLU.
  - Camada de MaxPooling2D.

- **Decoder**:
  - Camada Conv2D com 64 filtros e função de ativação ReLU.
  - Camada de UpSampling2D.
  - Camada Conv2D com 32 filtros e função de ativação ReLU.
  - Camada de UpSampling2D.
  - Camada Conv2D final com 1 filtro e função de ativação sigmoid.

O modelo foi compilado com o otimizador Adam e função de perda de erro quadrático médio (MSE). Foi treinado por 10 épocas com batch size de 8.


## Remoção de Ruído com Rede Neural Generativa

Foi implementada uma Rede Adversária Generativa (GAN) composta por:

- **Generator**:
  - Múltiplas camadas Conv2D e Conv2DTranspose com funções de ativação LeakyReLU.
  - Camadas de BatchNormalization para estabilização do treinamento.

- **Discriminator**:
  - Camadas Conv2D com funções de ativação LeakyReLU.
  - Camadas de BatchNormalization.
  - Camada Dense final com ativação sigmoid para classificação de validade.

O discriminador foi compilado com função de perda binária cruzada e otimizador Adam. O GAN foi treinado por 10 épocas com batch size de 32.


## Avaliação dos Resultados

A qualidade das imagens denoised foi avaliada utilizando o índice de similaridade estrutural (SSIM). Os resultados demonstraram uma melhoria significativa na qualidade das imagens após a aplicação dos modelos de remoção de ruído.

## Conclusão

Este projeto demonstrou duas abordagens para remoção de ruído em imagens de tomografia computadorizada:

✅ O Autoencoder é mais rápido e estável.

✅ A GAN pode gerar imagens de maior qualidade, mas exige mais dados e treino.



## Requisitos

- Python 3.10
- Bibliotecas:
  - pydicom
  - numpy
  - tensorflow
  - opencv-python
  - scikit-image
  - matplotlib

## Como Executar

1. Clone este repositório:

   ```bash
   git clone https://github.com/joaoribeirosl/desafio-klar.git

2. instale as dependências 
    ```py
    pip install numpy tensorflow pydicom opencv-python matplotlib scikit-image


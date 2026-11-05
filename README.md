# Controlador de Jogo de Corrida por Webcam

Controle um jogo de corrida com as mãos, sem teclado: a webcam rastreia as duas mãos em tempo real e converte gestos em comandos de teclado. Desenvolvido e testado com **Need for Speed Heat**.

Projeto individual da disciplina de **Visão Computacional** (Engenharia de Computação, UERJ), 2023.

## Como funciona

1. O **MediaPipe Hands** detecta até duas mãos e devolve 21 pontos de referência (landmarks) de cada uma.
2. O **OpenCV** captura os frames da webcam e desenha os pontos e as linhas usadas na decisão.
3. A distância (em pixels) entre pares de pontos dos dedos, e o ângulo da linha entre as duas mãos, viram teclas simuladas com a biblioteca `keyboard`.

| Gesto | Tecla | Como é detectado |
|---|---|---|
| Direção (esquerda/direita) | `A` / `D` | Ângulo da linha que liga o ponto 13 das duas mãos, como um volante. Quanto maior a inclinação, mais tempo a tecla fica pressionada (0,1 s a 0,3 s) |
| Acelerar | `W` | Distância entre polegar e indicador de uma das mãos |
| Frear | `Espaço` | Distância entre polegar e indicador da outra mão |
| Ré | `S` | Distância entre a ponta do indicador e a articulação do dedo médio |
| Nitro | `Ctrl` | Mesma medida, na outra mão |

Os pontos usados estão ilustrados em [`posição dos dedos mediapipe.jpg`](./posição%20dos%20dedos%20mediapipe.jpg).

## Tecnologias

Python · OpenCV · MediaPipe · keyboard

## Como executar

```bash
pip install opencv-python mediapipe keyboard
python trabalho_04.py
```

1. Abra o Need for Speed Heat (ou outro jogo de corrida) com os controles mapeados para `W`, `A`, `S`, `D`, `Espaço` e `Ctrl`.
2. Execute o script e posicione as duas mãos na frente da webcam.
3. Pressione `q` na janela da webcam para encerrar.

> A biblioteca `keyboard` pode exigir permissão de administrador no Linux e no macOS.

## Limitações conhecidas

- Os limiares de distância (55 px) e de ângulo estão fixos no código e dependem da distância da mão até a câmera.
- A direção usa pausas curtas (`time.sleep`), o que reduz a taxa de quadros durante as curvas.
- Funciona apenas quando as duas mãos estão visíveis ao mesmo tempo.

## Próximos passos

- **Otimização de desempenho** (planejado): reduzir a latência e aumentar a taxa de quadros do rastreamento e do envio de comandos, para deixar a resposta dos gestos mais fluida durante o jogo.
- Calibração dos limiares de distância e ângulo por usuário.

## Autor

Gustavo Dias de Oliveira · [LinkedIn](https://www.linkedin.com/in/gusdiaso/)

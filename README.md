<p align="center">
  <img src="helpher-logo.png" alt="HelpHer" width="320">
</p>

Reconhecimento automático do Gesto Universal de Ajuda (*Signal for Help*)
em vídeo, voltado a centrais de monitoramento.

## Contexto

O Gesto Universal de Ajuda é um sinal silencioso criado pela Canadian
Women's Foundation para que uma vítima de violência possa pedir socorro
sem falar. Sua eficácia depende de alguém reconhecer o gesto, o que
limita seu alcance em ambientes monitorados por câmera.

O HelpHer investiga o reconhecimento automático desse gesto e o
encaminhamento do alerta a um operador humano, que permanece como etapa
final de verificação.

## Estrutura do projeto

O sistema é dividido em dois módulos, desenvolvidos em paralelo:

| Módulo | Responsabilidade |
|---|---|
| Percepção | Detecta e rastreia pessoas e mãos em vídeo, extraindo 21 landmarks por mão a cada quadro |
| Decisão | Classifica a evolução temporal dessas sequências e aciona o alerta |

Este repositório contém o módulo de decisão.

## Abordagem

O gesto é dinâmico: a mão se abre, o polegar se dobra sobre a palma e os
demais dedos se fecham sobre ele. Reconhecê-lo exige modelar a ordem dos
quadros, e não apenas a configuração da mão em um instante.

- Segmentação em janelas deslizantes de 45 quadros a 30 fps
- Normalização espacial relativa ao punho, invariante a escala e posição
- Classificação por rede recorrente com memória (LSTM)
- Comparação com um classificador de referência não recorrente, para
  medir o ganho da modelagem temporal
- Avaliação por janela e por evento em vídeo contínuo, incluindo taxa de
  falsos positivos por hora
- Acionamento do alerta por MQTT e WebSocket

## Tecnologias

Python, TensorFlow, Keras, MediaPipe, scikit-learn, MQTT (Eclipse
Mosquitto), WebSocket.

## Status

Em desenvolvimento. Projeto de Iniciação Científica do
Instituto Federal de São Paulo, Campus Jacareí.

## Aviso

Este é um projeto de pesquisa acadêmica, sem validação para uso
operacional. O sistema é concebido como ferramenta de apoio, com
verificação humana obrigatória antes de qualquer resposta.

## Licença

(a definir)

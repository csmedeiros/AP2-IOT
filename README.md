# Documentação do Projeto Jumping Jacks Counter

## Introdução
Bem-vindo à documentação do projeto Jumping Jacks Counter. Este aplicativo móvel foi desenvolvido para contar o número de polichinelos realizados pelo usuário, utilizando o PoseLandmarker do MediaPipe.

## Tecnologias Utilizadas
- MediaPipe (PoseLandMarker)
- Kotlin

## Como Utilizar o Aplicativo
1. Abra o aplicativo em seu dispositivo móvel.
2. Conceda permissão para acessar a câmera.
3. Posicione-se de maneira que seu corpo esteja totalmente visível na câmera.
4. Comece a fazer polichinelos e o aplicativo contará automaticamente o número de repetições.

## Funcionalidades Principais
- **Contagem Automática:** O aplicativo conta automaticamente o número de polichinelos realizados.
- **Feedback Visual:** Exibe a pose do usuário em tempo real na tela.

## Mudanças Realizadas do Documento Padrão
Para detectar a execução de um polichinelo, capturamos os pontos dos landmarks 17, 18 (mindinho esquerdo e direito), 0 (nariz), 29, 30 (calcanhar esquerdo e direito) para detectar uma mudança de estado.

```kotlin
if (landmark[17].y() < landmark[0].y() && 
    landmark[18].y() < landmark[0].y() && 
    (landmark[17].x() - landmark[18].x()) < 0.5 && 
    (landmark[29].x() - landmark[30].x()) > 0.1) {
        
    //println("O homem está fazendo polichinelo")
    if (state == 0) {
        resultado++
        c.text = resultado.toString()
    }
    state = 1
    //println(state)

} else {
    state = 0
    //println(state)
}
```
Para atualizarmos o contador, foi criada uma variável compartilhada `c`, que permite ao `OverlayView` ter acesso ao `TextView`.

## Documentação
- [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/guide?hl=pt-br)
- [PoseLandmark](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker?hl=pt-br)

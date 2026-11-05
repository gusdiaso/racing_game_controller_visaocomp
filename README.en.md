🇧🇷 [Português](README.md) | 🇺🇸 English

# Webcam Racing Game Controller

Play a racing game with your hands, no keyboard needed: the webcam tracks both hands in real time and turns gestures into keyboard commands. Built and tested with **Need for Speed Heat**.

Individual project for the **Computer Vision** course (Computer Engineering, UERJ), 2023.

## How it works

1. **MediaPipe Hands** detects up to two hands and returns 21 landmarks per hand.
2. **OpenCV** captures the webcam frames and draws the points and lines used for each decision.
3. The pixel distance between pairs of finger landmarks, and the angle of the line between the two hands, become simulated key presses through the `keyboard` library.

| Gesture | Key | How it is detected |
|---|---|---|
| Steering (left/right) | `A` / `D` | Angle of the line connecting landmark 13 of both hands, like a steering wheel. The larger the tilt, the longer the key is held (0.1 s to 0.3 s) |
| Accelerate | `W` | Distance between thumb and index finger of one hand |
| Brake | `Space` | Distance between thumb and index finger of the other hand |
| Reverse | `S` | Distance between the index fingertip and the middle finger joint |
| Nitro | `Ctrl` | Same measure, on the other hand |

The landmarks used are illustrated in [`posição dos dedos mediapipe.jpg`](./posição%20dos%20dedos%20mediapipe.jpg).

## Tech stack

Python · OpenCV · MediaPipe · keyboard

## How to run

```bash
pip install opencv-python mediapipe keyboard
python trabalho_04.py
```

1. Open Need for Speed Heat (or another racing game) with controls mapped to `W`, `A`, `S`, `D`, `Space` and `Ctrl`.
2. Run the script and place both hands in front of the webcam.
3. Press `q` in the webcam window to quit.

> The `keyboard` library may require administrator permission on Linux and macOS.

## Known limitations

- Distance (55 px) and angle thresholds are hard-coded and depend on how far the hand is from the camera.
- Steering uses short pauses (`time.sleep`), which lowers the frame rate during turns.
- It only works while both hands are visible at the same time.

## Next steps

- **Performance optimization** (planned): reduce latency and increase the frame rate of tracking and command sending, so gesture response feels smoother in game.
- Per-user calibration of distance and angle thresholds.

## Author

Gustavo Dias de Oliveira · [LinkedIn](https://www.linkedin.com/in/gusdiaso/)

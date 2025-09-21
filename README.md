# Raspberry Pi LED Blinker (GPIO)

このプロジェクトは、Raspberry Pi の GPIO ピンを使用して、LED を1秒間隔で点滅させるシンプルな Python スクリプトです。

---

## 🔧 使用ハードウェア

- Raspberry Pi（Pi 4, Pi 400 など GPIO が使えるモデル）
- LED × 1
- 抵抗（220Ω〜330Ω程度）
- ブレッドボード & ジャンパー線

---

## ⚡ 回路図（簡易）

GPIO18 (ピン12) ──→───[抵抗]───→───|>|───→─── GND (ピン6)
（LED）


- GPIO18（BCM番号）を出力ピンとして使用
- LEDと抵抗を直列に接続し、GNDへ

---

## 📜 スクリプト内容（`led_blink.py`）

```python
import RPi.GPIO as GPIO
import time

LED_PIN = 18  # GPIO18 (BCM番号)

GPIO.setmode(GPIO.BCM)         # GPIO番号をBCMで指定
GPIO.setup(LED_PIN, GPIO.OUT)  # GPIO18を出力モードに設定

try:
    while True:
        GPIO.output(LED_PIN, GPIO.HIGH)  # LED ON
        time.sleep(1)                    # 1秒待つ
        GPIO.output(LED_PIN, GPIO.LOW)   # LED OFF
        time.sleep(1)                    # 1秒待つ
except KeyboardInterrupt:
    GPIO.cleanup()  # Ctrl+Cで終了時にGPIOをクリーンアップ


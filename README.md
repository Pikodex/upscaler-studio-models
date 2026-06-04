# upscaler-studio Models

Asset-Repository für vorkonvertierte ONNX-Modelle, die von der
[upscaler-studio](https://github.com/Pikodex/upscaler-studio)-App
bei Bedarf nachgeladen werden.

Hier liegt **kein Code** — nur GitHub-Releases mit `.onnx`-Dateien.

## Releases

| Tag | Inhalt |
|---|---|
| `hat-models-v1` | HAT (Hybrid Attention Transformer, CVPR 2023) — 14 Varianten: HAT-S, HAT, HAT-ImageNet, HAT-L-ImageNet (je 2×/3×/4×), Real-HAT-GAN, Real-HAT-GAN-sharper (je 4×) |

Konvertiert mit `tools/convert_hat_to_onnx.py` aus dem App-Repo,
basierend auf den offiziellen Gewichten von
[XPixelGroup/HAT](https://github.com/XPixelGroup/HAT).

## Lizenz

Die ONNX-Modelle erben die Lizenz der jeweiligen Original-Gewichte
(siehe [XPixelGroup/HAT](https://github.com/XPixelGroup/HAT) für HAT).

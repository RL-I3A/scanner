---
title: Pokemon Card Scanner
emoji: 🎴
colorFrom: blue
colorTo: yellow
sdk: gradio
sdk_version: 4.0.0
app_file: app.py
pinned: false
hardware: t4-small
---

# 🎴 Pokemon Card Scanner

Take a photo of a binder page and find out which Pokémon are in it. This is the recognition engine behind the Binder Scanner on [PokeBinderDex](https://pokebinderdex.com).

## 🔍 How it works

1. **OCR**: [EasyOCR](https://github.com/JaidedAI/EasyOCR) reads every piece of text on the image, in the language you choose.
2. **Size filter**: the name is printed at the same size on every card. The scanner takes the largest text that matches a Pokémon name as a reference, then keeps only the texts of a similar size. Attacks, descriptions and other small print are ignored.
3. **Fuzzy matching**: [RapidFuzz](https://github.com/rapidfuzz/RapidFuzz) compares each candidate with the Pokédex names, which tolerates small OCR mistakes.
4. **Result**: for each Pokémon found, you get its name, a similarity score and the OCR confidence.

## ⚙️ Settings

| Setting | Values | Default |
| --- | --- | --- |
| Language | `en`, `fr`, `es`, `de`, `it` | `en` |
| Similarity threshold | 50 to 95 (%) | 72 |
| Size tolerance | 0.1 to 1.0 | 0.3 |
| Best match only | on / off | off |
| Verbose | on / off | off |

A higher similarity threshold gives fewer false positives but may miss blurry names. A larger size tolerance helps when cards are photographed at different distances.

## 💡 Tips for good results

- Use sharp, well-lit photos.
- Avoid steep angles and reflections on sleeves.
- Make sure the names are visible and readable.
- PNG or JPG work best.

## 🛠️ Tech

Python with Gradio for the interface, EasyOCR and PyTorch for text recognition, OpenCV and Pillow for images and RapidFuzz for name matching. Built to run on a Hugging Face Space with a GPU.

## Project structure

```
.
├── app.py                # Gradio interface
├── pokemon_detector.py   # OCR, size filtering and name matching
├── pokedex.py            # Pokémon names in English, French, German, Spanish and Italian
└── requirements.txt
```

## Related

- [PokeBinderDex.github.io](https://github.com/RL-I3A/PokeBinderDex.github.io): the website that sends binder photos to this app.

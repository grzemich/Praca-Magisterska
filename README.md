# Praca magisterska: Metody oceny i analizy wydajności sieci neuronowych

Repozytorium zawiera kod źródłowy i notatniki Google Colab umożliwiające odtworzenie badań opisanych w pracy magisterskiej pt.:

**„Metody oceny i analizy wydajności sieci neuronowych”**  
Autor: Michał Grześkowiak  
Politechnika Wrocławska, 2025

---

## Zawartość eksperymentów

| Nr | Zakres badania                            | Notebook                                      | Uruchom w Colabie |
|----|--------------------------------------------|-----------------------------------------------|-------------------
| 1  | Benchmark klasyfikatorów CNN               | [`benchmark_cnn.ipynb`](experiments/1_benchmark_cnn/benchmark_cnn.ipynb) | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/grzemich/Praca-Magisterska/blob/main/experiments/1_benchmark_cnn/benchmark_cnn.ipynb) |
| 2  | Detekcja danych spoza rozkładu (OOD)       | [`ood_detection.ipynb`](experiments/2_ood_detection/ood_detection.ipynb) | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/grzemich/Praca-Magisterska/blob/main/experiments/2_ood_detection/ood_detection.ipynb) |
| 3  | Transfer learning (ImageNet → ImageNet-R)  | [`transfer_learning.ipynb`](experiments/3_transfer_learning/transfer_learning.ipynb) | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/grzemich/Praca-Magisterska/blob/main/experiments/3_transfer_learning/transfer_learning.ipynb) |
| 4  | Odporność na zakłócenia (ImageNet-C)       | [`robustness_analysis.ipynb`](experiments/4_robustness/robustness_analysis.ipynb) | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/grzemich/Praca-Magisterska/blob/main/experiments/4_robustness/robustness_analysis.ipynb) |


Każdy notebook zawiera własne zależności (np. `!pip install ...`) i może być uruchomiony bezpośrednio w Google Colaboratory za pomocą przycisku w ostatniej kolumnie, lub pobrany jako plik `.ipynb`.

## Konfiguracja środowiska

Eksperymenty były uruchamiane w środowisku Google Colab z poniższą konfiguracją:

- GPU: NVIDIA Tesla T4
- RAM: 13 GB
- CPU: 2 vCPU (Intel Xeon)
- Batch size: 128
- Epoki: 1 (dla transfer learning)

## Wymagane zbiory danych

### ImageNet v1

- Używany w każdym eksperymencie
- Pobierany automatycznie przez notebook — wymaga pliku `kaggle.json`
  
#### Instrukcja pobrania pliku json:
1. Zaloguj się lub zarejestruj konto na [https://www.kaggle.com](https://www.kaggle.com)
2. Wygeneruj token API (`Account > Create New API Token`)
3. Wykonaj następujące komendy zawarte w każdym notebooku:
```python
from google.colab import files
files.upload()  # Gdy strona poprosi o plik, należy wybrać wygenerowany wcześniej token kaggle.json

!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json
```
### ImageNet-O

- Używany w: OOD detection (2)
- Źródło: https://github.com/hendrycks/natural-adv-examples

### ImageNet-R

- Używany w: transfer learning (3)
- Źródło: https://github.com/hendrycks/imagenet-r

### ImageNet-C

- Używany w: robustness testing (4)
- W badaniach używana była tylko część zbioru, zawarta w archiwum "digital.tar"
- Źródło: https://github.com/hendrycks/robustness

### Uwaga

Zbiory danych nie zostały dołączone do repozytorium ze względu na ograniczenia licencyjne oraz ich duży rozmiar (kilkanaście GB lub więcej).
Użytkownik powinien pobrać je samodzielnie i:
- umieścić je lokalnie w folderze datasets/, lub
- załadować do Google Drive i podłączyć w notebooku za pomocą:
```
from google.colab import drive
drive.mount('/content/drive')
```
Ścieżki do danych można dostosować w notebookach za pomocą zmiennych takich jak data_path.

## Licencja

Kod dostępny na licencji MIT. Zbiory danych pochodzą z zewnętrznych źródeł i podlegają ich własnym warunkom licencyjnym.

## Replikowalność

Wszystkie eksperymenty można uruchomić bezpośrednio w środowisku Google Colab. Każdy notebook zawiera kod instalacyjny, definicje modeli i sposób wczytywania danych. Wyniki mogą minimalnie się różnić w zależności od użytego GPU i dostępnych zasobów.

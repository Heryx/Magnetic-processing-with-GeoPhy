# Magnetic-processing-with-GeoPhy

Workflow in Jupyter Notebook per l'elaborazione di dati magnetometrici (gradiometria, valori in nT) con la libreria **GeophPy** (versione usata nel notebook: 0.32.2).

## Contenuto

```
notebooks/Geomag_elab_grad_nT.ipynb   # workflow completo (output rimossi)
data/raw/                             # dati XYZ di input (non versionati)
outputs/                              # mappe, istogrammi, PDF (non versionati)
requirements.txt
```

## Sequenza di elaborazione

1. Importazione del file ASCII (`.XYZ`, separatore spazio; colonne x, y, z = gradiente; la colonna 4, campo totale, è predisposta ma commentata).
2. `threshold` (−10/+10) e `peakfilt` (mediana, halfwidth 5, soglia 15, modalità assoluta).
3. `destripecon` (additivo, riferimento mediana) e `zeromeanprofile` (mediana).
4. Interpolazione lineare e filtro di Wallis (`wallisfilt`, finestra 9×9).
5. Mappe di correlazione tra profili (`correlation_plotmap`, `correlation_plotsum`) e profili medi cross-track (`meantrack_plot`).
6. Statistiche descrittive (media, mediana, deviazione standard, skewness, curtosi) e istogramma.

Sono presenti, ma commentati, `festoonfilt`, `ploughfilt` e `medianfilt`.

## Uso

1. Creare un ambiente con le dipendenze di `requirements.txt` e installare GeophPy seguendo la documentazione ufficiale della libreria.
2. Copiare il file `.XYZ` in `data/raw/` e impostare `file_path` nella cella 2 del notebook.
3. Eseguire le celle in ordine: i filtri modificano `grad_ds` in place, perciò rieseguire una cella intermedia senza ripartire dall'inizio applica il filtro due volte.

## Note e limiti

- I parametri (soglie, finestre, target del Wallis) sono quelli del caso di studio originale e vanno riadattati a ogni rilievo.
- I titoli delle figure riportano il nome del sito del caso di studio (Rocavecchia).
- Le unità non sono coerenti nel notebook: i file sono nominati in nT, le etichette dell'istogramma indicano nT/m. Da verificare in base allo strumento e al formato di esportazione.
- Il notebook salva i file con nomi fissi nella cartella di lavoro: i file con lo stesso nome vengono sovrascritti.

## Licenza

MIT (vedi `LICENSE`). Verificare la compatibilità con la licenza di GeophPy.

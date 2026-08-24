# Analisi della Politica Monetaria nella Zona Euro

Questo repository contiene un'analisi econometrica delle interazioni tra la politica monetaria e le principali variabili macroeconomiche nell'area euro. Il progetto utilizza modelli per serie storiche multivariate per identificare l'esistenza di una relazione di equilibrio di lungo periodo e per simulare come shock inattesi nei tassi di interesse si trasmettano all'economia reale e ai prezzi.

Per il report completo dell'analisi, consultare il file Analisi politica monetaria dati economici.pdf.

## 📊 Dati Utilizzati

I dati grezzi sono stati estratti dal database FRED (Federal Reserve Economic Data).
*   **Frequenza:** Mensile.
*   **Copertura:** Intera Eurozona.
*   **Variabili:** Tasso di interesse a breve termine (proxy dello strumento di politica monetaria della BCE), Tasso di disoccupazione, Tasso di inflazione. I dati sui prezzi (indice HICP) sono stati trasformati in tasso di inflazione Year-over-Year (YoY) per eliminare la stagionalità.

*Nota: Il dataset è stato diviso in un set di addestramento (fino a Dicembre 2019) e un set di test (2020-2022) per valutare la tenuta del modello a fronte degli shock strutturali post-COVID.*

## 🔬 Metodologia

Il flusso di lavoro analitico è strutturato nei seguenti passaggi:
*   **Analisi Esplorativa:** Ispezione grafica, funzioni di autocorrelazione (ACF) e autocorrelazione parziale (PACF).
*   **Test di Radice Unitaria:** Applicazione del Test Augmented Dickey-Fuller (ADF) in livelli e differenze prime, confermando che le serie sono processi integrati di ordine 1, ovvero I(1).
*   **Test di Cointegrazione di Johansen:** Identificazione di una singola relazione di equilibrio di lungo periodo (r=1) tra le tre variabili.
*   **Modellazione VECM:** Stima di un Vector Error Correction Model (K=2).
*   **Diagnostica e Robustezza:** Valutazione della stabilità tramite le radici del polinomio caratteristico e test sui residui (Portmanteau e Jarque-Bera). La robustezza è stata verificata isolando i sotto-campioni pre-2006 e 2009-2019 per gestire le rotture strutturali della crisi del 2008.
*   **Analisi delle Dinamiche:** Simulazione degli effetti della politica monetaria tramite Funzioni di Impulso-Risposta (IRF) ortogonalizzate e Scomposizione della Varianza dell'Errore (FEVD).
*   **Forecasting:** Confronto delle capacità predittive out-of-sample del modello VECM contro un modello ARIMA univariato come benchmark, validato statisticamente tramite il test di Diebold-Mariano.

## 📈 Risultati Principali

*   **Dinamiche di Lungo Periodo:** Dall'analisi della matrice di caricamento emerge una causalità di lungo periodo che va dai tassi e dalla disoccupazione verso l'inflazione. I tassi di interesse agiscono come guida senza reagire agli scostamenti dall'equilibrio.
*   **Risposta agli Shock:** Le IRF dimostrano che uno shock positivo ai tassi d'interesse produce una contrazione significativa dell'inflazione, con il picco di efficacia raggiunto tra i 4 e i 6 mesi successivi.
*   **Performance Predittiva:** Il test di Diebold-Mariano conferma la superiorità robusta del modello multivariato VECM rispetto all'ARIMA univariato (RMSE e MAE significativamente inferiori).
*   **Limiti Strutturali:** Nonostante la superiorità metodologica, sia il modello VECM stimato sia le proiezioni ufficiali BCE del Dicembre 2019 non sono riuscite a prevedere l'eccezionale impennata inflazionistica del triennio 2020-2022, evidenziando i limiti dei modelli lineari di fronte a shock sistemici senza precedenti.

## 🛠️ Stack Tecnologico

Il progetto è interamente sviluppato in R. Le librerie principali includono:
*   `vars`, `urca`, `dynlm` per la stima econometrica, i test di cointegrazione e di radice unitaria.
*   `tseries`, `forecast` per l'analisi delle serie storiche univariata e il forecasting.
*   `tidyverse`, `lubridate`, `xts` per l'importazione, la pulizia e la manipolazione delle serie temporali.

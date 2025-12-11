README — ML4N Project: SSH Shell Attack Session Classification
Overview

Questo progetto affronta l’analisi automatica di sessioni malevole di shell Unix raccolte tramite honeypot.
L’obiettivo è classificare ogni sessione secondo una o più tattiche MITRE ATT&CK, oltre a esplorare il dataset con tecniche di:

Data exploration

Text preprocessing

Supervised Learning (multi-label classification)

Unsupervised Learning (clustering)

Language Models (BERT o Doc2Vec)

Il dataset contiene circa 230.000 attacchi unici, registrati dopo login SSH.

Dataset

Il dataset (in formato .parquet) contiene 5 colonne:

session_id: ID della sessione

full_session: testo della sessione (comandi eseguiti)

first_timestamp: timestamp di inizio

Set_Fingerprint: insieme delle tattiche associate

... (eventuali metadati aggiuntivi)

Le possibili etichette sono:

Persistence

Discovery

Defense Evasion

Execution

Impact

Other

Harmless

Ogni sessione può avere più etichette → problema multi-label.

Project Structure
Section 1 — Exploration & Preprocessing

Analisi temporale: distribuzione degli attacchi nel tempo

Lunghezza delle sessioni: caratteri, parole

Parole più frequenti

Distribuzione delle tattiche e numero di etichette per sessione

Conversione del testo in vettori:

Bag of Words (BoW)

TF-IDF (term frequency–inverse document frequency)

Section 2 — Multi-Label Classification

Obiettivo: predire le tattiche di una sessione.

Attività richieste:

Split train/test

Preprocessing

Addestramento con almeno due modelli (es. Logistic Regression, Random Forest, SVM, Naive Bayes, MLkNN)

Valutazione:

Confusion matrix

Classification report (per etichetta)

Analisi overfitting/underfitting

Hyperparameter tuning (grid search / randomized search)

Confronto tra rappresentazioni (BoW vs TF-IDF)

Section 3 — Unsupervised Learning (Clustering)

Obiettivo: raggruppare sessioni simili.

Richiede:

Almeno due algoritmi (es. K-Means, Agglomerative, DBSCAN)

Scelta del numero di cluster (Elbow, Silhouette, dendrogrammi…)

Visualizzazione (PCA, t-SNE, UMAP)

Analisi dei cluster:

parole rappresentative (word clouds)

coerenza rispetto alle tattiche

Identificazione di pattern ricorrenti di attacco

Section 4 — Language Models

Obiettivo: classificare usando reti neurali NLP.

Scegli uno tra:

Doc2Vec (training su tutto il corpus)

BERT (pretrained da HuggingFace + fine-tuning)

Passi richiesti:

Pretraining (Doc2Vec) oppure caricamento modello pre-trained (BERT)

Aggiunta di un layer Dense finale

Fine-tuning sul training set

Plot delle learning curves (train/validation)

Early stopping: valutazione del miglior numero di epoche

Requirements
Python 3.x
pandas
numpy
scikit-learn
matplotlib
seaborn
pyarrow
gensim (per Doc2Vec)
transformers (per BERT)
torch / tensorflow (a seconda del modello)
wordcloud


Installazione essenziale:

pip install pandas numpy scikit-learn pyarrow gensim transformers torch wordcloud

How to Run

Scaricare il dataset .parquet

Caricare il progetto Jupyter/Colab/Python

Avviare sequenzialmente le sezioni:

1_exploration.ipynb

2_classification.ipynb

3_clustering.ipynb

4_language_models.ipynb

Salvare i risultati finali nella relazione

Acknowledgments

Dataset fornito da SmartData@PoliTO
Progetto supervisionato da:

Luca Vassio (Politecnico di Torino)

Matteo Boffa
import yfinance as yf
import pandas as pd

def fetch_stock_data(tickers, start_date, end_date):
    """
    Fonction pour récupérer les données historiques des actions spécifiées.

    Args:
    tickers (list): Liste des symboles boursiers des actions à récupérer.
    start_date (str): Date de début au format 'YYYY-MM-DD'.
    end_date (str): Date de fin au format 'YYYY-MM-DD'.

    Returns:
    DataFrame: DataFrame contenant les données historiques des actions.
    """
    # Créer un DataFrame vide pour stocker les données
    stock_data = pd.DataFrame()

    # Récupérer les données historiques pour chaque action
    for ticker in tickers:
        # Récupérer les données historiques depuis Yahoo Finance
        data = yf.download(ticker, start=start_date, end=end_date)
        # Ajouter une colonne avec le symbole boursier pour référence
        data['Ticker'] = ticker
        # Concaténer les données avec le DataFrame principal
        stock_data = pd.concat([stock_data, data])

    return stock_data

# Liste des symboles boursiers des actions à récupérer
tickers = ['AAPL', 'MSFT', 'GOOG', 'AMZN', 'FB']

# Dates de début et de fin pour les données historiques
start_date = '2020-01-01'
end_date = '2024-01-01'

# Récupérer les données historiques des actions spécifiées
stock_data = fetch_stock_data(tickers, start_date, end_date)

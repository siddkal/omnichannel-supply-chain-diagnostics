import pandas as pd
import numpy as np

def run_supply_chain_pipeline(file_path):
    print("🚀 Starting Omni-Channel Supply Chain Data Pipeline...")
    
    # 1. Load Data
    try:
        df = pd.read_csv(file_path)
    except FileNotFoundError:
        df = pd.read_csv('Warehouse_and_Retail_Sales.csv')
        
    # 2. Standardize Schema
    df.columns = df.columns.str.strip().str.upper()
    
    # 3. Handle Missing Values
    df['SUPPLIER'] = df['SUPPLIER'].fillna('UNKNOWN SUPPLIER').str.strip()
    df['ITEM TYPE'] = df['ITEM TYPE'].fillna('UNKNOWN TYPE').str.strip()
    
    df['RETAIL SALES'] = df['RETAIL SALES'].fillna(0.0)
    df['RETAIL TRANSFERS'] = df['RETAIL TRANSFERS'].fillna(0.0)
    df['WAREHOUSE SALES'] = df['WAREHOUSE SALES'].fillna(0.0)
    
    # 4. Feature Engineering: Reverse Logistics Isolation
    df['TRANSACTION_TYPE'] = np.where(df['WAREHOUSE SALES'] >= 0, 'FORWARD_LOGISTICS', 'REVERSE_LOGISTICS')
    df['RETURNS_VOLUME'] = np.where(df['WAREHOUSE SALES'] < 0, abs(df['WAREHOUSE SALES']), 0.0)
    df['NET_WAREHOUSE_SALES'] = np.where(df['WAREHOUSE SALES'] > 0, df['WAREHOUSE SALES'], 0.0)
    
    # 5. Temporal Reconstruction
    df['DATE'] = pd.to_datetime(df['YEAR'].astype(str) + '-' + df['MONTH'].astype(str) + '-01')
    
    # 6. Data Integrity Check
    df = df.drop_duplicates()
    
    print(f"✅ Data processing complete. Cleaned shape: {df.shape}")
    
    # Export cleaned file
    output_path = 'processed_supply_chain_data.csv'
    df.to_csv(output_path, index=False)
    print(f"📦 Processed file exported successfully to: {output_path}")

if __name__ == "__main__":
    run_supply_chain_pipeline('../data/Warehouse_and_Retail_Sales.csv')

# Ex.No: 13 Learning – Use Supervised Learning  
### DATE:  31-10-2025                                                                          
### REGISTER NUMBER : 212223060231
### AIM: 
To develop an AI-based system that predicts maternal health risk levels using clinical parameters and alerts users for timely medical action.

###  Algorithm:
1. **Data Preprocessing:**

   * Load the *Maternal Health Risk Dataset* and separate features (Age, BP, BS, etc.) and target (RiskLevel).
   * Encode categorical target values using `LabelEncoder`.
   * Split data into training and testing sets (80:20).

2. **Model Training:**

   * Initialize the **XGBoost Classifier** (or Decision Tree).
   * Train the model on the training dataset using the feature inputs.

3. **Model Evaluation:**

   * Evaluate accuracy using the test dataset.
   * Analyze feature importance to identify key health indicators.

4. **Model Saving:**

   * Save the trained model and label encoder using `joblib` for future predictions.

5. **Prediction Pipeline:**

   * Load the saved model and encoder.
   * Input a new patient’s health data and predict their risk level (Low, Mid, or High).
   * Display corresponding alert messages based on the predicted risk category.

### Program:

```python
import pandas as pd
from xgboost import XGBClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from joblib import dump, load
import os

file_path = 'Maternal Health Risk Data Set.csv'
output_dir = 'models'
model_filename = os.path.join(output_dir, 'maternal_risk_model_xgb.joblib')

def analyze_model_importance(model, features):
    if not hasattr(model, 'feature_importances_'):
        print("Model does not support feature importance analysis.")
        return
        
    importances = model.feature_importances_
    feature_names = features.columns.tolist()
    
    feature_importance_df = pd.DataFrame({
        'Feature': feature_names,
        'Importance': importances
    }).sort_values(by='Importance', ascending=False)
    
    print("\n--- Model Feature Importance ---")
    print("Top factors influencing Risk Level prediction:")
    print(feature_importance_df.head(5).to_string(index=False))
    print("------------------------------")

def train_and_save_model(use_xgboost=True): 
    try:
        os.makedirs(output_dir, exist_ok=True)
        data = pd.read_csv(file_path)
        print(f"Dataset loaded successfully. Shape: {data.shape}")
    except FileNotFoundError:
        print(f"Error: The file '{file_path}' was not found.")
        return None

    X = data.drop('RiskLevel', axis=1)
    y = data['RiskLevel']
    
    if use_xgboost:
        le = LabelEncoder()
        y_encoded = le.fit_transform(y)
        y = y_encoded
        dump(le, os.path.join(output_dir, 'label_encoder.joblib'))
        print("Target variable encoded and encoder saved.")
        
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

    if use_xgboost:
        model = XGBClassifier(use_label_encoder=False, eval_metric='mlogloss', random_state=42)
        model.fit(X_train, y_train)
        print("\nXGBoost Model trained successfully.")
    else:
        model = DecisionTreeClassifier(random_state=42)
        model.fit(X_train, y_train)
        print("\nDecision Tree Model trained successfully.")

    print(f"Model Accuracy (Test Set): {model.score(X_test, y_test):.4f}")
    analyze_model_importance(model, X)
    dump(model, model_filename)
    print(f"Model saved successfully to: {model_filename}")
    
    return model

def run_prediction_pipeline(loaded_model, use_xgboost=True):
    if loaded_model is None:
        print("Model could not be loaded for testing.")
        return
        
    high_risk_patient_data = pd.DataFrame([{
        'Age': 50,
        'SystolicBP': 150,
        'DiastolicBP': 100,
        'BS': 15.0,
        'BodyTemp': 98.0,
        'HeartRate': 90
    }])

    prediction_code = loaded_model.predict(high_risk_patient_data)[0]

    if use_xgboost:
        le = load(os.path.join(output_dir, 'label_encoder.joblib'))
        prediction = le.inverse_transform([int(prediction_code)])[0]
    else:
        prediction = prediction_code
    
    prediction_label = prediction.upper()
    print()
    print(f"Patient Health Data:\n{high_risk_patient_data.to_string(index=False)}")
    print(f"\nAI PREDICTION: {prediction_label}")
    
    if prediction == 'high risk':
        print("\nCRITICAL ALERT! IMMEDIATE ACTION REQUIRED!")
        print("Your vital signs indicate severe risk factors (Hypertension and/or High Blood Sugar).")
    elif prediction == 'mid risk':
        print("\nMODERATE ALERT! Consult your Doctor soon.")
        print("Your vital signs show elevated risk. Do not ignore these readings.")
    else:
        print("\nLOW RISK DETECTED.")
        print("Your parameters are within a healthy range. Continue monitoring regularly.")
    
if __name__ == "__main__":
    USE_XGBOOST = True 
    trained_model = train_and_save_model(use_xgboost=USE_XGBOOST)
    
    if os.path.exists(model_filename):
        loaded_model = load(model_filename)
        run_prediction_pipeline(loaded_model, use_xgboost=USE_XGBOOST)
    else:
        print("Could not find the saved model file.")

```

### Output:

Terminal Output:
<img width="996" height="544" alt="image" src="https://github.com/user-attachments/assets/2bf00213-d1a7-4dc9-b3d6-07f26550a73e" />


Visual Output:
<img width="794" height="873" alt="image" src="https://github.com/user-attachments/assets/354c0021-2384-49d7-87fe-8b8f855d70ad" />




### Result:
Thus the system was trained successfully and the prediction was carried out.

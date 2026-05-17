# OELP-Through-Wall-Dielectric-Material-Identification


README – final.py (Dielectric Constant
Prediction using Autoencoder + Regressor)
1. Purpose of final.py File
• The final.py file is used to predict the dielectric constant (εr) of unknown materials.
• The prediction is performed using RF S-parameter data generated from CST Studio simulations.
• The system combines Deep Learning and Machine Learning techniques.
• The code uses an Autoencoder model for latent feature extraction.
• A trained regression model is used for final dielectric constant prediction.
2. Main Workflow of the Code
• Read CST magnitude and phase files.
• Extract S-parameter values.
• Create RF feature vectors.
• Normalize RF features using trained scalers.
• Pass RF features through Encoder network.
• Generate latent electromagnetic features.
• Normalize latent features.
• Predict dielectric constant using regressor.
• Display final predicted εr value.
3. Libraries Used
• NumPy → Used for numerical computations and arrays.
• Pandas → Used for dataframe handling.
• re → Used for extracting εr from filename.
• joblib → Used for loading trained models and scalers.
• TensorFlow/Keras → Used for loading autoencoder neural network.
4. Input Files Used
• 20mag.txt → Contains magnitude S-parameter values.
• 20ph.txt → Contains phase S-parameter values.
• The files contain S11, S12, S21 and S22 responses.
• The files are generated using CST Studio simulations.
5. Extracting Dielectric Constant from Filename
• The function extract_er(filepath) is used.
• Regular Expressions are used for extraction.
• Example:
• 20mag.txt → εr = 20
• This value acts as the material label.
6. Reading CST S-Parameter Files
• The function read_cst_multi(filepath) reads CST text files.
• The code detects:
• • S11
• • S12
• • S21
• • S22
• Frequency values are extracted.
• Magnitude and phase values are extracted.
• The extracted data is stored inside Python dictionaries.
7. Dataset Creation
• The code combines magnitude and phase data.
• A Pandas DataFrame is created.
• The DataFrame contains:
• • Frequency
• • S11 Magnitude
• • S11 Phase
• • S12 Magnitude
• • S12 Phase
• • S21 Magnitude
• • S21 Phase
• • S22 Magnitude
• • S22 Phase
• The dataset represents RF electromagnetic behavior.
8. What is an Autoencoder?
• An Autoencoder is a Deep Neural Network.
• It is used for dimensionality reduction.
• It learns hidden electromagnetic patterns.
• It compresses high-dimensional RF data.
• It automatically extracts important RF characteristics.
• The autoencoder contains:
• • Input Layer
• • Encoder Layers
• • Latent Layer
• • Decoder Layers
• • Output Layer
9. Purpose of Encoder
• The Encoder is the most important section of the autoencoder.
• It compresses RF feature vectors.
• It removes redundant information.
• It learns hidden resonance behavior.
• It captures dielectric dependent RF patterns.
• It converts large RF data into compact latent vectors.
10. Latent Feature Learning
• Latent features are compressed electromagnetic representations.
• They are automatically learned by the neural network.
• The latent space may represent:
• • Resonance shifts
• • Reflection behavior
• • Transmission characteristics
• • Electromagnetic interactions
• • Material dependent RF patterns
• Example:
• 8008 RF Features → 64 Latent Features
11. Encoder Extraction from Autoencoder
• The encoder is extracted using:
• encoder = Model(inputs=autoencoder.input, outputs=autoencoder.get_layer(index=3).output)
• This keeps only the compression section.
• The decoder section is removed.
• Only latent feature extraction is needed during prediction.
12. RF Feature Vector Creation
• All RF responses are concatenated into one feature vector.
• Feature order used:
• • s11mag
• • s11ph
• • s12mag
• • s12ph
• • s21mag
• • s21ph
• • s22mag
• • s22ph
• The exact feature order must be maintained.
13. Feature Scaling
• RF features are normalized using rf_scaler.
• Scaling improves neural network stability.
• Scaling prevents large values from dominating.
• Scaling improves prediction performance.
• The same scaler used during training must be used during testing.
14. Latent Feature Extraction
• The encoder predicts compressed latent vectors.
• Code used:
• latent = encoder.predict(X_scaled)
• The encoder learns important RF scattering behavior.
• The latent vectors contain hidden electromagnetic information.
15. Regression Model
• The latent vectors are passed into the regressor.
• The regressor predicts dielectric constant values.
• The regressor learns the relationship between:
• Latent RF Features → Dielectric Constant (εr)
• The regression model performs final prediction.
16. Electromagnetic Theory Used
• The project is based on electromagnetic propagation principles.
• Wave velocity relation used:
• v = c / √εr
• Resonance relation used:
• fr ∝ 1 / √εr
• Different dielectric materials produce different RF responses.
17. Output Prediction
• Final prediction is displayed as:
• Predicted Dielectric Constant (εr) ≈ XX.XX
• Prediction is clipped between:
• 5 ≤ εr ≤ 80
• This is because the model was trained only within this range.
18. Advantages of the Model
• Automatic RF feature extraction.
• Reduced manual analysis.
• Compact latent electromagnetic representation.
• Better generalization capability.
• Efficient dimensionality reduction.
• Faster prediction process.
• Deep learning based automation.
19. Files Required to Run final.py
• final.py
• autoencoder_model.h5
• er_regressor.pkl
• rf_scaler.pkl
• latent_scaler.pkl
• 20mag.txt
• 20ph.txt
20. Conclusion
• The project demonstrates intelligent dielectric constant prediction using RF S-parameter responses.
• The autoencoder successfully learns hidden electromagnetic behavior.
• The encoder extracts compact latent electromagnetic features.
• The regression model predicts dielectric constant accurately.
• The system combines CST simulations with Deep Learning and Machine Learning techniques.
• The framework can be extended for RF sensing and dielectric material characterization applications.

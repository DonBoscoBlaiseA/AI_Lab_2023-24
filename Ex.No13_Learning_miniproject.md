# Ex.No: 13 Mini Project  
### DATE:                                                                            
### REGISTER NUMBER : 212221040045
### AIM: 
To write a program to train the classifier for Wine Quality Prediction.
###  Algorithm:
1. Load the diabetes dataset and split it into features (`x`) and target (`y`).
2. Split the dataset into training and testing sets using `train_test_split`.
3. Scale the features using `StandardScaler` for both training and testing data.
4. Instantiate the MLP (Multilayer Perceptron) classifier and train it on the scaled training data.
5. Build a Gradio interface to input values for the model, predict diabetes outcomes, and display "YES" or "NO" based on the prediction.

### Program:
```
from google.colab import drive
drive.mount('/content/drive')
import pandas as pd
import numpy as np
import seaborn as sns
import pickle
import matplotlib.pyplot as plt
from sklearn.metrics import accuracy_score
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
wine_dataset = pd.read_csv('/content/drive/MyDrive/Colab Dataset/WineQT.csv')
wine_dataset = wine_dataset.drop(columns = ['Id'])
wine_dataset.head()
wine_dataset.isnull().sum()
plt.figure(figsize=(3,3))
sns.barplot(x = 'quality', y = 'fixed acidity', data = wine_dataset)
correlation = wine_dataset.corr()
plt.figure(figsize = (5,5))
sns.heatmap(correlation, cbar=True, square=True, fmt='.1f', annot=True, annot_kws={'size':8}, cmap='Blues')
X = wine_dataset.drop(columns = ['quality'])
y = wine_dataset['quality'].apply(lambda y_value: 1 if y_value>=7 else 0)
X.head()
y.head()
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state=4)
print(X.shape, X_train.shape, X_test.shape)
model = RandomForestClassifier()
model.fit(X_train.values, y_train)
prediction = model.predict(X_test.values)
print(prediction)
score = accuracy_score(prediction, y_test)
print(score)
pickle.dump(model, open('/content/drive/MyDrive/Colab Notebooks/Flask app/models/model_011', 'wb'))
pip install -U scikit-learn
model_loaded = pickle.load(open('/content/drive/MyDrive/Colab Notebooks/Flask app/models/model_011', 'rb'))
load_prediction = model_loaded.predict(X_test.values)
accuracy_score(load_prediction, y_test)
ip_data = (2.3,0.2,0.9,1.2,0.5,15.0,21.0,0.9946,3.39,0.47,10.0)
numpy_ip_data = np.asarray(ip_data)
reshaped_ip_data = numpy_ip_data.reshape(1, -1)

ip_prediction = model_loaded.predict(reshaped_ip_data)

print(ip_prediction)
if(ip_prediction == 1):
  print("Good Quality Wine")
else:
  print("Bad Quality Wine")
```


### Output:
<img src="https://github.com/user-attachments/assets/cd4d97b9-fee4-4a39-bf45-9cf2f3313eb1" height=600>
<img src="https://github.com/user-attachments/assets/58b23cca-ab57-4b2f-a6ec-ac7598fa301e" height=600>

### Result:
Thus the system was trained successfully and the prediction was carried out.

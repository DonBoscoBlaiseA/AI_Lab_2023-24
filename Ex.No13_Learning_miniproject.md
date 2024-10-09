# Ex.No: 10 Learning – Use Supervised Learning  
### DATE:                                                                            
### REGISTER NUMBER : 212221040045
### AIM: 
To write a program to train the classifier for Diabetes.
###  Algorithm:
1. Load the diabetes dataset and split it into features (`x`) and target (`y`).
2. Split the dataset into training and testing sets using `train_test_split`.
3. Scale the features using `StandardScaler` for both training and testing data.
4. Instantiate the MLP (Multilayer Perceptron) classifier and train it on the scaled training data.
5. Build a Gradio interface to input values for the model, predict diabetes outcomes, and display "YES" or "NO" based on the prediction.

### Program:
```
import numpy as np
import pandas as pd
!pip install gradio
!pip install typing-extensions --upgrade
import gradio as gr

data = pd.read_csv('diabetes.csv')
data.head()

print(data.columns)

x = data.drop(['Outcome'], axis=1)
y = data['Outcome']
print(x[:5])

from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test= train_test_split(x,y)

#scale data
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
x_train_scaled = scaler.fit_transform(x_train)
x_test_scaled = scaler.fit_transform(x_test)

#instatiate model
from sklearn.neural_network import MLPClassifier
model = MLPClassifier(max_iter=1000, alpha=1)
model.fit(x_train, y_train)
print("Model Accuracy on training set:", model.score(x_train, y_train))
print("Model Accuracy on Test Set:", model.score(x_test, y_test))

#create a function for gradio
def diabetes(Pregnancies, Glucose, Blood_Pressure, SkinThickness, Insulin, BMI,Diabetes_Pedigree, Age):
    x = np.array([Pregnancies,Glucose,Blood_Pressure,SkinThickness,Insulin,BMI,Diabetes_Pedigree,Age])
    prediction = model.predict(x.reshape(1, -1))
    if(prediction==0):
      return "NO"
    else:
      return "YES"

outputs = gr.Textbox()
app = gr.Interface(fn=diabetes, inputs=['number','number','number','number','number','number','number','number'], outputs=outputs,description="Detection of Diabeties")
app.launch(share=True)
```

### Output:
<img src="https://github.com/user-attachments/assets/dbdde81b-990f-46cc-8135-be3d451fab8c" height=600>

### Result:
Thus the system was trained successfully and the prediction was carried out.
